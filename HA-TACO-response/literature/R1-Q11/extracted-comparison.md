# R1-Q11 literature extraction

## Sources and access status

- Fu et al., *MiniMCTAD: Minimalist Monte Carlo Transport Architecture Design*, ISPA 2021, DOI: 10.1109/ISPA-BDCloud-SocialCom-SustainCom52081.2021.00016. Full paper acquired as `Fu2021-MiniMCTAD.pdf`.
- Zhang, Li, and Zhang, *A 128-core scalable architecture for Monte Carlo application*, Computer Engineering & Science 45(4), 2023, pp. 590--598, DOI: 10.3969/j.issn.1007-130X.2023.04.004. Full paper supplied by the author as `一种面向蒙特卡洛程序的128核可扩展体系结构.pdf` and checked against the archived official metadata.

## Verified reported parameters

| Parameter | MiniMCTAD (Fu et al.) | 128-core architecture (Zhang et al.) |
|---|---|---|
| Application | Quicksilver, an MC-transport proxy for Mercury | Quicksilver |
| Evaluation | gem5 20.01 full-system + McPAT 1.3 | gem5 simulation; Intel VTune is additionally used for host-side characterization |
| Technology | 28 nm | N/R |
| ISA/core | ARM-compatible, four-stage in-order MiniMCTAD core | ARM HPI core derived from gem5 MinorCPU, four-stage in-order pipeline |
| Clock | 2.2 GHz | 2.2 GHz |
| Evaluated scale | 4 and 8 MiniMCTAD cores; 4 Cortex-A15 OoO cores as baseline | 128 cores; single core as scaling baseline |
| L1 | Private 32 kB I-cache and 32 kB D-cache, 64-B line | Private 32 kB I-cache (direct mapped, 2 MSHRs) and 32 kB D-cache (2-way, 2 MSHRs), 64-B line |
| L2 | Shared per tile; selected 256 kB for 4 cores and 512 kB for 8 cores | 256 kB per core, 16-way, 4 MSHRs; shared within each 32-core Cluster (8 MB/Cluster) |
| LLC | No L3 reported | No L3: the evaluated 16 MB L3 provides less benefit than adding L2 capacity |
| Main memory | 4 GB HBM2, 8 channels | 4 GB HBM2, 8 channels; DDR4-2400 comparison shows similar performance at up to 32 cores |
| Parallel/runtime policy | OpenMP 4.5 | OpenMP dynamic scheduling for the parallel loop |
| Absolute modeled area/power | 4-core MiniMCTAD: 4.85 mm2, 76 mW; 8-core MiniMCTAD: 8.92 mm2, 148 mW | N/R; the paper does not report area, power, or energy efficiency |
| Same-core-count result | A MiniMCTAD core is 41% slower than Cortex-A15, but has 6.26x area and 3.92x power advantages; consequently 4.45x Perf/W and 2.78x Perf/area | N/A; the paper evaluates scaling relative to its own one-core configuration |
| Increased-core-count result | 8 MiniMCTAD cores deliver about 1.416x the performance of the 4-core Cortex-A15 system; 4.56x Perf/W and 3.01x Perf/area are reported for this unequal-core-count comparison | 128 cores achieve 90x speedup over one core and 70.1% parallel efficiency |

## Zhang et al. design-space and scaling details

- Before clustering, the shared-L2 baseline reaches 83.4% efficiency at 32 cores but only 54.5% at 64 cores; shared-L2 latency/bandwidth contention is identified as the limiting factor.
- The selected cache is 256 kB/core and 16-way associative. Increasing L2 from 128 kB to 256 kB improves performance by 4.4% at 16-way associativity, whereas increasing it from 256 kB to 512 kB adds only 2.7%.
- A 16 MB inclusive L3 is tested but rejected because its benefit diminishes with core count and is smaller than spending the capacity on L2.
- The Cluster sweep covers 1, 2, 4, 8, 16, 32, and 64 cores per Cluster. A 32-core Cluster gives the lowest average L2 access latency and is selected.
- At 64 cores, clustering raises scaling efficiency from 54.5% to 72.7%. Adding OpenMP dynamic scheduling raises it further to 85.6%, a 17.3% performance improvement over static scheduling at 64 cores.
- At 128 cores, the combined 32-core Cluster organization and dynamic scheduling reach 90x speedup and 70.1% efficiency; performance is reported as 53.3% above the corresponding static-scheduling strategy.

## MiniMCTAD workload details

The reported Quicksilver input uses a 16 x 16 x 16 cm simulation, 163,840 particles, absorption/fission/scattering ratios of 0.04/0.05/1, `nuBar=1.6`, and `dt=2e-9 s`. Performance sampling uses 180 particle-tracking regions of interest. These settings are not identical to the FluxArch P1/P2/CTS2/Homogeneous inputs, so the absolute runtime and reported ratios must not be treated as a direct FluxArch-vs-MiniMCTAD speedup.

## Safe paper-facing comparison boundary

The following quantities can be placed side by side: evaluation method, process node, clock, core type, core count, cache/memory organization, workload family, and each paper's author-reported result relative to its own baseline. The result column must explicitly say "relative to each work's own baseline." FluxArch must not be claimed to outperform MiniMCTAD or the Zhang architecture by dividing unrelated throughput, runtime, power, or area values.

Zhang et al. can support a quantitative scalability comparison, but not an area or energy-efficiency comparison: it reports no process node, area, power, or performance-per-watt/area. The most defensible entries are its 32-core Cluster, 256 kB L2 per core, 90x self-speedup at 128 cores, and 70.1% self-scaling efficiency. Its OpenMP dynamic scheduling must be mentioned because the final 128-core result is a hardware-software co-design result rather than an architecture-only result.
