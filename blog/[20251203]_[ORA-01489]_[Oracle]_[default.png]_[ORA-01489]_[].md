## ORA-01489: result of string concatenation is too long

### Join 결과가 없는 경우에도 발생할 수 있음
```sql
SELECT LISTAGG(J.JOB_NO, ', ') WITHIN GROUP (ORDER BY J.JOB_NO)
    FROM WMT_TA_JOB J
        WHERE J.WH_ID = T.WH_ID
            AND J.TO_CELL_ID = T.CELL_ID
            AND J.REPL_JOB_NO = T.REPL_NO
-- 조건에 맞는 JOB_NO가 조회되지 않을 경우 ORA-01489 발생


-- Solution
SELECT LISTAGG(COALESCE(J.JOB_NO, null), ', ') WITHIN GROUP (ORDER BY J.JOB_NO)
    FROM WMT_TA_JOB J
        WHERE J.WH_ID = T.WH_ID
            AND J.TO_CELL_ID = T.CELL_ID
            AND J.REPL_JOB_NO = T.REPL_NO
```