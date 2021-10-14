* Graph of LAW matrics for a specific VM 

```
let vm_name = "ene4vpcadm03";
Perf | where Computer contains vm_name | where (CounterName == "% Committed Bytes In use") | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 60m) | render timechart
```
