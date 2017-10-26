---
title: "SQLServerResultSet 멤버 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2a438d5d-2d6a-46a0-a2ae-f35fbae4a472
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 16088d8260afdd23c89d4d583153193b894f8249
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverresultset-members"></a>SQLServerResultSet 멤버
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  다음 표에서에 의해 노출 되는 멤버가 나와 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 클래스입니다.  
  
## <a name="constructors"></a>생성자  
 없음  
  
## <a name="fields"></a>필드  
  
|이름|Description|  
|----------|-----------------|  
|[CONCUR_SS_OPTIMISTIC_CC](../../../connect/jdbc/reference/concur-ss-optimistic-cc-field-sqlserverresultset.md)|지정 하는 데는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 읽기/쓰기 낙관적 동시성 유형 행 잠금이 없는 합니다.|  
|[CONCUR_SS_OPTIMISTIC_CCVAL](../../../connect/jdbc/reference/concur-ss-optimistic-ccval-field-sqlserverresultset.md)|지정 하는 데는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 읽기/쓰기 낙관적 동시성 유형 행 잠금이 없는 합니다.|  
|[CONCUR_SS_SCROLL_LOCKS](../../../connect/jdbc/reference/concur-ss-scroll-locks-field-sqlserverresultset.md)|지정 하는 데는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 읽기/쓰기 낙관적 동시성 유형 행 잠금 사용 합니다.|  
|[TYPE_SS_DIRECT_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-direct-forward-only-field-sqlserverresultset.md)|지정 하는 데는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 빠른 정방향 전용, 읽기 전용 커서 유형입니다.|  
|[TYPE_SS_SCROLL_DYNAMIC](../../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md)|지정 하는 데는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 동적 커서 유형입니다.|  
|[TYPE_SS_SCROLL_KEYSET](../../../connect/jdbc/reference/type-ss-scroll-keyset-field-sqlserverresultset.md)|지정 하는 데는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 키 집합 커서 유형입니다.|  
|[TYPE_SS_SCROLL_STATIC](../../../connect/jdbc/reference/type-ss-scroll-static-field-sqlserverresultset.md)|지정 하는 데는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 정적 커서 유형입니다.|  
|[TYPE_SS_SERVER_CURSOR_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-server-cursor-forward-only-field-sqlserverresultset.md)|지정 하는 데는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 빠른 정방향 전용, 읽기 전용 커서 유형입니다.|  
  
## <a name="inherited-fields"></a>상속된 필드  
  
|상속하는 원본 클래스|Description|  
|---------------------------|-----------------|  
|java.sql.ResultSet|CLOSE_CURSORS_AT_COMMIT, CONCUR_READ_ONLY, CONCUR_UPDATABLE, FETCH_FORWARD, FETCH_REVERSE, FETCH_UNKNOWN, HOLD_CURSORS_OVER_COMMIT, TYPE_FORWARD_ONLY, TYPE_SCROLL_INSENSITIVE, TYPE_SCROLL_SENSITIVE|  
  
## <a name="methods"></a>메서드  
  
