---
description: SQLServerStatement 멤버
title: SQLServerStatement 멤버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 828cbaa9-ea7a-4986-95c3-5ba0d7d01d83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26430e0617bb562cdd300c56f57e882a2aa7fca4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462575"
---
# <a name="sqlserverstatement-members"></a>SQLServerStatement 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스에 의해 노출되는 멤버가 나와 있습니다.  
  
## <a name="constructors"></a>생성자  
 없음  
  
## <a name="fields"></a>필드  
 없음  
  
## <a name="inherited-fields"></a>상속된 필드  
  
|이름|설명|  
|----------|-----------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="methods"></a>메서드  
  
|속성|설명|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 대한 명령의 현재 목록에 지정된 SQL 명령을 추가합니다.|  
|[cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 의해 현재 실행되고 있는 SQL 문을 취소합니다.|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 대한 SQL 명령의 현재 목록을 비웁니다.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 대해 보고된 모든 경고를 지웁니다.|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 데이터베이스와 JDBC 리소스를 자동으로 해제될 때까지 기다리지 않고 즉시 해제합니다.|  
|[execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)|여러 결과를 반환할 수 있는 지정된 SQL 문을 실행합니다.|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md)|실행할 명령 일괄 처리를 데이터베이스로 전송합니다. 모든 명령이 성공적으로 실행되면 업데이트 횟수의 배열을 반환합니다.|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)|지정된 SQL 문을 실행하고 단일 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 반환합니다.|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)|INSERT, UPDATE, MERGE 또는 DELETE 문과 같은 지정된 SQL 문이나 SQL DDL 문 같이 아무 것도 반환하지 않는 SQL 문을 실행합니다.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체를 생성한 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체를 검색합니다.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에서 생성된 결과 집합에 기본값으로 사용되는 데이터베이스 테이블에서의 행 인출 방향을 검색합니다.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에서 생성된 결과 집합 개체의 기본 인출 크기로 사용되는 결과 집합 행 수를 검색합니다.|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체를 실행한 결과로 만들어진 자동 생성 키를 검색합니다.|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 의해 생성된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 문자 및 이진 열 값에 대해 반환될 수 있는 최대 바이트 수를 검색합니다.|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 의해 생성된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 포함될 수 있는 최대 행 수를 검색합니다.|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 다음 결과로 이동합니다.|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서 이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체가 실행될 때까지 대기하는 시간(초)을 검색합니다.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 대한 응답 버퍼링 모드를 검색합니다.|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|현재 결과를 검색하여 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 반환합니다.|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 의해 생성된 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 결과 집합 동시성을 검색합니다.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 의해 생성된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 결과 집합 유지 기능을 검색합니다.|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 의해 생성된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 결과 집합 유형을 검색합니다.|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|현재 결과를 검색하여 업데이트 횟수로 반환합니다.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 대한 호출에서 보고된 첫 번째 경고를 검색합니다.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체가 닫혔는지 여부를 나타냅니다.|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|사용자가 제공한 문 풀에 문을 추가할 수 있는지 여부를 나타내는 값을 반환합니다.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)|이 문 개체가 지정된 인터페이스에 대한 래퍼인지 여부를 나타냅니다.|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|SQL 커서 이름을 이후 실행 메서드에 사용될 지정된 문자열로 설정합니다.|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|이스케이프 처리 모드를 설정합니다.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|결과 집합 행을 처리할 방향에 관한 힌트를 JDBC 드라이버에 제공합니다.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|추가 행이 필요할 경우 데이터베이스에서 인출되는 행 수에 관한 힌트를 JDBC 드라이버에 제공합니다.|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|문자 또는 이진 값을 저장하는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 열의 최대 바이트 수에 대한 제한을 지정된 바이트 수로 설정합니다.|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 포함될 수 있는 최대 행 수에 대한 제한을 지정된 수로 설정합니다.|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|문을 풀링하거나 풀링하지 않도록 요청합니다.|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|드라이버에서 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체가 실행될 때까지 대기하는 시간(초)을 지정된 시간(초)으로 설정합니다.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 응답 버퍼링 모드를 대/소문자를 구분하지 않는 **String full** 또는 **adaptive**로 설정합니다.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)|[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 관련 메서드에 액세스할 수 있도록 지정된 인터페이스를 구현하는 개체를 반환합니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
