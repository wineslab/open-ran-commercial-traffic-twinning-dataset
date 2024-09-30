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
    - Users 1-4 demand Enhanced Mobile Broadband (eMBB) traffic
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
- The dataset has the following structure: 3 clusters, 5 slicings, 2 schedualing. In total 30 combinations.
    - cluster/slicing/schedualing
- Each experiment has a directory named `RESERVATION-<experiment_id>`
- Inside each experiment directory, there is a directory named `bs` for the base station files, and there is one directory named `ue_<IMSI>` for each UE for the files related to that UE.
- Base Station files:
    - `mgen-script-scope.mgen`: The MGEN script that twins the real-world traffic used for generating traffic for all the UEs in the experiment. 
    - `<IMSI>_metrics.csv`: PHY- and MAC-layer KMPs collected at the base station for each UE.
    - `end_metrics.csv`: downlink bitrate and uplink bitrate for all the UEs in the experiment.
    - `enb.log`: log file collected at the base station.
- UE files: 
    - `mgen.log`: MGEN logs for the UE that are from the APP layer.
    - `mgen.csv`: Same mgen.log data converted to a csv table.
    - `ue_metrics.csv`: PHY- and MAC-layer KPMs collected at the ue side. (?)
    - `ue.log`: log file collected at each UE.