|이름|Description|  
|----------|-----------------|  
|[절대](../../../connect/jdbc/reference/absolute-method-sqlserverresultset.md)|지정된 된 행이 커서 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[afterLast](../../../connect/jdbc/reference/afterlast-method-sqlserverresultset.md)|이 마지막 행 뒤에 커서를 이동 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[beforeFirst](../../../connect/jdbc/reference/beforefirst-method-sqlserverresultset.md)|이 첫 번째 행 앞에 커서를 이동 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[cancelRowUpdates](../../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md)|이 현재 행에 대 한 업데이트를 취소 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverresultset.md)|이 보고 된 모든 경고를 지웁니다 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[닫기](../../../connect/jdbc/reference/close-method-sqlserverresultset.md)|이 해제 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 데이터베이스와 JDBC 리소스를 자동으로 닫힐 때 동작을 기다리지 않고 즉시 해제 합니다.|  
|[deleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md)|이 통해 현재 행을 삭제[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체와 기본 데이터베이스입니다.|  
|[마무리](../../../connect/jdbc/reference/finalize-method-sqlserverresultset.md)|이것을 명시적으로 닫으면 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[findColumn](../../../connect/jdbc/reference/findcolumn-method-sqlserverresultset.md)|이 지정 된 열 이름에 대 한 첫 번째 일치 하는 열의 인덱스를 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[첫 번째](../../../connect/jdbc/reference/first-method-sqlserverresultset.md)|이 첫 번째 행으로 커서 이동 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[getArray](../../../connect/jdbc/reference/getarray-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Array 개체로 개체입니다.|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) ASCII 문자의 스트림으로 개체입니다.|  
|[getBigDecimal](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열 인덱스의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체 java.math.BigDecimal로 반환 합니다.|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 해석 되지 않은 바이트의 이진 스트림으로 개체입니다.|  
|[getBlob](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Java 프로그래밍 언어의에서 Blob 개체로 개체입니다.|  
|[getBoolean](../../../connect/jdbc/reference/getboolean-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **부울** Java 프로그래밍 언어의에서 합니다.|  
|[getByte](../../../connect/jdbc/reference/getbyte-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **바이트** Java 프로그래밍 언어의에서 합니다.|  
|[getBytes](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **바이트** Java 프로그래밍 언어의에서 배열입니다.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체 java.io.Reader 개체로 반환 합니다.|  
|[getClob](../../../connect/jdbc/reference/getclob-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Java 프로그래밍 언어의에서 Clob 개체로 개체입니다.|  
|[getConcurrency](../../../connect/jdbc/reference/getconcurrency-method-sqlserverresultset.md)|이 동시성 모드를 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[getCursorName](../../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md)|사용 하는 SQL 커서의 이름을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[getDate](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Java 프로그래밍 언어의에서 java.sql.Date 개체로 개체입니다.|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)|지정 된 열의 값을 검색 하는[DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체입니다.|  
|[getDouble](../../../connect/jdbc/reference/getdouble-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **double** Java 프로그래밍 언어의에서 합니다.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverresultset.md)|이 대 한 인출 방향을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md)|이 대 한 인출 크기를 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[getFloat](../../../connect/jdbc/reference/getfloat-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **float** Java 프로그래밍 언어의에서 합니다.|  
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverresultset.md)|이 유지 기능을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[getInt](../../../connect/jdbc/reference/getint-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **int** Java 프로그래밍 언어의에서 합니다.|  
|[getLong](../../../connect/jdbc/reference/getlong-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **긴** Java 프로그래밍 언어의에서 합니다.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)|수, 형식 및이 속성을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 열입니다.|  
|[getNCharacterStream](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)|현재 행에서 지정 된 열의 값을 검색 하는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 판독기 개체로 개체입니다.|  
|[getNClob](../../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)|현재 행에서 지정 된 열의 값을 검색 하는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)개체로 **NClob** Java 프로그래밍 언어의에서 개체입니다.|  
|[getNString](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)|현재 행에서 지정 된 열의 값을 검색 하는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 문자열로 java에서 프로그래밍 언어입니다.|  
|[getObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 가져옵니다 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Java 프로그래밍 언어의에서 개체로 개체입니다.|  
|[getRef](../../../connect/jdbc/reference/getref-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Java 프로그래밍 언어의에서 Ref 개체로 개체입니다.|  
|[getRow](../../../connect/jdbc/reference/getrow-method-sqlserverresultset.md)|현재 행 번호를 검색합니다.|  
|[getShort](../../../connect/jdbc/reference/getshort-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **짧은** Java 프로그래밍 언어의에서 합니다.|  
|[getStatement](../../../connect/jdbc/reference/getstatement-method-sqlserverresultset.md)|검색 된 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 이 생성 한 개체를 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[getString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **문자열** Java 프로그래밍 언어의에서 합니다.|  
|[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)|현재 행에서 지정 된 열의 값을 검색 하는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **SQLXML** 개체입니다.|  
|[getTime](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Java 프로그래밍 언어의에서 java.sql.Time 개체로 개체입니다.|  
|[getTimestamp](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Java 프로그래밍 언어의에서 java.sql.Timestamp 개체로 개체입니다.|  
|[getType](../../../connect/jdbc/reference/gettype-method-sqlserverresultset.md)|이 커서 유형을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[getUnicodeStream](../../../connect/jdbc/reference/getunicodestream-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 유니코드 문자의 스트림으로 개체입니다.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverresultset.md)|이 현재 행에서 지정 된 열의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) URL 개체로 개체입니다.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverresultset.md)|이 호출에서 보고 된 첫 번째 경고 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md)|이 삽입 행의 내용을 삽입 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체와 해당 데이터베이스에 있습니다.|  
|[isAfterLast](../../../connect/jdbc/reference/isafterlast-method-sqlserverresultset.md)|이 마지막 행 뒤에 커서가 있는지 여부를 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[isBeforeFirst](../../../connect/jdbc/reference/isbeforefirst-method-sqlserverresultset.md)|커서가 첫 번째 행이 있는지 여부를 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverresultset.md)|나타냅니다 여부이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체가 잠겨 있습니다.|  
|[isFirst](../../../connect/jdbc/reference/isfirst-method-sqlserverresultset.md)|커서가 첫 번째 행에 있는지 여부를 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[isLast](../../../connect/jdbc/reference/islast-method-sqlserverresultset.md)|커서가 마지막 행에 있는지 여부를 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[마지막](../../../connect/jdbc/reference/last-method-sqlserverresultset.md)|커서의 마지막 행이 이동 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[moveToCurrentRow](../../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)|커서를 저장된 커서 위치(대개 현재 행)로 이동합니다.|  
|[moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md)|커서를 삽입 행으로 이동합니다.|  
|[다음](../../../connect/jdbc/reference/next-method-sqlserverresultset.md)|커서를 현재 위치에서 한 행 아래로 이동합니다.|  
|[이전](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md)|이 이전 행으로 커서 이동 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[refreshRow](../../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md)|데이터베이스의 최신 값으로 현재 행을 새로 고칩니다.|  
|[상대](../../../connect/jdbc/reference/relative-method-sqlserverresultset.md)|현재 행을 기준으로 지정된 행 수만큼 커서를 양의 방향 또는 음의 방향으로 이동합니다.|  
|[rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md)|행이 삭제되었는지 여부를 검색합니다.|  
|[rowInserted](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md)|현재 행에 삽입된 내용이 있는지 여부를 검색합니다.|  
|[rowUpdated](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md)|현재 행이 업데이트되었는지 여부를 검색합니다.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md)|방향에 관한 힌트를 제공이 행 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체 처리 됩니다.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)|데이터베이스에서이 대 한 추가 행이 필요할 때 인출 되는 행 수에 관한 힌트를 JDBC 드라이버에 제공 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[updateArray](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)|Array 개체와 지정된 된 열을 업데이트 합니다.|  
|[updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)|지정된 열을 ASCII 스트림 값으로 업데이트합니다.|  
|[updateBigDecimal](../../../connect/jdbc/reference/updatebigdecimal-method-sqlserverresultset.md)|BigDecimal 개체와 지정된 된 열을 업데이트 합니다.|  
|[updateBinaryStream](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)|지정된 열을 이진 스트림 값으로 업데이트합니다.|  
|[updateBlob](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)|지정된 열을 java.sql.Blob 값으로 업데이트합니다.|  
|[updateBoolean](../../../connect/jdbc/reference/updateboolean-method-sqlserverresultset.md)|으로 지정된 된 열 업데이트는 **부울** 값입니다.|  
|[updateByte](../../../connect/jdbc/reference/updatebyte-method-sqlserverresultset.md)|으로 지정된 된 열 업데이트는 **바이트** 값입니다.|  
|[updateBytes](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)|지정된 된 열을의 배열로 업데이트 **바이트** 값입니다.|  
|[updateCharacterStream](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)|지정된 열을 문자 스트림 값으로 업데이트합니다.|  
|[updateClob](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)|지정된 열을 java.sql.Clob 값으로 업데이트합니다.|  
|[updateDate](../../../connect/jdbc/reference/updatedate-method-sqlserverresultset.md)|지정된 열을 날짜 값으로 업데이트합니다.|  
|[updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)|업데이트는 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 열입니다.|  
|[updateDouble](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)|으로 지정된 된 열 업데이트는 **double** 값입니다.|  
|[updateFloat](../../../connect/jdbc/reference/updatefloat-method-sqlserverresultset.md)|으로 지정된 된 열 업데이트는 **float** 값입니다.|  
|[updateInt](../../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)|으로 지정된 된 열 업데이트는 **int** 값입니다.|  
|[updateLong](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)|으로 지정된 된 열 업데이트는 **긴** 값입니다.|  
|[updateNCharacterStream](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)|지정된 열을 문자 스트림 값으로 업데이트합니다.|  
|[updateNClob](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)|지정된 열을 지정된 개체 값으로 업데이트합니다.|  
|[updateNString](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)|으로 지정된 된 열 업데이트는 **문자열** 값입니다.|  
|[updateNull](../../../connect/jdbc/reference/updatenull-method-sqlserverresultset.md)|지정된 열을 null 값으로 업데이트합니다.|  
|[updateObject](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)|으로 지정된 된 열 업데이트는 **개체** 값입니다.|  
|[updateRef](../../../connect/jdbc/reference/updateref-method-sqlserverresultset.md)|지정된 열을 java.sql.Ref 값으로 업데이트합니다.|  
|[updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)|기본 데이터베이스의 현재 행이 새 내용으로 업데이트 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.|  
|[updateShort](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)|으로 지정된 된 열 업데이트는 **짧은** 값입니다.|  
|[updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)|으로 지정된 된 열 업데이트는 **문자열** 값입니다.|  
|[updateSQLXML](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)|으로 지정된 된 열 업데이트는 **SQLXML** 값입니다.|  
|[updateTime](../../../connect/jdbc/reference/updatetime-method-sqlserverresultset.md)|지정된 열을 시간 값으로 업데이트합니다.|  
|[updateTimestamp](../../../connect/jdbc/reference/updatetimestamp-method-sqlserverresultset.md)|지정된 열을 타임스탬프 값으로 업데이트합니다.|  
|[wasNull](../../../connect/jdbc/reference/wasnull-method-sqlserverresultset.md)|마지막으로 읽은 값이 null 값이었는지 여부를 확인합니다.|  
  
## <a name="inherited-methods"></a>상속된 메서드  
  
|상속하는 원본 클래스|메서드|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

