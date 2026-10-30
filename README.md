# K6 lab results

## Part 0
- Step 0.1, http_req_duration: 295.66 ms
- Step 0.2, requests: 80, rate: 3.800936/s, p(95): 265.91 ms
- เหตุผลที่ rate ต่ำกว่า 5: แต่ละ VU ต้องรอการตอบกลับและ sleep(1) วินาที จึงไม่ได้ส่ง request ต่อเนื่องตลอดเวลา