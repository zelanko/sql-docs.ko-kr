---
title: SQLServerConnection 멤버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3115a533-756b-4c78-aee9-4ba7253c85e0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a3e3ba3d7da52f10b9bd51934b25f44a38a16be0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971725"
---
# <a name="sqlserverconnection-members"></a>SQLServerConnection 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에는 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스에 의해 노출되는 멤버가 나와 있습니다.  
  
## <a name="constructors"></a>생성자  
 없음  
  
## <a name="fields"></a>필드  
  
|속성|설명|  
|----------|-----------------|  
|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|스냅샷 트랜잭션 격리 수준을 지정하는 데 사용됩니다.|  
  
## <a name="inherited-fields"></a>상속된 필드  
  
|상속하는 원본 클래스|설명|  
|---------------------------|-----------------|  
|java.sql.Connection|TRANSACTION_NONE, TRANSACTION_READ_COMMITTED, TRANSACTION_READ_UNCOMMITTED, TRANSACTION_REPEATABLE_READ, TRANSACTION_SERIALIZABLE|  
  
## <a name="methods"></a>메서드  
  
|속성|설명|  
|----------|-----------------|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에 대해 보고된 모든 경고를 지웁니다.|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체의 데이터베이스와 JDBC 리소스를 자동으로 해제될 때까지 기다리지 않고 즉시 해제합니다.|  
|[closeUnreferencedPreparedStatementHandles](../../../connect/jdbc/reference/closeunreferencedpreparedstatementhandles-method-sqlserverconnection.md)|보류 중인 삭제 된 준비 문이 실행 될 때까지 준비 취소 요청을 강제로 실행 합니다.| 
|[commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md)|이전의 커밋 또는 롤백 후에 변경된 모든 내용을 영구적으로 만들고, 이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에서 현재 보유 중인 데이터베이스 잠금을 해제합니다.|  
|[createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md)|데이터를 사용 하지 않고 **java .sql** 개체를 만듭니다.|  
|[createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md)|데이터 없이 **java .sql** 개체를 만듭니다.|  
|[createNClob](../../../connect/jdbc/reference/createnclob-method-sqlserverconnection.md)|데이터 없이 **java. NClob** 개체를 만듭니다.|  
|[createStatement](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)|데이터베이스로 SQL 문을 보내기 위한 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체를 만듭니다.|  
|[createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md)|데이터 없이 **java .SQL SQLXML** 개체를 만듭니다.|  
|[getAutoCommit](../../../connect/jdbc/reference/getautocommit-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에 대한 현재 자동 커밋 모드를 검색합니다.|  
|[getCatalog](../../../connect/jdbc/reference/getcatalog-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에 대한 현재 카탈로그 이름을 검색합니다.|  
|[getClientConnectionID 메서드 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|연결 시도가 성공 또는 실패했는지 여부에 관계 없이 최근 연결 시도의 연결 ID를 가져옵니다.|  
|[getClientInfo](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)|JDBC 드라이버에서 지원되는 클라이언트 정보 속성에 대한 정보를 검색합니다.|  
|[getDisableStatementPooling](../../../connect/jdbc/reference/getdisablestatementpooling-method-sqlserverconnection.md)|**Statementpoolingcachesize** connection 속성의 값을 반환 합니다. 이 설정은이 연결에 대해 문 풀링이 사용 되는지 여부를 제어 합니다.|
|[getDiscardedServerPreparedStatementCount](../../../connect/jdbc/reference/getdiscardedserverpreparedstatementcount-method-sqlserverconnection.md)|현재 해결 되지 않은 준비 된 문 unprepare 작업 수를 반환 합니다.|
|[getEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/getenableprepareonfirstpreparedstatementcall-method-sqlserverconnection.md)|**EnablePrepareOnFirstPreparedStatementCall** connection 속성의 값을 반환 합니다.|
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체를 사용하여 만든 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 유지 기능을 검색합니다.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 나타내는 연결의 대상 데이터베이스에 대한 메타데이터가 들어 있는 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 개체를 검색합니다.|  
|[getServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/getserverpreparedstatementdiscardthreshold-method-sqlserverconnection.md)|**ServerPreparedStatementDiscardThreshold** connection 속성의 값을 반환 합니다.|  
|[getStatementHandleCacheEntryCount](../../../connect/jdbc/reference/getstatementhandlecacheentrycount-method-sqlserverconnection.md)|풀링된 준비 된 문 핸들의 현재 수를 반환 합니다.|  
|[getStatementPoolingCacheSize](../../../connect/jdbc/reference/getstatementpoolingcachesize-method-sqlserverconnection.md)|이 연결에 대해 준비 된 문 캐시의 크기를 반환 합니다.|  
|[getTransactionIsolation](../../../connect/jdbc/reference/gettransactionisolation-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에 대한 현재 트랜잭션 격리 수준을 검색합니다.|  
|[getTypeMap](../../../connect/jdbc/reference/gettypemap-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체와 연결된 Map 개체를 검색합니다.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에 대한 호출에서 보고된 첫 번째 경고를 검색합니다.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 닫혔는지 여부를 나타냅니다.|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 읽기 전용 모드인지 여부를 나타냅니다.|  
|[isStatementPoolingEnabled](../../../connect/jdbc/reference/isstatementpoolingenabled-method-sqlserverconnection.md)|이 연결에 대해 문 풀링이 사용 되는지 여부를 반환 합니다.|  
|[isValid](../../../connect/jdbc/reference/isvalid-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 닫히지 않고 아직 유효한지 여부를 나타냅니다.|  
|[nativeSQL](../../../connect/jdbc/reference/nativesql-method-sqlserverconnection.md)|지정된 SQL 문을 데이터베이스 서버의 네이티브 SQL 문법으로 변환합니다.|  
|[prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)|데이터베이스 저장 프로시저를 호출하기 위한 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 개체를 만듭니다.|  
|[prepareStatement](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)|데이터베이스로 매개 변수가 있는 SQL 문을 보내기 위한 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 개체를 만듭니다.|  
|[releaseSavepoint](../../../connect/jdbc/reference/releasesavepoint-method-sqlserverconnection.md)|지정된 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 개체를 현재 트랜잭션에서 제거합니다.|  
|[rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)|현재 트랜잭션에서 변경한 모든 내용을 취소하고 이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 현재 보유하고 있는 데이터베이스 잠금을 해제합니다.|  
|[setAutoCommit](../../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에 대한 자동 커밋 모드를 지정된 상태로 설정합니다.|  
|[setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md)|지정된 카탈로그 이름을 설정하여 이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체의 데이터베이스 중 작업할 하위 공간을 선택합니다.|  
|[setClientInfo](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)|클라이언트 정보 속성의 값을 설정합니다.|  
|[setDisableStatementPooling](../../../connect/jdbc/reference/setdisablestatementpooling-method-sqlserverconnection.md)|문 풀링을 true 또는 false로 설정 합니다.|  
|[setEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/setenableprepareonfirstpreparedstatementcall-method-sqlserverconnection.md)|**EnablePrepareOnFirstPreparedStatementCall** connection 속성의 새 값을 지정 합니다.|  
|[setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md)|이 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 개체를 사용하여 만든 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 유지 기능을 변경합니다.|  
|[setReadOnly](../../../connect/jdbc/reference/setreadonly-method-sqlserverconnection.md)|JDBC 드라이버에서 데이터베이스 최적화를 수행하기 위한 힌트로 사용할 수 있도록 이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체를 읽기 전용 모드로 설정합니다.|  
|[setSavepoint](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)|현재 트랜잭션에 명명되지 않은 저장점을 만들고 이 저장점을 나타내는 새 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 개체를 반환합니다.|  
|[setServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/setserverpreparedstatementdiscardthreshold-method-sqlserverconnection.md)|**ServerPreparedStatementDiscardThreshold** connection 속성의 새 값을 설정 합니다.|  
|[setStatementPoolingCacheSize](../../../connect/jdbc/reference/setstatementpoolingcachesize-method-sqlserverconnection.md)|이 연결에 대해 준비 된 문 캐시의 크기를 설정 합니다.|  
|[setTransactionIsolation](../../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md)|이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에 대한 트랜잭션 격리 수준을 지정된 수준으로 변경합니다.|  
|[setTypeMap](../../../connect/jdbc/reference/settypemap-method-sqlserverconnection.md)|지정된 TypeMap 개체를 이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체에 대한 형식 맵으로 설치합니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.lang.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
