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

| A1 | Smoke | 1 | 0.524518/s | 368.99 ms | 377.49 ms | 0% | 100% |
| A2 | Average load | 3 | 1.307582/s | 371.3 ms | 658.68 ms | 0% | 100% |