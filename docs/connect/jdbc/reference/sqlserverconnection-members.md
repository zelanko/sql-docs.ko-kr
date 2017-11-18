---
title: "SQLServerConnection 멤버 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3115a533-756b-4c78-aee9-4ba7253c85e0
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 917a5561dd3de7f9f45434aef88bd2eb98661473
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverconnection-members"></a>SQLServerConnection 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에서에 의해 노출 되는 멤버가 나와 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스입니다.  
  
## <a name="constructors"></a>생성자  
 없음  
  
## <a name="fields"></a>필드  
  
|이름|Description|  
|----------|-----------------|  
|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|스냅숏 트랜잭션 격리 수준을 지정하는 데 사용됩니다.|  
  
## <a name="inherited-fields"></a>상속된 필드  
  
|상속하는 원본 클래스|Description|  
|---------------------------|-----------------|  
|java.sql.Connection|TRANSACTION_NONE, TRANSACTION_READ_COMMITTED, TRANSACTION_READ_UNCOMMITTED, TRANSACTION_REPEATABLE_READ, TRANSACTION_SERIALIZABLE|  
  
## <a name="methods"></a>메서드  
  
|이름|Description|  
|----------|-----------------|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverconnection.md)|이 대해 보고 된 모든 경고를 지웁니다 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.|  
|[닫기](../../../connect/jdbc/reference/close-method-sqlserverconnection.md)|이 데이터베이스를 해제 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체와 JDBC 리소스를 자동으로 해제 되기를 기다리지 않고 즉시 해제 합니다.|  
|[커밋](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md)|이전의 커밋 또는 롤백 후 내용을 영구적으로 적용 된 모든 변경 내용을 적용 하 고 보유 하 고 있는 현재이 데이터베이스 잠금을 해제 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.|  
|[createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md)|만듭니다는 **java.sql.Blob** 데이터가 없는 개체입니다.|  
|[createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md)|만듭니다는 **java.sql.Clob** 데이터가 없는 개체입니다.|  
|[createNClob](../../../connect/jdbc/reference/createnclob-method-sqlserverconnection.md)|만듭니다는 **java.sql.NClob** 데이터가 없는 개체입니다.|  
|[createStatement](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)|만듭니다는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 데이터베이스로 SQL 문을 보내기 위한 개체입니다.|  
|[createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md)|만듭니다는 **java.sql.SQLXML** 데이터가 없는 개체입니다.|  
|[getAutoCommit](../../../connect/jdbc/reference/getautocommit-method-sqlserverconnection.md)|이 대 한 현재 자동 커밋 모드를 검색 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.|  
|[getCatalog](../../../connect/jdbc/reference/getcatalog-method-sqlserverconnection.md)|이 대 한 현재 카탈로그 이름을 검색 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.|  
|[getClientConnectionID 메서드 &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|연결 시도가 성공 또는 실패했는지 여부에 관계 없이 최근 연결 시도의 연결 ID를 가져옵니다.|  
|[getClientInfo](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)|JDBC 드라이버에서 지원되는 클라이언트 정보 속성에 대한 정보를 검색합니다.|  
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverconnection.md)|현재 유지 기능을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 이 사용 하 여 만든 개체 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md)|검색 한 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 이 데이터베이스에 대 한 메타 데이터가 포함 된 개체 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체 연결을 나타냅니다.|  
|[getTransactionIsolation](../../../connect/jdbc/reference/gettransactionisolation-method-sqlserverconnection.md)|이 대 한 현재 트랜잭션 격리 수준을 검색 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.|  
|[getTypeMap](../../../connect/jdbc/reference/gettypemap-method-sqlserverconnection.md)|연결 된 지도 개체를 검색 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md)|이 호출에서 보고 된 첫 번째 경고 검색 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverconnection.md)|나타냅니다 여부이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 잠겨 있습니다.|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverconnection.md)|나타냅니다 여부이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 읽기 전용 모드 인지 합니다.|  
|[isValid](../../../connect/jdbc/reference/isvalid-method-sqlserverconnection.md)|나타냅니다 여부이 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체가 닫히지 않은 하 고 여전히 유효 합니다.|  
|[nativeSQL](../../../connect/jdbc/reference/nativesql-method-sqlserverconnection.md)|지정된 SQL 문을 데이터베이스 서버의 네이티브 SQL 문법으로 변환합니다.|  
|[prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)|만듭니다는 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 데이터베이스 저장 프로시저를 호출 하기 위한 개체입니다.|  
|[prepareStatement](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)|만듭니다는 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 보내는 개체를 데이터베이스에 대 한 SQL 문을 매개 변수화 합니다.|  
|[releaseSavepoint](../../../connect/jdbc/reference/releasesavepoint-method-sqlserverconnection.md)|지정 된 제거 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 를 현재 트랜잭션에서 개체입니다.|  
|[롤백](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)|현재 트랜잭션에서 변경한 모든 내용을 취소 하 고이 현재 보유 하 고 있는 데이터베이스 잠금을 해제 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.|  
|[setAutoCommit](../../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)|이 대 한 자동 커밋 모드를 설정 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체 지정 된 상태입니다.|  
|[setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md)|이러한 하위 네임 스페이스를 선택 하는 데 지정 된 카탈로그 이름을 설정 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 작업 하려는 개체의 데이터베이스입니다.|  
|[setClientInfo](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)|클라이언트 정보 속성의 값을 설정합니다.|  
|[setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md)|유지 기능을 변경 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 이 사용 하 여 만든 개체 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 를 개체입니다.|  
|[setReadOnly](../../../connect/jdbc/reference/setreadonly-method-sqlserverconnection.md)|이 배치 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체의 읽기 전용 모드는 힌트를 JDBC 드라이버에서 데이터베이스 최적화를 사용할 수 있습니다.|  
|[setSavepoint](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)|현재 트랜잭션에 명명 되지 않은 저장 점을 만들고 새 반환 [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) 점을 나타내는 개체입니다.|  
|[setTransactionIsolation](../../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md)|이 대 한 트랜잭션 격리 수준을 변경 하려고 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 지정한 개체입니다.|  
|[setTypeMap](../../../connect/jdbc/reference/settypemap-method-sqlserverconnection.md)|주어진된 TypeMap 개체를이 대 한 형식 맵으로 설치 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체입니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.lang.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

