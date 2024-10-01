# Open RAN Commercial Traffic Twinning Dataset

Dataset for the paper L. Bonati, R. Shirkhani, C. Fiandrino, S. Maxenti, S. D'Oro, M. Polese, T. Melodia, "Twinning Commercial Network Traces on Experimental Open RAN Platforms," in Proceedings of ACM WiNTECH, Washington, DC, USA, November 2024.

The dataset is available at the following [link](https://repository.library.northeastern.edu/collections/neu:h989sz017). If you use it in your work, please reference the paper above.

# Experimental setup
- Number of Base Stations (BSs): 1
- Channel bandwidth: 10 MHz (50 Physical Resource Blocks (PRBs))
- Number of slices for each BS: 2
- Scheduling policies available to each slice:
    - Policy 0: Round-robin (RR)
    - Policy 2: Proportionally fair (PF)
- Number of User Equipments (UEs): 8
    - Users 1-4 belong to the enhanced Mobile Broadband (eMBB) slice
    - Users 5-8 demand Ultra Reliable and Low Latency Communications (URLLC) traffic
- UE mobility: static

| UE ID   | UE IMSI   |   Traffic Type  |
|------------|------------|------------|
| 1 | 1010123456002 | eMBB | 
| 2 | 1010123456003 | eMBB |
| 3 | 1010123456004 | eMBB |
| 4 | 1010123456005 | eMBB | 
| 5 | 1010123456006 | URLLC |
| 6 | 1010123456007 | URLLC |
| 7 | 1010123456008| URLLC | 
| 8 | 1010123456009 | URLLC | 

- Traffic: The traffic is twinned from a public dataset of LTE network from 3 BSs located in Madrid, Spain.
    - BS1: carrier frequency at 816 MHz
    - BS2: carrier frequency at 1835 MHz
    - BS3: carrier frequency at 2650 MHz
- Number of slices for the BS: 2 (slice_id 0 for eMBB UEs and slice_id 1 for URLLC UEs)
- Slicing configurations: There are 50 PRBs in total to allocate for the two slices.

|  Slice Resouce Allocation  | Slice ID 0 (eMBB: UEs 1-4) PRBs  |  Slice ID 1 (URLLC: UEs 5-8) PRBs  |
|------------|------------|------------|
| Slicing 1 | 9 | 41 |
| Slicing 2 | 21 | 29 |
| Slicing 3 | 30 | 20 |
| Slicing 4 | 39 | 11 |
| Slicing 5 | 50 | 0 |

# Dataset stucture
- There are two compressed files available for downloading:
    - `open-ran-commercial-traffic-twinning-dataset-kmp`, which contains the metrics and the MGEN scripts.
    - `open-ran-commercial-traffic-twinning-dataset-log`, which contains the log files. 
- The dataset has the following structure: cluster_<#>/slicing_<#>/schedualing_<#>
    - 3 cluster configurations (cluster_1, cluster_2, cluster_3)
    - 5 slicings (slicing_1, slicing_2, slicing_3, slicing_4, slicing_5)
    - 2 schedualings (scheduling_0, scheduling_2)
- In total there are 30 combinations of configurations in the available experiments.
- Here is a tree example of directory structure for `RESERVATION-142634` in cluster_1, slicing_1, schedualing_0 for both datasets.
```
├── cluster_1
│   ├── slicing_1
│   │   ├── scheduling_0
│   │   │   ├── RESERVATION-142634
│   │   │   │   ├── bs
│   │   │   │   │   ├── 1010123456002_metrics.csv
│   │   │   │   │   ├── 1010123456003_metrics.csv
│   │   │   │   │   ├── 1010123456004_metrics.csv
│   │   │   │   │   ├── 1010123456005_metrics.csv
│   │   │   │   │   ├── 1010123456006_metrics.csv
│   │   │   │   │   ├── 1010123456007_metrics.csv
│   │   │   │   │   ├── 1010123456008_metrics.csv
│   │   │   │   │   ├── 1010123456009_metrics.csv
│   │   │   │   │   ├── enb_metrics.csv
│   │   │   │   │   ├── mgen-script-scope.mgn
│   │   │   │   ├── ue_001010123456002
│   │   │   │   │   ├── mgen.csv
│   │   │   │   │   ├── mgen-script-scope.mgn
│   │   │   │   │   └── ue_metrics.csv
...
```

```
├── cluster_1
│   ├── slicing_1
│   │   ├── scheduling_0
│   │   │   ├── RESERVATION-142634
│   │   │   │   ├── bs
│   │   │   │   │   └── enb.log
│   │   │   │   ├── ue_001010123456002
│   │   │   │   │   └── ue.log
...
```

- Each experiment has a directory named `RESERVATION-<experiment_id>`
- Inside each experiment directory, there is a directory named `bs` for the base station files, as well as directories named `ue_<IMSI>`, one for each UE, that contains the files related to the specific UE.
- Base Station files:
    - `mgen-script-scope.mgen`: MGEN script that twins the real-world traffic used for generating downlink traffic for the UEs in the experiment. 
    - `<IMSI>_metrics.csv`: PHY- and MAC-layer KPMs collected at the base station for each UE.
    - `enb_metrics.csv`: downlink and uplink bitrate of the network, aggregated for all the UEs served by the base station.
    - `enb.log`: log file of the base station protocol stack.
- UE files: 
    - `mgen-script-scope.mgn`: MGEN script running at the UE, used to start the MGEN listening process.
    - `mgen.csv`: Application-layer KPMs collected from the MGEN logs and converted to a .csv file.
    - `ue_metrics.csv`: PHY- and MAC-layer KPMs collected at the UE side.
    - `ue.log`: log file of the UE cellular protocol stack.
