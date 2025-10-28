## 이미 생성된 테이블에 특정 컬럼을 추가해야 할 경우, create가 아닌 update 옵션으로 처리 가능하다.

3. select * from all_sequences
 {executed in 7 msec}
Hibernate: 
    
    alter table IFT_OB_INVOICE_RESULT 
       add API_ID varchar2(30 char) not null
2025-10-28 13:13:53,635 DEBUG 27456 [           main] jdbc.sqltiming                           sqlTimingOccurr [368 ] :  com.p6spy.engine.wrapper.StatementWrapper.execute(StatementWrapper.java:114)
3. alter table IFT_OB_INVOICE_RESULT 
       add API_ID varchar2(30 char) not null
 {executed in 89 msec}
2025-10-28 13:13:58,067 DEBUG 27456 [           main] jdbc.sqltiming                           sqlTimingOccurr [368 ] :  com.p6spy.engine.wrapper.PreparedStatementWrapper.executeQuery(PreparedStatementWrapper.java:78)
3. select * from "LF_DEV"."IFT_DAS_ORDER_HR" where 1=0
 {executed in 12 msec}
2025-10-28 13:13:58,080 DEBUG 27456 [           main] jdbc.sqltiming                           sqlTimingOccurr [368 ] :  com.p6spy.engine.wrapper.PreparedStatementWrapper.executeQuery(PreparedStatementWrapper.java:78)
3. select * from "LF_DEV"."IFT_DAS_ORDER_HR" where 1=0
 {executed in 5 msec}
2025-10-28 13:13:58,092 DEBUG 27456 [           main] jdbc.sqltiming                           sqlTimingOccurr [368 ] :  com.p6spy.engine.wrapper.PreparedStatementWrapper.executeQuery(PreparedStatementWrapper.java:78)
3. select * from "LF_DEV"."IFT_DAS_ORDER_HR" where 1=0
 {executed in 5 msec}
2025-10-28 13:13:58,104 DEBUG 27456 [           main] jdbc.sqltiming                           sqlTimingOccurr [368 ] :  com.p6spy.engine.wrapper.PreparedStatementWrapper.executeQuery(PreparedStatementWrapper.java:78)
3. select * from "LF_DEV"."IFT_DAS_ORDER_HR" where 1=0
 {executed in 5 msec}
2025-10-28 13:13:58,116 DEBUG 27456 [           main] jdbc.sqltiming                           sqlTimingOccurr [368 ] :  com.p6spy.engine.wrapper.PreparedStatementWrapper.executeQuery(PreparedStatementWrapper.java:78)
3. select * from "LF_DEV"."IFT_DAS_ORDER_HR" where 1=0
 {executed in 5 msec}
2025-10-28 13:14:02,721 DEBUG 27456 [           main] jdbc.sqltiming                           sqlTimingOccurr [368 ] :  com.p6spy.engine.wrapper.PreparedStatementWrapper.executeQuery(PreparedStatementWrapper.java:78)
3. select * from "LF_DEV"."IFT_DAS_WAVE" where 1=0
 {executed in 6 msec}
2025-10-28 13:14:02,735 DEBUG 27456 [           main] jdbc.sqltiming                           sqlTimingOccurr [368 ] :  com.p6spy.engine.wrapper.PreparedStatementWrapper.executeQuery(PreparedStatementWrapper.java:78)
3. select * from "LF_DEV"."IFT_DAS_WAVE" where 1=0
 {executed in 6 msec}
2025-10-28 13:14:02,745 DEBUG 27456 [           main] jdbc.sqltiming                           sqlTimingOccurr [368 ] :  com.p6spy.engine.wrapper.PreparedStatementWrapper.executeQuery(PreparedStatementWrapper.java:78)
3. select * from "LF_DEV"."IFT_DAS_WAVE" where 1=0
 {executed in 4 msec}
2025-10-28 13:14:02,756 DEBUG 27456 [           main] jdbc.sqltiming                           sqlTimingOccurr [368 ] :  com.p6spy.engine.wrapper.PreparedStatementWrapper.executeQuery(PreparedStatementWrapper.java:78)
3. select * from "LF_DEV"."IFT_DAS_WAVE" where 1=0
 {executed in 5 msec}
2025-10-28 13:14:02,785 DEBUG 27456 [           main] jdbc.sqltiming                           sqlTimingOccurr [368 ] :  com.p6spy.engine.wrapper.PreparedStatementWrapper.executeQuery(PreparedStatementWrapper.java:78)
3. select * from "LF_DEV"."IFT_RCV_INB_HR" where 1=0
 {executed in 7 msec}
2025-10-28 13:14:02,810 DEBUG 27456 [           main] jdbc.sqltiming                           sqlTimingOccurr [368 ] :  com.p6spy.engine.wrapper.PreparedStatementWrapper.executeQuery(PreparedStatementWrapper.java:78)
3. select * from "LF_DEV"."IFT_RCV_MD_ITEM" where 1=0
 {executed in 7 msec}
2025-10-28 13:14:02,877 DEBUG 27456 [           main] jdbc.sqltiming                           sqlTimingOccurr [368 ] :  com.p6spy.engine.wrapper.PreparedStatementWrapper.executeQuery(PreparedStatementWrapper.java:78)
3. select * from "LF_DEV"."IFT_RCV_OUTB_HR" where 1=0
 {executed in 48 msec}
