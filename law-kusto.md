* Graph of LAW matrics for a specific VM 

```
let vm_name = "ene4vpcadm03";
Perf 
| where Computer contains vm_name 
| where (CounterName == "% Committed Bytes In use") 
| summarize avg(CounterValue) by Computer, bin(TimeGenerated, 60m) 
| render timechart
```

* OS Matrics Data ingestion into LAW

```
Heartbeat
| extend E2EIngestionLatencyMin = todouble(datetime_diff("Second",ingestion_time(),TimeGenerated))/60
| extend AgentLatencyMin = todouble(datetime_diff("Second",_TimeReceived,TimeGenerated))/60
| summarize percentiles(E2EIngestionLatencyMin,50,95), percentiles(AgentLatencyMin,50,95) by bin(TimeGenerated,30m)
| render timechart
```
