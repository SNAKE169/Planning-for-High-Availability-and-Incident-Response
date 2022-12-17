## Availability SLI
### The percentage of successful requests over the last 5m
http_request_total { code =~ "200" }[5m] / http_request_total[5m]

## Latency SLI
### 90% of requests finish in these times
histogram_quantile(0.90, sum(rate(http_request_duration_seconds_bucket{job="ec2"}[30s])) by (le, verb))

## Throughput
### Successful requests per second
sum(rate(http_request_total{code=~"2.."}[1s]))

## Error Budget - Remaining Error Budget
### The error budget is 20%
1 - ((1 - (sum(increase(http_request_total{job="webserver", code="200"}[7d])) by (verb)) /  sum(increase(http_request_total{job="ec2"}[7d])) by (verb)) / (1 - .90))
