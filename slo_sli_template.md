# API Service

| Category     | SLI | SLO                                                                                                         |
|--------------|-----|-------------------------------------------------------------------------------------------------------------|
| Availability | Ratio of successful requests to total requests in the last 10 minutes    | 99%                                    |
| Latency      | Ratio of the requests that took 100ms or less to the total requests      | 90% of requests below 100ms            |
| Error Budget | The percentage of the error budget used  | Error budget is defined at 20%. This means that 20% of the requests can fail and still be within the budget |
| Throughput   | Number of successful requests in 1 minutes divided by 60   | 5 RPS indicates the application is functioning            |
