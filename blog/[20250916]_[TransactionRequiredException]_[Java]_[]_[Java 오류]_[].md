# javax.persistence.TransactionRequiredException

javax.persistence.TransactionRequiredException: Executing an update/delete query
	at org.hibernate.internal.AbstractSharedSessionContract.checkTransactionNeededForUpdateOperation(AbstractSharedSessionContract.java:445)
	at org.hibernate.query.internal.AbstractProducedQuery.executeUpdate(AbstractProducedQuery.java:1692)
	at com.querydsl.jpa.impl.JPAUpdateClause.execute(JPAUpdateClause.java:76)
	at com.slp.module.ifs.outbound.sender.repository.OutbResultRepoCustomImpl.updateRetryIfStatus(OutbResultRepoCustomImpl.java:47)
	at com.slp.module.ifs.outbound.sender.repository.OutbResultRepoCustomImpl$$FastClassBySpringCGLIB$$f7207c27.invoke(<generated>)
	at org.springframework.cglib.proxy.MethodProxy.invoke(MethodProxy.java:218)



