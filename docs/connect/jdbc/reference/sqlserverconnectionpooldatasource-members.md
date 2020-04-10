---
title: SQLServerConnectionPoolDataSource 멤버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: dac0337e-8088-488c-a25a-801a2190f6ca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e5f75ad27e2e6a346adc098f59f5c54144bafb4d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922001"
---
# <a name="sqlserverconnectionpooldatasource-members"></a>SQLServerConnectionPoolDataSource 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에는 [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) 클래스에 의해 노출되는 멤버가 나와 있습니다.  
  
## <a name="constructors"></a>생성자  
  
|속성|Description|  
|----------|-----------------|  
|[SQLServerConnectionPoolDataSource ()](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-constructor.md)|[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) 클래스의 새 인스턴스를 초기화합니다.|  
  
## <a name="fields"></a>필드  
 없음  
  
## <a name="inherited-fields"></a>상속된 필드  
 없음  
  
## <a name="methods"></a>메서드  
  
|속성|Description|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며 **applicationIntent** 연결 속성의 값을 반환합니다.|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 애플리케이션 이름을 반환합니다.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 이 DataSource 개체가 나타내는 데이터 원본과의 연결을 설정합니다.|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 데이터베이스 이름을 반환합니다.|  
|[getDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 데이터 원본에 대한 설명을 반환합니다.|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 데이터베이스 미러링 구성에 사용되는 장애 조치(Failover) 서버의 이름을 반환합니다.|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름을 반환합니다.|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, lastUpdateCount 속성이 사용되는지 여부를 나타내는 **boolean** 값을 반환합니다.|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 데이터베이스에서 잠금 시간 초과가 보고되기 전까지 대기하는 시간(밀리초)을 나타내는 **int** 값을 반환합니다.|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 이 DataSource 개체에서 연결을 시도하는 동안 대기하는 시간(초)을 반환합니다.|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 모든 로깅 및 추적 메시지에 사용할 문자 출력 스트림을 반환합니다.|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며 **multiSubnetFailover** 연결 속성의 값을 반환합니다.|  
|[getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)|풀링된 연결로 사용할 수 있는 실제 데이터베이스 연결을 설정합니다.|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와의 통신에 사용되는 현재 포트 번호를 반환합니다.|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverconnectionpooldatasource.md)|이 DataSource 개체에 대한 참조를 반환합니다.|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 이 DataSource 개체를 사용하여 만들어진 모든 결과 집합에 사용되는 기본 커서 유형을 반환합니다.|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 문자열 매개 변수를 유니코드 형식으로 서버에 보낼 수 있는지 여부를 나타내는 **Boolean** 값을 반환합니다.|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행하고 있는 컴퓨터의 이름을 반환합니다.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 데이터 원본에 연결하는 데 사용되는 URL을 반환합니다.|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 데이터 원본에 연결하는 데 사용되는 사용자 이름을 반환합니다.|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 데이터 원본에 연결하는 데 사용되는 클라이언트 컴퓨터 이름을 반환합니다.|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, SQL 상태에서 XOPEN 규격 상태로의 변환이 가능한지 여부를 나타내는 **Boolean** 값을 반환합니다.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)|이 개체가 지정된 인터페이스에 대한 래퍼인지 여부를 나타냅니다.|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며 **applicationIntent** 연결 속성의 값을 설정합니다.|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 애플리케이션 이름을 설정합니다.|  
|[setAuthenticationSceme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며 애플리케이션에서 사용하려는 통합 보안의 종류를 나타냅니다.|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 연결할 데이터베이스 이름을 설정합니다.|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 데이터 원본에 대한 설명을 설정합니다.|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 데이터베이스 미러링 구성에 사용되는 장애 조치(Failover) 서버의 이름을 설정합니다.|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 이름을 설정합니다.|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, integratedSecurity 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 설정합니다.|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, lastUpdateCount 속성이 사용되는지 여부를 나타내는 **Boolean** 값을 설정합니다.|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 데이터베이스에서 잠금 시간 초과가 보고되기 전까지 대기하는 시간(밀리초)을 나타내는 **int** 값을 설정합니다.|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 이 DataSource 개체에서 연결을 시도하는 동안 대기하는 시간(초)을 설정합니다.|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 모든 로깅 및 추적 메시지에 사용할 문자 출력 스트림을 설정합니다.|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며 **multiSubnetFailover** 연결 속성의 값을 설정합니다.|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결하는 데 사용할 암호를 설정합니다.|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와의 통신에 사용할 포트 번호를 설정합니다.|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 이 DataSource 개체를 사용하여 만들어진 모든 결과 집합에 사용되는 기본 커서 유형을 설정합니다.|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 문자열 매개 변수를 유니코드 형식으로 서버에 보낼 수 있는지 여부를 나타내는 **Boolean** 값을 설정합니다.|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행하고 있는 컴퓨터의 이름을 설정합니다.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 데이터 원본에 연결하는 데 사용되는 URL을 설정합니다.|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 데이터 원본에 연결하는 데 사용되는 사용자 이름을 설정합니다.|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, 데이터 원본에 연결하는 데 사용되는 클라이언트 컴퓨터 이름을 설정합니다.|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)에서 상속되며, SQL 상태에서 XOPEN 규격 상태로의 변환이 가능한지 여부를 나타내는 **boolean** 값을 설정합니다.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)|[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 관련 메서드에 액세스할 수 있도록 지정된 인터페이스를 구현하는 개체를 반환합니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerDataSource|getApplicationName, getConnection, getDatabaseName, getDescription, getFailoverPartner, getInstanceName, getLastUpdateCount, getLockTimeout, getLoginTimeout, getLogWriter, getPortNumber, getSelectMethod, getSendStringParametersAsUnicode, getServerName, getURL, getUser, getWorkstationID, getXopenStates, setApplicationName, setDatabaseName, setDescription, setFailoverPartner, setInstanceName, setIntegratedSecurity, setLastUpdateCount, setLockTimeout, setLoginTimeout, setLogWriter, setPassword, setPortNumber, setSelectMethod, setSendStringParametersAsUnicode, setServerName, setURL, setUser, setWorkstationID, setXopenStates|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
|javax.sql.ConnectionPoolDataSource|getLoginTimeout, getLogWriter, setLoginTimeout, setLogWriter, getPooledConnection|  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnectionPoolDataSource 클래스](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
