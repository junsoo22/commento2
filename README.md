# 3주차 과제

## 월별 접속자 수 
```
SELECT
    DATE_FORMAT(createdate, '%Y-%m') AS login_month,
    COUNT(DISTINCT user_id) AS user_count
FROM request_info
GROUP BY DATE_FORMAT(createdate, '%Y-%m')
ORDER BY login_month;
```

##  일자별 접속자 수 
```
SELECT
    createdate,
    COUNT(DISTINCT user_id) AS user_count
FROM request_info
GROUP BY createdate
ORDER BY createdate;
```

## 평균 하루 로그인 수 
```
SELECT
    ROUND(COUNT(*) / COUNT(DISTINCT createdate), 2) AS avg_daily_login
FROM request_info;

```

## 휴일 제외 로그인 수 
```
-- 휴일 테이블 예시
CREATE TABLE holidays (
    holiday_date DATE PRIMARY KEY,
    holiday_name VARCHAR(50)
);

-- 제외한 로그인 수
SELECT COUNT(*)
FROM request_info
WHERE createdate NOT IN (SELECT holiday_date FROM holidays);
```


##  부서별 월별 로그인 수 
```
SELECT
    u.hr_organ,
    DATE_FORMAT(r.createdate, '%Y-%m') AS login_month,
    COUNT(*) AS login_count
FROM request_info r
JOIN user u ON r.user_id = u.user_id
GROUP BY u.hr_organ, DATE_FORMAT(r.createdate, '%Y-%m')
ORDER BY u.hr_organ, login_month;
```
