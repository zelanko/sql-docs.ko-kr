---
title: "SQLServerCallableStatement 멤버 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apitype: Assembly
ms.assetid: 5ebdc186-e50f-4d14-bbf4-95af5051e4a4
caps.latest.revision: "50"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a930408957d61c61738c271914dca734920908f4
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="sqlservercallablestatement-members"></a>SQLServerCallableStatement 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에서에 의해 노출 되는 멤버가 나와 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스입니다.  
  
## <a name="constructors"></a>생성자  
 없음  
  
## <a name="fields"></a>필드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="inherited-fields"></a>상속된 필드  
 없음  
  
## <a name="methods"></a>메서드  
  
|이름|Description|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 이 CallableStatement 개체의 명령 일괄 처리에 매개 변수 집합을 추가합니다.|  
|[취소](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 이 CallableStatement 개체에 의해 현재 실행 되 고 있는 SQL 문을 취소 합니다.|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 이 CallableStatement 개체에 대 한 SQL 명령의 현재 목록을 비웁니다.|  
|[clearParameters](../../../connect/jdbc/reference/clearparameters-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 현재 매개 변수 값을 즉시 지웁니다.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 이 CallableStatement 개체에 보고 되는 모든 경고를 지웁니다.|  
|[닫기](../../../connect/jdbc/reference/close-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 데이터베이스와 JDBC 리소스를이 CallableStatement 개체에 자동으로 해제 될 때까지 기다리지 않고 즉시 해제 합니다.|  
|[실행](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 모든 종류의 SQL 문 될 수 있는이 CallableStatement 개체에서 SQL 문을 실행 합니다.|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 실행할 명령 일괄 처리를 데이터베이스로 전송합니다. 모든 명령이 성공적으로 실행되면 업데이트 횟수의 배열을 반환합니다.|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 이 CallableStatement 개체에서 SQL 쿼리를 실행 하 고 반환 된 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 쿼리에 의해 생성 되는 개체입니다.|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) SQL INSERT, UPDATE, MERGE 또는 DELETE 문; 있어야이 CallableStatement 개체에서 SQL 문을 실행합니다 또는 DDL 문 같이 아무 것도 반환 하는 SQL 문을 지정 합니다.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 검색 된 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 이 CallableStatement 개체를 생성 하는 개체입니다.|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)|지정 된 열의 값을 검색 하는 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체입니다.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 검색이 CallableStatement 개체에서 생성 된 결과 집합에 대 한 기본 데이터베이스 테이블에서 행 인출 방향을 검색 됩니다.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 결과 대 한 기본 인출 크기로 사용 되는 결과 집합 행 수 집합이 CallableStatement 개체에서 생성 된 개체를 검색 합니다.|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 이 CallableStatement 개체를 실행 한 결과로 만들어진 자동 생성 키를 검색 합니다.|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 바이트의 문자 및 이진 열 값에 대 한 반환 될 수 있는 최대 수를 검색 한 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 이 CallableStatement 개체에 의해 생성 된 개체입니다.|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 행의 최대 수를 검색 하는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 이 CallableStatement 개체에 의해 생성 된 개체에 포함 될 수 있습니다.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 검색 한 [SQLServerResultSetMetaData 클래스](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) 개체의 열에 대 한 정보를 포함 하는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 이 CallableStatement 개체가 실행 될 때 반환 되는 개체입니다.|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 이 CallableStatement 개체의 다음 결과로 이동 합니다.|  
|[getParameterMetaData](../../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 수, 형식 및이 CallableStatement 개체에 대 한 매개 변수의 속성을 검색합니다.|  
|[getArray](../../../connect/jdbc/reference/getarray-method-sqlservercallablestatement.md)|Array 개체와 지정된 된 매개 변수의 값을 검색합니다.|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservercallablestatement.md)|스트림으로 지정된 된 매개 변수의 값을 검색 **ASCII** 문자입니다.|  
|[getBigDecimal](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)|지정된 매개 변수의 값을 검색하여 java.math.BigDecimal로 반환합니다.|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlservercallablestatement.md)|지정된 매개 변수의 값을 검색하여 중단되지 않는 바이트의 이진 스트림으로 반환합니다.|  
|[getBlob](../../../connect/jdbc/reference/getblob-method-sqlservercallablestatement.md)|Java 프로그래밍 언어에 있는 Blob 개체와 지정된 된 JDBC Blob 매개 변수의 값을 검색합니다.|  
|[getboolean](../../../connect/jdbc/reference/getboolean-method-sqlservercallablestatement.md)|로 지정된 된 매개 변수의 값을 검색 하는 **부울** 값입니다.|  
|[getByte](../../../connect/jdbc/reference/getbyte-method-sqlservercallablestatement.md)|로 지정된 된 매개 변수의 값을 검색 하는 **바이트** 값입니다.|  
|[getBytes](../../../connect/jdbc/reference/getbytes-method-sqlservercallablestatement.md)|지정된 매개 변수의 값을 검색하여 바이트 배열로 반환합니다.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservercallablestatement.md)|지정된 매개 변수의 값을 검색하여 java.io.Reader 개체로 반환합니다.|  
|[getClob](../../../connect/jdbc/reference/getclob-method-sqlservercallablestatement.md)|Java 프로그래밍 언어에 Clob 개체와 지정된 된 JDBC Blob 매개 변수의 값을 검색합니다.|  
|[getDate](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)|지정된 매개 변수의 값을 검색하여 Java 프로그래밍 언어의 java.sql.Date 개체로 반환합니다.|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)|지정 된 열의 값을 검색 하는[DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체입니다.|  
|[getDouble](../../../connect/jdbc/reference/getdouble-method-sqlservercallablestatement.md)|로 지정된 된 매개 변수의 값을 검색 하는 **double** Java 프로그래밍 언어의에서 합니다.|  
|[getFloat](../../../connect/jdbc/reference/getfloat-method-sqlservercallablestatement.md)|로 지정된 된 매개 변수의 값을 검색 하는 **float** Java 프로그래밍 언어의에서 합니다.|  
|[getInt](../../../connect/jdbc/reference/getint-method-sqlservercallablestatement.md)|로 지정된 된 매개 변수의 값을 검색 하는 **int** Java 프로그래밍 언어의에서 합니다.|  
|[getLong](../../../connect/jdbc/reference/getlong-method-sqlservercallablestatement.md)|로 지정된 된 매개 변수의 값을 검색 하는 **긴** Java 프로그래밍 언어의에서 합니다.|  
|[getNCharacterStream](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)|판독기 개체와 지정된 된 매개 변수의 값을 검색합니다.|  
|[getNClob](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)|지정 된 JDBC의 값을 검색 **NCLOB** 로 매개 변수는 **NClob** Java 프로그래밍 언어의에서 개체입니다.|  
|[getNString](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)|지정된 된 값을 검색 **NCHAR**, **NVARCHAR** 또는 **LONGNVARCHAR** java에서 프로그래밍 언어 문자열 매개 변수입니다.|  
|[getObject](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)|지정된 매개 변수의 값을 검색하여 Java 프로그래밍 언어의 개체로 반환합니다.|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 시간 (초)의 수를 검색 된 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 에서이 CallableStatement 개체가 실행 될 때까지 대기 합니다.|  
|[getRef](../../../connect/jdbc/reference/getref-method-sqlservercallablestatement.md)|Java 프로그래밍 언어의 Ref 개체로 지정된 된 매개 변수의 값을 검색합니다.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 응답 버퍼링 모드를이 대 한 검색 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체입니다.|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 현재 결과 검색 한 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 결과 집합 동시성을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 이 CallableStatement 개체에 의해 생성 된 개체입니다.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 결과 집합 유지 기능에 대 한 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 이 CallableStatement 개체에 의해 생성 된 개체입니다.|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 검색 결과 집합에 대 한 유형이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 이 CallableStatement 개체에 의해 생성 된 개체입니다.|  
|[getShort](../../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md)|로 지정된 된 매개 변수의 값을 검색 하는 **짧은** Java 프로그래밍 언어의에서 합니다.|  
|[getString](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)|로 지정된 된 매개 변수의 값을 검색 하는 **문자열** Java 프로그래밍 언어의에서 합니다.|  
|[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md)|지정된 매개 변수의 값을 검색하여 java.sql.SQLXML 개체로 반환합니다.|  
|[getTime](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)|지정된 매개 변수의 값을 검색하여 Java 프로그래밍 언어의 java.sql.Time 개체로 반환합니다.|  
|[getTimestamp](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)|지정된 매개 변수의 값을 검색하여 Java 프로그래밍 언어의 java.sql.Timestamp 개체로 반환합니다.|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 현재 결과를 검색하여 업데이트 횟수로 반환합니다.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)|Java 프로그래밍 언어의 URL 개체로 지정된 된 매개 변수의 값을 검색합니다.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 이 CallableStatement 개체에 대 한 호출에서 보고 하는 첫 번째 경고를 검색 합니다.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 이 문 개체가 닫혔는지 여부를 나타냅니다.|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 사용자가 제공한 문 풀에 문을 추가할 수 있는지 여부를 나타내는 값을 반환합니다.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)|이 문 개체가 지정된 인터페이스에 대한 래퍼인지 여부를 나타냅니다.|  
|[registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)|OUT 매개 변수를 등록합니다.|  
|[setArray](../../../connect/jdbc/reference/setarray-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 지정 된 배열 개체에 지정 된 매개 변수 번호를 설정합니다.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-sqlservercallablestatement.md)|지정된 매개 변수를 지정된 입력 스트림으로 설정합니다.|  
|[setBigDecimal](../../../connect/jdbc/reference/setbigdecimal-method-sqlservercallablestatement.md)|지정 된 BigDecimal 개체에 지정 된 매개 변수 번호를 설정합니다.|  
|[setBinaryStream](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)|지정된 매개 변수를 지정된 입력 스트림으로 설정합니다.|  
|[setBlob](../../../connect/jdbc/reference/setblob-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 지정 된 Blob 개체에 지정된 된 매개 변수를 설정합니다.|  
|[setboolean](../../../connect/jdbc/reference/setboolean-method-sqlservercallablestatement.md)|지정된 된 매개 변수 설정 하는 지정 된 **부울** 값입니다.|  
|[setByte](../../../connect/jdbc/reference/setbyte-method-sqlservercallablestatement.md)|지정된 된 매개 변수 설정 하는 지정 된 **바이트** 값입니다.|  
|[setBytes](../../../connect/jdbc/reference/setbytes-method-sqlservercallablestatement.md)|지정 된 배열에 지정된 된 매개 변수를 설정 **바이트** 값입니다.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservercallablestatement.md)|지정된 된 판독기 개체를 지정된 된 매개 변수를 설정합니다.|  
|[setClob](../../../connect/jdbc/reference/setclob-method-sqlservercallablestatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 지정된 매개 변수를 지정된 개체로 설정합니다.|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) SQL 커서 이름을 이후 실행 메서드에 사용될 지정된 문자열로 설정합니다.|  
|[setDate](../../../connect/jdbc/reference/setdate-method-sqlservercallablestatement.md)|지정된 매개 변수를 지정된 날짜 값으로 설정합니다.|  
|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md)|에 지정 된 열의 값을 설정 하는 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 값입니다.|  
|[setDouble](../../../connect/jdbc/reference/setdouble-method-sqlservercallablestatement.md)|지정 된 매개 변수를 설정 된 주어진 **double** 값입니다.|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 이스케이프 처리 모드를 설정합니다.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 결과 집합 행을 처리할 방향에 관한 힌트를 JDBC 드라이버에 제공합니다.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 추가 행이 필요할 경우 데이터베이스에서 인출되는 행 수에 관한 힌트를 JDBC 드라이버에 제공합니다.|  
|[setFloat](../../../connect/jdbc/reference/setfloat-method-sqlservercallablestatement.md)|지정 된 매개 변수를 지정 된 설정 **float** 값입니다.|  
|[setInt](../../../connect/jdbc/reference/setint-method-sqlservercallablestatement.md)|지정 된 매개 변수를 지정 된 설정 **int** 값입니다.|  
|[setLong](../../../connect/jdbc/reference/setlong-method-sqlservercallablestatement.md)|지정 된 매개 변수를 지정 된 설정 **긴** 값입니다.|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 바이트의 최대 수에 대 한 제한을 설정 하는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 문자 또는 이진 값을 지정 된 바이트 수를 저장 하는 열입니다.|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 최대 행 수에 대 한 제한을 설정 하는 모든 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체는 지정된 된 수로 포함 될 수 있습니다.|  
|[setNCharacterStream](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)|지정된 된 Reader 개체를 지정된 된 매개 변수를 설정합니다.|  
|[setNClob](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)|지정된 매개 변수를 지정된 개체로 설정합니다.|  
|[setNString](../../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md)|지정된 된 String 개체를 지정된 된 매개 변수를 설정합니다.|  
|[setNull](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)|설정할 매개 변수 형식이 지정된 경우 지정된 매개 변수를 null 값으로 설정합니다.|  
|[setObject](../../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)|지정된 개체를 사용하여 지정된 매개 변수의 값을 설정합니다.|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 문을 풀링하거나 풀링하지 않도록 요청합니다. 기본적으로 SQLServerCallableStatement 개체는 풀링 가능한 상태로 만들어집니다.|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 지정된 된 초 수를 실행 하는 CallableStatement 개체에 대 한 드라이버를 대기할 시간 (초)을 설정 합니다.|  
|[setRef](../../../connect/jdbc/reference/setref-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 지정된 된 Ref 개체에 지정된 된 매개 변수를 설정합니다.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|(에서 상속 되며, [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) 응답 버퍼링 모드를이 대 한 설정 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체를 대/소문자 구분 **문자열 전체** 또는 **적응**합니다.|  
|[setShort](../../../connect/jdbc/reference/setshort-method-sqlservercallablestatement.md)|지정 된 매개 변수를 지정 된 설정 **짧은** 값입니다.|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md)|지정 된 java 지정된 매개 변수를 설정 **문자열** 값입니다.|  
|[setSQLXML](../../../connect/jdbc/reference/setsqlxml-method-sqlservercallablestatement.md)|지정 된 매개 변수를 지정 된 설정 **SQLXML** 개체입니다.|  
|[setTime](../../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)|지정된 매개 변수를 지정된 시간 값으로 설정합니다.|  
|[setTimestamp](../../../connect/jdbc/reference/settimestamp-method-sqlservercallablestatement.md)|지정된 매개 변수를 지정된 타임스탬프 값으로 설정합니다.|  
|[setUnicodeStream](../../../connect/jdbc/reference/setunicodestream-method-sqlserverpreparedstatement.md)|(에서 상속 되며, [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).) 지정된 매개 변수 번호를 지정된 바이트 수를 포함하는 지정된 입력 스트림으로 설정합니다.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlservercallablestatement.md)|지정된 매개 변수를 지정된 URL 값으로 설정합니다.|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)|에 대 한 액세스를 허용 하도록 지정된 된 인터페이스를 구현 하는 개체를 반환 합니다.는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-특정 메서드.|  
|[wasNull](../../../connect/jdbc/reference/wasnull-method-sqlservercallablestatement.md)|마지막으로 읽은 OUT 매개 변수의 값이 SQL NULL인지 여부를 검색합니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerPreparedStatement|addBatch, clearBatch, clearParameters, close, execute, executeBatch, executeQuery, executeUpdate, getMetaData, getParameterMetaData, setArray, setAsciiStream, setBigDecimal, setBinaryStream, setBlob, setboolean, setByte, setBytes, setCharacterStream, setClob, setDate, setDouble, setFloat, setInt, setLong, setNull, setObject, setRef, setShort, setString, setTime, setTimestamp, setUnicodeStream, setURL|  
|com.microsoft.sqlserver.jdbc.SQLServerStatement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, isPoolable, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setPoolable, setQueryTimeout|  
|class java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.PreparedStatement|addBatch, clearParameters, execute, executeQuery, executeUpdate, getMetaData, getParameterMetaData, getSQLXML, setArray, setAsciiStream, setBigDecimal, setBinaryStream, setBlob, setboolean, setByte, setBytes, setCharacterStream, setClob, setDate, setDate, setDouble, setFloat, setInt, setLong, setNull, setObject, setRef, setShort, setString, setSQLXML, setTime, setTimestamp, setUnicodeStream, setURL|  
|java.sql.Statement|addBatch, cancel, clearBatch, clearWarnings, close, execute, executeBatch, executeQuery, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setQueryTimeout|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
