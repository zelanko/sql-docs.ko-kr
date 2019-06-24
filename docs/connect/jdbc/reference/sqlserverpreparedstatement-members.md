---
title: SQLServerPreparedStatement 멤버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2363902f-d4c6-4cd4-a5fc-86079eb9e418
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 89b4d7bedb2572c0396c3de80f000fdccdd1a2cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803012"
---
# <a name="sqlserverpreparedstatement-members"></a>SQLServerPreparedStatement 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에서는 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스에 의해 노출되는 멤버를 나열합니다.  
  
## <a name="constructors"></a>생성자  
 없음  
  
## <a name="fields"></a>필드  
 없음  
  
## <a name="inherited-fields"></a>상속된 필드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="methods"></a>메서드  
  
|속성|설명|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)|이 Statement 개체의 명령 일괄 처리에 대한 매개 변수 집합을 추가합니다.|  
|[cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 Statement 개체에 의해 현재 실행되고 있는 SQL 문을 취소합니다.|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)|이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 대한 SQL 명령의 현재 목록을 비웁니다.|  
|[clearParameters](../../../connect/jdbc/reference/clearparameters-method-sqlserverpreparedstatement.md)|현재 매개 변수 값을 즉시 지웁니다.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 Statement 개체에 대해 보고된 모든 경고를 지웁니다.|  
|[close](../../../connect/jdbc/reference/close-method-sqlserverpreparedstatement.md)|이 Statement 개체의 데이터베이스와 JDBC 리소스가 자동으로 해제될 때까지 기다리지 않고 즉시 해제합니다.|  
|[execute](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)|이 Statement 개체에서 모든 종류의 SQL 문을 실행합니다.|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverpreparedstatement.md)|실행할 명령 일괄 처리를 데이터베이스로 전송합니다. 모든 명령이 성공적으로 실행되면 업데이트 횟수의 배열을 반환합니다.|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)|이 Statement 개체에서 SQL 쿼리를 실행하고 쿼리에 의해 생성된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 반환합니다.|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)|이 Statement 개체에서 SQL INSERT, UPDATE, MERGE 또는 DELETE 문과 같은 SQL 문이나 DDL 문 같이 아무 것도 반환하지 않는 SQL 문을 실행합니다.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 Statement 개체를 생성한 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 개체를 검색합니다.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 Statement 개체에서 생성된 결과 집합에 기본값으로 사용되는 데이터베이스 테이블에서의 행 인출 방향을 검색합니다.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 Statement 개체에서 생성된 결과 집합 개체의 기본 인출 크기로 사용되는 결과 집합 행 수를 검색합니다.|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 Statement 개체를 실행한 결과로 만들어진 자동 생성 키를 검색합니다.|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 Statement 개체에 의해 생성된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 문자 및 이진 열 값에 대해 반환될 수 있는 최대 바이트 수를 검색합니다.|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 Statement 개체에 의해 생성된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 포함될 수 있는 최대 행 수를 검색합니다.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverpreparedstatement.md)|이 Statement 개체가 실행될 때 반환되는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 열에 대한 정보가 들어 있는 [SQLServerResultSetMetaData 클래스](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) 개체를 검색합니다.|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 문 개체의 다음 결과로 이동 합니다.|  
|[getParameterMetaData](../../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md)|이 Statement 개체에 대한 매개 변수의 수, 형식 및 속성을 검색합니다.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 대한 응답 버퍼링 모드를 검색합니다.|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서 이 Statement 개체가 실행될 때까지 대기하는 시간(초)을 검색합니다.|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 현재 결과를 검색하여 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 반환합니다.|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 Statement 개체에 의해 생성된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 결과 집합 동시성을 검색합니다.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 Statement 개체에 의해 생성된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 결과 집합 동시성을 검색합니다.|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 Statement 개체에 의해 생성된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 결과 집합 형식을 검색합니다.|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 현재 결과를 검색하여 업데이트 횟수로 반환합니다.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 Statement 개체에 대한 호출에서 보고된 첫 번째 경고를 검색합니다.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 Statement 개체가 닫혔는지 여부를 나타냅니다.|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 사용자가 제공한 문 풀에 문을 추가할 수 있는지 여부를 나타내는 값을 반환합니다.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)|이 문 개체가 지정된 인터페이스에 대한 래퍼인지 여부를 나타냅니다.|  
|[setArray](../../../connect/jdbc/reference/setarray-method-sqlserverpreparedstatement.md)|지정된 매개 변수 번호를 지정된 Array 개체로 설정합니다.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)|지정된 매개 변수 번호를 지정된 InputStream 개체로 설정합니다.|  
|[setBigDecimal](../../../connect/jdbc/reference/setbigdecimal-method-sqlserverpreparedstatement.md)|지정된 매개 변수 번호를 지정된 BigDecimal 개체로 설정합니다.|  
|[setBinaryStream](../../../connect/jdbc/reference/setbinarystream-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 입력 스트림으로 설정합니다.|  
|[setBlob](../../../connect/jdbc/reference/setblob-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 Blob 개체로 설정합니다.|  
|[setboolean](../../../connect/jdbc/reference/setboolean-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 **Boolean** 값으로 설정합니다.|  
|[setByte](../../../connect/jdbc/reference/setbyte-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 **byte** 값으로 설정합니다.|  
|[setBytes](../../../connect/jdbc/reference/setbytes-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 바이트 배열로 설정합니다.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 Reader 개체로 설정합니다.|  
|[setClob](../../../connect/jdbc/reference/setclob-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 Clob 개체로 설정합니다.|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, SQL 커서 이름을 이후 실행 메서드에 사용될 지정된 문자열로 설정합니다.|  
|[setDate](../../../connect/jdbc/reference/setdate-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 날짜 값으로 설정합니다.|  
|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md)|에 지정 된 열의 값을 설정 합니다 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 값입니다.|  
|[setDouble](../../../connect/jdbc/reference/setdouble-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 **double** 값으로 설정합니다.|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이스케이프 처리 모드를 설정합니다.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 결과 집합 행을 처리할 방향에 관한 힌트를 JDBC 드라이버에 제공합니다.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 추가 행이 필요할 경우 데이터베이스에서 인출되는 행 수에 관한 힌트를 JDBC 드라이버에 제공합니다.|  
|[setFloat](../../../connect/jdbc/reference/setfloat-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 **float** 값으로 설정합니다.|  
|[setInt](../../../connect/jdbc/reference/setint-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 **int** 값으로 설정합니다.|  
|[setLong](../../../connect/jdbc/reference/setlong-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 **long** 값으로 설정합니다.|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 문자 또는 이진 값을 저장하는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 열의 최대 바이트 수에 대한 제한을 지정된 바이트 수로 설정합니다.|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 포함될 수 있는 최대 행 수에 대한 제한을 지정된 수로 설정합니다.|  
|[setNCharacterStream](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 Reader 개체로 설정합니다.|  
|[setNClob](../../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 개체로 설정합니다.|  
|[setNull](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)|설정할 매개 변수 형식이 지정된 경우 지정된 매개 변수를 null 값으로 설정합니다.|  
|[setNString](../../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md)|지정된 매개 변수를 지정된 **String** 개체로 설정합니다.|  
|[setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)|지정된 개체를 사용하여 지정된 매개 변수의 값을 설정합니다.|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 문을 풀링하거나 풀링하지 않도록 요청합니다. 기본적으로 SQLServerPreparedStatement 개체는 풀링 가능한 상태로 만들어집니다.|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 드라이버에서 Statement 개체가 실행될 때까지 대기하는 시간(초)을 지정된 시간(초)으로 설정합니다.|  
|[setRef](../../../connect/jdbc/reference/setref-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 Ref 개체로 설정합니다.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)에서 상속되며, 이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 응답 버퍼링 모드를 대/소문자를 구분하지 않는 **String full** 또는 **adaptive**로 설정합니다.|  
|[setShort](../../../connect/jdbc/reference/setshort-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 **short** 값으로 설정합니다.|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 **String** 값으로 설정합니다.|  
|[setSQLXML](../../../connect/jdbc/reference/setsqlxml-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 **SQLXML** 개체로 설정합니다.|  
|[setTime](../../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 시간 값으로 설정합니다.|  
|[setTimestamp](../../../connect/jdbc/reference/settimestamp-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 타임스탬프 값으로 설정합니다.|  
|[setUnicodeStream](../../../connect/jdbc/reference/setunicodestream-method-sqlserverpreparedstatement.md)|지정된 매개 변수 번호를 지정된 바이트 수를 포함하는 지정된 입력 스트림으로 설정합니다.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverpreparedstatement.md)|지정된 매개 변수를 지정된 URL 값으로 설정합니다.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)|[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 관련 메서드에 액세스할 수 있도록 지정된 인터페이스를 구현하는 개체를 반환합니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerStatement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, isPoolable, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setPoolable, setQueryTimeout|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Statement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setQueryTimeout|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
