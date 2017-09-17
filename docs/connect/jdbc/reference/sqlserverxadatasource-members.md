---
title: "SQLServerXADataSource 멤버 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 04178645-915f-4569-8907-d45e299bbe7d
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2b81229c9c1f4164635e25342456d16b2c578168
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverxadatasource-members"></a>SQLServerXADataSource 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에서에 의해 노출 되는 멤버가 나와 [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) 클래스입니다.  
  
## <a name="constructors"></a>생성자  
  
|이름|Description|  
|----------|-----------------|  
|[(SQLServerXADataSource)](../../../connect/jdbc/reference/sqlserverxadatasource-constructor.md)|새 인스턴스를 초기화는 [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) 클래스입니다.|  
  
## <a name="fields"></a>필드  
 없음  
  
## <a name="inherited-fields"></a>상속된 필드  
 없음  
  
## <a name="methods"></a>메서드  
  
|이름|Description|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md))의 값을 반환 된 **applicationIntent** 연결 속성입니다.|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 응용 프로그램 이름을 반환 합니다.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md))이 데이터 원본 개체가 나타내는 데이터 원본과 연결을 설정 하려고 시도 합니다.|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 데이터베이스 이름을 반환 합니다.|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 데이터베이스 미러링 구성에에서 사용 되는 장애 조치 서버의 이름을 반환 합니다.|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 반환은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 인스턴스 이름입니다.|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 반환은 **부울** lastUpdateCount 속성이 사용 되는지 여부를 나타내는 값입니다.|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 반환은 **int** 는 데이터베이스에서 잠금 시간 초과가 보고 되기 전까지 대기 하는 시간 (밀리초)의 수를 나타내는 값입니다.|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 연결을 시도 하는 동안이 데이터 원본 개체에서 대기 하는 시간 (초)의 수를 반환 합니다.|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 모든 로깅 및 추적 메시지에 사용할 문자 출력 스트림을 반환 합니다.|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md))의 값을 검색 하는 **multiSubnetFailover** 연결 속성입니다.|  
|[getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)|(에서 상속 되며, [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)) 풀링된 연결으로 사용할 수 있는 실제 데이터베이스 연결을 설정 하려고 시도 합니다.|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md))와 통신 하는 데 사용 되는 현재 포트 번호를 반환 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverxadatasource.md)|이에 대 한 참조를 반환 [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md) 개체입니다.|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md))이 데이터 원본 개체를 사용 하 여 만들어진 모든 결과 집합에 사용 되는 기본 커서 유형을 반환 합니다.|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 반환은 **부울** 나타내는 값을 보내는 경우 **문자열** 서버에 유니코드 형식으로 매개 변수를 사용할 수 있습니다.|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md))를 실행 하는 컴퓨터의 이름을 반환 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 데이터 원본에 연결 하는 데 사용 되는 URL을 반환 합니다.|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 데이터 원본에 연결 하는 데 사용 되는 사용자 이름을 반환 합니다.|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 클라이언트의 이름을 데이터 원본에 연결 하는 데 사용 되는 컴퓨터 이름을 반환 합니다.|  
|[getXAConnection](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)|분산 트랜잭션에 사용할 수 있는 실제 데이터베이스 연결을 설정합니다.|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 반환은 **부울** SQL 상태를 XOPEN 규격 상태로 변환할을 사용할 수 있는지를 나타내는 값입니다.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)|이 개체가 지정된 인터페이스에 대한 래퍼인지 여부를 나타냅니다.|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md))의 값을 설정 하는 **applicationIntent** 연결 속성입니다.|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 응용 프로그램 이름을 설정 합니다.|  
|[setAuthenticationSceme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 응용 프로그램에서 사용 하려는 통합된 보안의 종류를 나타냅니다.|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md))에 연결할 데이터베이스 이름을 설정 합니다.|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 데이터 원본에 대 한 설명을 설정 합니다.|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 데이터베이스 미러링 구성에에서 사용 되는 장애 조치 서버의 이름을 설정 합니다.|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 집합의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 인스턴스 이름입니다.|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 집합을 **부울** integratedSecurity 속성이 사용 되는지 여부를 나타내는 값입니다.|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 집합을 **부울** lastUpdateCount 속성이 사용 되는지 여부를 나타내는 값입니다.|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 집합은 **int** 데이터베이스에서 잠금 시간 초과가 보고 되기 전까지 대기 시간 (밀리초)의 수를 나타내는 값입니다.|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 연결을 시도 하는 동안이 데이터 원본 개체에서 대기 하는 시간 (초)의 수를 설정 합니다.|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 모든 로깅 및 추적 메시지에 사용할 문자 출력 스트림을 설정 합니다.|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md))의 값을 설정 하는 **multiSubnetFailover** 연결 속성입니다.|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md))에 연결 하는 데 사용할 수는 암호를 설정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md))와 통신 하는 데 사용할 포트 번호를 설정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md))이 데이터 원본 개체를 사용 하 여 만들어진 모든 결과 집합에 사용 되는 기본 커서 유형을 설정 합니다.|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 집합은 **부울** 나타내는 값을 보내는 경우 **문자열** 서버에 유니코드 형식으로 매개 변수를 사용할 수 있습니다.|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md))를 실행 하는 컴퓨터의 이름을 설정 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]합니다.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 데이터 원본에 연결 하는 데 사용 되는 URL을 설정 합니다.|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 데이터 원본에 연결 하는 데 사용 되는 사용자 이름을 설정 합니다.|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 클라이언트 데이터 원본에 연결 하는 데 사용 되는 컴퓨터 이름을 설정 합니다.|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|(에서 상속 되며, [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) 집합을 **부울** SQL 상태를 XOPEN 규격 상태로 변환할을 사용할 수 있는지를 나타내는 값입니다.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)|에 대 한 액세스를 허용 하도록 지정된 된 인터페이스를 구현 하는 개체를 반환 합니다.는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-특정 메서드.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerConnectionPoolDataSource|getPooledConnection|  
|com.microsoft.sqlserver.jdbc.SQLServerDataSource|getApplicationName, getConnection, getDatabaseName, getDescription, getFailoverPartner, getInstanceName, getLastUpdateCount, getLockTimeout, getLoginTimeout, getLogWriter, getPortNumber, getSelectMethod, getSendStringParametersAsUnicode, getServerName, getURL, getUser, getWorkstationID, getXopenStates, setApplicationName, setDatabaseName, setDescription, setFailoverPartner, setInstanceName, setIntegratedSecurity, setLastUpdateCount, setLockTimeout, setLoginTimeout, setLogWriter, setPassword, setPortNumber, setSelectMethod, setSendStringParametersAsUnicode, setServerName, setURL, setUser, setWorkstationID, setXopenStates|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
|javax.sql.XADataSource|getLoginTimeout, getLogWriter, setLoginTimeout, setLogWriter|  
|javax.sql.ConnectionPoolDataSource|getLoginTimeout, getLogWriter, setLoginTimeout, setLogWriter|  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerXADataSource 클래스](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
