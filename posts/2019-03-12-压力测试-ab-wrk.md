---
title: 压力测试 ab wrk
author: fan
type: post
date: 2019-03-12T08:37:12+00:00
excerpt: |
  ab -n1000 -c10 http://localhost:8080/
  wrk -c10 -t10 -d5 http://localhost:8080/
url: /压力测试-ab-wrk/
categories:
  - Go
  - 操作系统

---
压力测试 ab wrk

#### ab为Apache内置

ab -n1000 -c10 http://localhost:8080/
  
1000次请求 10个并发,分析 Requests per second 字段

    Server Software:        Iris:
    Server Hostname:        localhost
    Server Port:            8080
    Document Path:          /
    Document Length:        5368 bytes
    Concurrency Level:      10
    Time taken for tests:   0.758 seconds
    Complete requests:      1000
    Failed requests:        0
    Total transferred:      5580884 bytes
    HTML transferred:       5368000 bytes
    Requests per second:    1318.86 [#/sec] (mean)
    Time per request:       7.582 [ms] (mean)
    Time per request:       0.758 [ms] (mean, across all concurrent requests)
    Transfer rate:          7187.91 [Kbytes/sec] received
    Connection Times (ms)
                  min  mean[+/-sd] median   max
    Connect:        0    0   0.2      0       2
    Processing:     1    7  11.5      4     124
    Waiting:        1    7  11.4      3     123
    Total:          1    7  11.5      4     125
    Percentage of the requests served within a certain time (ms)
      50%      4
      66%      6
      75%      8
      80%      9
      90%     14
      95%     22
      98%     43
      99%     57
     100%    125 (longest request)
    

#### wrk：brew install wrk

wrk -c10 -t10 -d5 http://localhost:8080/
  
10个连接 10个线程，持续5秒，分析 Requests/sec 请求次数/秒

<pre><code class="line-numbers">Running 5s test @ http://localhost:8080
  10 threads and 10 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     6.57ms   10.77ms 139.45ms   95.19%
    Req/Sec   212.90     51.14   383.00     74.85%
  10604 requests in 5.02s, 57.00MB read
Requests/sec:   2114.45
Transfer/sec:     11.37MB
</code></pre>

简单高效，ab默认短连接(http1.0)，wrk默认长连接
  
分析结果：
  
&#8211; 减少数据库依赖
  
&#8211; 模板尽量少使用动态数据