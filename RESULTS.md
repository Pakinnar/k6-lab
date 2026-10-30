# K6 lab results

## Part 0
- Step 0.1, http_req_duration: 295.66 ms
- Step 0.2, requests: 80, rate: 3.800936/s, p(95): 265.91 ms
- Step 0.3, iterations: 20, rate: 3.370549/s, p(95): 276.93 ms
- Step 0.4, checks: 3/3 passed, http_req_duration p(95): 388.17 ms, http_req_failed: 0%
- Step 0.5, request without token: passed, status 401, p(95): 260.04 ms
- Step 0.6, normal run: p(95) 374.3 ms, exit code 0
- Step 0.6, run with P95=300: threshold failed, exit code 99
- Step 0.7, passed rules: p(95)<1000, p(99)<1500, checks>0.99, http_req_failed<0.01
- Step 0.7, measured p(95): 382.12 ms, p(99): 398.21 ms
- Step 0.7, changed p(95) limit to 1 ms; threshold failed, exit code: 99
- Step 0.8, bug: ใช้ชื่อ pepperoni และ knife ตัวพิมพ์เล็ก แต่ API ต้องการ Pepperoni และ Knife แบบตัวพิมพ์ใหญ่ จึงไม่ถูกตัดออก
- Step 0.8, หลังแก้ไขแล้ว checks ทั้งหมดผ่าน

| Step | Test type | Users | Req/s | p(95) | Max | Failed | Checks |
| ---- | --------- | ----- | ----- | ----- | --- | ------ | ------ |
| A1 | Smoke | 1 | 0.524518/s | 368.99 ms | 377.49 ms | 0% | 100% |
| A2 | Average load | 3 | 1.307582/s | 371.3 ms | 658.68 ms | 0% | 100% |
| A3 | Stress | 5 | 2.097755/s | 369.23 ms | 791.01 ms | 0% | 100% |
| A4 | Spike | 5 | 1.073722/s | 374.81 ms | 423.66 ms | 0% | 100% |
| A5 | Soak | 2 | 0.98885/s | 376.28 ms | 934.02 ms | 0% | 100% |

## Part B

1. The results table for Steps A1 to A5 is shown above.

2. The request rate stayed below 5 requests per second because each VU waits for the HTTP response and then sleeps for one second. Therefore, the five VUs do not send requests continuously.

3. The p(95) response time was very similar between the average-load test and the stress test. This suggests that QuickPizza was still inside its operational envelope at 5 VUs.

4. The response time returned to approximately its previous level about 5 seconds after the spike, during the ramp-down from 5 VUs to 1 VU.

5. The response time and error rate did not get worse over time. A long soak test could reveal a memory leak.

6. The p(95) is used instead of the average because the average can hide slow requests. p(95) shows the response time experienced by the slower 5% of requests.

7. Tests over the internet can produce different results because of network latency and congestion. The public QuickPizza server may also be shared with other users.

8. A test with hundreds of users could overload the site, harm its availability, and be considered an unauthorized denial-of-service attack.

9. Vague requirement: “The application should be fast.”

   Testable requirement: “With 3 users for 30 seconds, 95% of requests must finish within 1 second, 99% within 1.5 seconds, and fewer than 1% may fail.”

   Example K6 thresholds:
   
   ```javascript
   thresholds: {
     http_req_failed: ['rate<0.01'],
     http_req_duration: ['p(95)<1000', 'p(99)<1500'],
   }
   ```
