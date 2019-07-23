---
title: SQLServerDataSource 멤버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7e749bc5-d765-4864-be2b-7822d4c20c09
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 800f87c82987396743ec4c0c278444c4ba61d49b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971412"
---
# <a name="sqlserverdatasource-members"></a>SQLServerDataSource 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에는 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스에 의해 노출되는 멤버가 나와 있습니다.  
  
## <a name="constructors"></a>생성자  
  
|속성|설명|  
|----------|-----------------|  
|[SQLServerDataSource ()](../../../connect/jdbc/reference/sqlserverdatasource-constructor.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 클래스의 새 인스턴스를 초기화합니다.|  
  
## <a name="fields"></a>필드  
 없음  
  
## <a name="inherited-fields"></a>상속된 필드  
 없음  
  
## <a name="methods"></a>메서드  
  
|속성|설명|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|**Applicationintent** 된 연결 속성의 값을 반환 합니다.|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|응용 프로그램 이름을 반환합니다.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체가 나타내는 데이터 원본과의 연결을 설정합니다.|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|데이터베이스 이름을 반환합니다.|  
|[getDisableStatementPooling](../../../connect/jdbc/reference/getdisablestatementpooling-method-sqlserverdatasource.md)|**Statementpoolingcachesize** connection 속성의 값을 반환 합니다. 이 설정은이 연결에 대해 문 풀링이 사용 되는지 여부를 제어 합니다.|  
|[getEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/getenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource.md)|**EnablePrepareOnFirstPreparedStatementCall** connection 속성의 값을 반환 합니다.|  
|[getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md)|encrypt 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 반환합니다.|  
|[getDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|데이터 원본에 대한 설명을 반환합니다.|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|데이터베이스 미러링 구성에 사용되는 장애 조치(Failover) 서버의 이름을 반환합니다.|  
|[getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md)|SQL Server SSL(Secure Sockets Layer) 인증서의 유효성을 검사하는 데 사용되는 호스트 이름을 반환합니다.|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름을 반환합니다.|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|lastUpdateCount 속성이 사용되는지 여부를 나타내는 **boolean** 값을 반환합니다.|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|데이터베이스에서 잠금 시간 초과가 보고되기 전까지 대기하는 시간(밀리초)을 나타내는 **int** 값을 반환합니다.|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체가 연결을 시도하는 동안 대기하는 시간(초)을 반환합니다.|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|모든 로깅 및 추적 메시지에 사용할 문자 출력 스트림을 반환합니다.|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|**MultiSubnetFailover** connection 속성의 값을 반환 합니다.|  
|[getPacketSize](../../../connect/jdbc/reference/getpacketsize-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와의 통신에 사용되는 현재 네트워크 패킷 크기(바이트)를 반환합니다.|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와의 통신에 사용되는 현재 포트 번호를 반환합니다.|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md)|이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체에 대한 참조를 반환합니다.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverdatasource.md)|이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체에 대한 응답 버퍼링 모드를 반환합니다.|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체를 사용하여 만들어진 모든 결과 집합에 사용되는 기본 커서 유형을 반환합니다.|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|문자열 매개 변수를 서버에 유니코드 형식으로 보낼 수 있는지 여부를 나타내는 **Boolean** 값을 반환합니다.|  
|[getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|**SendTimeAsDatetime** connection 속성의 설정을 반환 합니다.|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행하고 있는 컴퓨터의 이름을 반환합니다.|  
|[getServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource.md)|**ServerPreparedStatementDiscardThreshold** connection 속성의 값을 반환 합니다.|  
|[getStatementPoolingCacheSize](../../../connect/jdbc/reference/getstatementpoolingcachesize-method-sqlserverdatasource.md)|이 연결에 대해 준비 된 문 캐시의 크기를 반환 합니다.|  
|[getTrustManagerClass](../../../connect/jdbc/reference/gettrustmanagerclass-method-sqlserverdatasource.md)|TrustManagerClass 연결 속성의 문자열 값을 반환 합니다.|  
|[getTrustManagerConstructorArg](../../../connect/jdbc/reference/gettrustmanagerconstructorarg-method-sqlserverdatasource.md)|TrustManagerConstructorArg connection 속성의 문자열 값을 반환 합니다.|  
|[getTrustServerCertificate](../../../connect/jdbc/reference/gettrustservercertificate-method-sqlserverdatasource.md)|trustServerCertificate 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 반환합니다.|  
|[getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md)|인증서 trustStore 파일의 경로(파일 이름 포함)를 반환합니다.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|데이터 원본에 연결하는 데 사용되는 URL을 반환합니다.|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|데이터 원본에 연결하는 데 사용되는 사용자 이름을 반환합니다.|  
|[getUseSQLServerBaseDate](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|useSQLServerBaseDate 연결 속성의 설정을 반환합니다.|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|데이터 원본에 연결하는 데 사용되는 클라이언트 컴퓨터 이름을 반환합니다.|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|SQL 상태를 XOPEN 규격 상태로 변환할 수 있는지 여부를 나타내는 **Boolean** 값을 반환합니다.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)|이 데이터 원본 개체가 지정된 인터페이스에 대한 래퍼인지 여부를 나타냅니다.|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|**Applicationintent** 연결 속성의 값을 설정 합니다.|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|응용 프로그램 이름을 설정합니다.|  
|[setAuthenticationScheme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|응용 프로그램에서 사용하려는 통합 보안의 종류를 나타냅니다.|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|연결할 데이터베이스 이름을 설정합니다.|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|데이터 원본에 대한 설명을 설정합니다.|  
|[setDisableStatementPooling](../../../connect/jdbc/reference/setdisablestatementpooling-method-sqlserverdatasource.md)|문 풀링을 true 또는 false로 설정 합니다.|  
|[setEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/setenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource.md)|**EnablePrepareOnFirstPreparedStatementCall** connection 속성의 새 값을 지정 합니다.|  
|[setEncrypt](../../../connect/jdbc/reference/setencrypt-method-sqlserverdatasource.md)|encrypt 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 설정합니다.|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|데이터베이스 미러링 구성에 사용되는 장애 조치(Failover) 서버의 이름을 설정합니다.|  
|[setHostNameInCertificate](../../../connect/jdbc/reference/sethostnameincertificate-method-sqlserverdatasource.md)|SQL Server SSL(Secure Sockets Layer) 인증서의 유효성을 검사하는 데 사용할 호스트 이름을 설정합니다.|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름을 설정합니다.|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|integratedSecurity 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 설정합니다.|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|lastUpdateCount 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 설정합니다.|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|데이터베이스에서 잠금 시간 초과가 보고되기 전까지 대기하는 시간(밀리초)을 나타내는 **int** 값을 설정합니다.|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체가 연결을 시도하는 동안 대기하는 시간(초)을 설정합니다.|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|모든 로깅 및 추적 메시지에 사용할 문자 출력 스트림을 설정합니다.|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|**MultiSubnetFailover** connection 속성의 값을 설정 합니다.|  
|[setPacketSize](../../../connect/jdbc/reference/setpacketsize-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와의 통신에 사용되는 현재 네트워크 패킷 크기(바이트)를 설정합니다.|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결하는 데 사용되는 암호를 설정합니다.|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와의 통신에 사용되는 포트 번호를 설정합니다.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)|이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체를 사용하여 만들어진 연결에 대한 응답 버퍼링 모드를 설정합니다.|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체를 사용하여 만들어진 모든 결과 집합에 사용되는 기본 커서 유형을 설정합니다.|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|문자열 매개 변수를 서버에 유니코드 형식으로 보낼 수 있는지 여부를 나타내는 **Boolean** 값을 설정합니다.|  
|[setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)|java.sql.Time 값을 서버에 보내는 방식을 지정합니다.|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행하고 있는 컴퓨터의 이름을 설정합니다.|  
|[setServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/setserverpreparedstatementdiscardthreshold-method-sqlserverdatasource.md)|**ServerPreparedStatementDiscardThreshold** connection 속성의 새 값을 설정 합니다.|  
|[setStatementPoolingCacheSize](../../../connect/jdbc/reference/setstatementpoolingcachesize-method-sqlserverdatasource.md)|이 연결에 대해 준비 된 문 캐시의 크기를 설정 합니다.|  
|[setTrustManagerClass](../../../connect/jdbc/reference/settrustmanagerclass-method-sqlserverdatasource.md)|TrustManagerClass 연결 속성의 문자열 값을 설정 합니다.|  
|[setTrustManagerConstructorArg](../../../connect/jdbc/reference/settrustmanagerconstructorarg-method-sqlserverdatasource.md)|TrustManagerConstructorArg connection 속성의 문자열 값을 설정 합니다.|  
|[setTrustServerCertificate](../../../connect/jdbc/reference/settrustservercertificate-method-sqlserverdatasource.md)|trustServerCertificate 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 설정합니다.|  
|[setTrustStore](../../../connect/jdbc/reference/settruststore-method-sqlserverdatasource.md)|인증서 trustStore 파일의 경로(파일 이름 포함)를 설정합니다.|  
|[setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md)|trustStore 데이터의 무결성을 검사하는 데 사용되는 암호를 설정합니다.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|데이터 원본에 연결하는 데 사용되는 URL을 설정합니다.|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|데이터 원본에 연결하는 데 사용되는 사용자 이름을 설정합니다.|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|데이터 원본에 연결하는 데 사용되는 클라이언트 컴퓨터의 이름을 설정합니다.|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|SQL 상태를 XOPEN 규격 상태로 변환할 수 있는지 여부를 나타내는 **Boolean** 값을 설정합니다.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)|[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 관련 메서드에 액세스할 수 있도록 지정된 인터페이스를 구현하는 개체를 반환합니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
