# org.springframework.dao.InvalidDataAccessApiUsageException

org.springframework.dao.InvalidDataAccessApiUsageException: Parameter value [\] did not match expected type [java.lang.String (n/a)]; nested exception is java.lang.IllegalArgumentException: Parameter value [\] did not match expected type [java.lang.String (n/a)]
	at org.springframework.orm.jpa.EntityManagerFactoryUtils.convertJpaAccessExceptionIfPossible(EntityManagerFactoryUtils.java:374)
	at org.springframework.orm.jpa.vendor.HibernateJpaDialect.translateExceptionIfPossible(HibernateJpaDialect.java:235)
	at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.translateExceptionIfPossible(AbstractEntityManagerFactoryBean.java:551)
	at org.springframework.dao.support.ChainedPersistenceExceptionTranslator.translateExceptionIfPossible(ChainedPersistenceExceptionTranslator.java:61)
	at org.springframework.dao.support.DataAccessUtils.translateIfNecessary(DataAccessUtils.java:242)
	at org.springframework.dao.support.PersistenceExceptionTranslationInterceptor.invoke(PersistenceExceptionTranslationInterceptor.java:152)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186)
	at org.springframework.data.jpa.repository.support.CrudMethodMetadataPostProcessor$CrudMethodMetadataPopulatingMethodInterceptor.invoke(CrudMethodMetadataPostProcessor.java:145)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186)
	at org.springframework.aop.interceptor.ExposeInvocationInterceptor.invoke(ExposeInvocationInterceptor.java:97)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186)
	at org.springframework.aop.framework.JdkDynamicAopProxy.invoke(JdkDynamicAopProxy.java:215)
	at jdk.proxy2/jdk.proxy2.$Proxy272.findAllByPartnerNmContaining(Unknown Source)
	at com.slp.module.ifs.item.receiver.service.ItemMasterRcvService.savePartnerItemLabel(ItemMasterRcvService.java:181)
	at com.slp.module.ifs.item.receiver.service.ItemMasterRcvService.create(ItemMasterRcvService.java:197)
	at com.slp.module.ifs.common.api.receiver.service.ApiReceiverExecutor.lambda$execute$0(ApiReceiverExecutor.java:50)
	at com.slp.boot.database.DefaultTxTrigger.newTx(DefaultTxTrigger.java:20)




