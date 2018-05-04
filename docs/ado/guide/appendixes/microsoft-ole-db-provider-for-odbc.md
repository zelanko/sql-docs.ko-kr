---
title: Microsoft OLE DB Provider for ODBC | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for ODBC [ADO]
- providers [ADO], OLE DB provider for ODBC
ms.assetid: 2dc0372d-e74d-4d0f-9c8c-04e5a168c148
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 612ca78e6af181aaf3e2d3b1eb16ae5fea7eec3c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>Microsoft OLE DB Provider for ODBC 개요
ADO 또는 RDS 프로그래머가 이상적인 것 모든 데이터에서 원본에서 OLE DB 인터페이스를 제공 ADO 데이터 원본으로 직접 호출할 수 있도록 합니다. 하지만 점점 더 많은 데이터베이스 공급 업체 OLE DB 인터페이스를 구현 하는 경우 일부 데이터 원본은이 방식으로 아직 노출 되지 않습니다. 그러나 현재 사용 중인 대부분의 DBMS 시스템 ODBC를 통해 액세스할 수 있습니다.

 ODBC 드라이버는 Microsoft SQL Server, Microsoft 액세스 (Microsoft Jet 데이터베이스 엔진) 및 Microsoft FoxPro Oracle과 같은 타사 데이터베이스 제품 외에도 포함 하 여 오늘날 사용 중인 모든 주요 DBMS에 사용할 수 있습니다.

 그러나 Microsoft ODBC 공급자는 ADO를 모든 ODBC 데이터 원본에 연결할 수 있습니다. 공급자는 자유 스레드 및 유니코드를 사용할 수 있습니다.

 공급자 지원 트랜잭션을 DBMS 엔진 마다 다른 유형의 트랜잭션 지원 제공 합니다. 예를 들어 중첩 된 트랜잭션을 5 단계까지 지원 됩니다.

 ADO에 대 한 기본 공급자 이며 모든 공급자에 종속 된 ADO 속성 및 메서드 지원 됩니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결할 설정는 **공급자 =** 의 인수는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성:

```
MSDASQL
```

 읽기는 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성은이 문자열을 반환 합니다.

## <a name="typical-connection-string"></a>일반적인 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은:

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 이러한 키워드의 문자열 구성 됩니다.

|키워드|Description|
|-------------|-----------------|
|**공급자**|ODBC 용 OLE DB 공급자를 지정합니다.|
|**DSN**|데이터 원본 이름을 지정합니다.|
|**UID**|사용자 이름을 지정합니다.|
|**PWD**|사용자 암호를 지정합니다.|
|**URL**|파일 또는 웹 폴더에 게시 하는 디렉터리의 URL을 지정 합니다.|

 생략 하면 이것이 ADO에 대 한 기본 공급자는 **공급자 =** ADO 연결 문자열에서 매개 변수는이 공급자에 대 한 연결을 설정 하려고 합니다.

> [!NOTE]
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, **Trusted_Connection = yes** 또는 **통합 보안 = SSPI** 사용자 ID와 암호 대신 연결 문자열에 대 한 정보입니다.

 공급자는 ADO에서 정의 된 권한과 함께 특정 연결 매개 변수를 지원 하지 않습니다. 그러나 공급자는 ODBC 드라이버 관리자를 비 ADO 연결 매개 변수를 전달 합니다.

 생략할 수 있으므로 **공급자** 매개 변수를 구성할 수 있습니다 따라서 동일한 데이터 원본에 대 한 ODBC 연결 문자열과 동일 하 게 ADO 연결 문자열입니다. 동일한 매개 변수 이름을 사용 하 여 (**드라이버 =**, **데이터베이스 =**, **DSN =** 등), 값 및 구문으로는 ODBC 연결 문자열을 작성할 때. 또는 미리 정의 된 데이터 원본 이름 (DSN) 또는 FileDSN 없이 연결할 수 있습니다.

## <a name="syntax-with-a-dsn-or-filedsn"></a>DSN 또는 FileDSN 구문:

```
"[Provider=MSDASQL;] { DSN=name | FileDSN=filename } ;
[DATABASE=database;] UID=user; PWD=password"
```

## <a name="syntax-without-a-dsn-dsn-less-connection"></a>DSN (DSN 없는 연결) 없이 구문:

```
"[Provider=MSDASQL;] DRIVER=driver; SERVER=server;
DATABASE=database; UID=MyUserID; PWD=MyPassword"
```

## <a name="remarks"></a>주의
 사용 하는 경우는 **DSN** 또는 **FileDSN**, Windows 제어판의 ODBC 데이터 원본 관리자를 통해 정의 해야 합니다. Microsoft Windows 2000에서 ODBC 관리자 관리 도구에 있습니다. 이전 버전의 Windows에서 ODBC 관리자 아이콘 이름은 **32 비트 ODBC** 또는 그냥 **ODBC**합니다.

 설정 하는 대신 한 **DSN**, ODBC 드라이버를 지정할 수 있습니다 (**드라이버 =**), "SQL server;" 서버 이름 (**서버 =**); 및 데이터베이스 이름 (**데이터베이스 =**).

 사용자 계정 이름을 지정할 수도 있습니다 (**UID =**), 및 사용자 계정에 대 한 암호 (**PWD =**) 또는 표준 ODBC 관련 매개 변수에서 ADO 정의 *사용자* 및 *암호* 매개 변수입니다.

 하지만 **DSN** 정의가 이미 데이터베이스를 지정 하는 경우 지정할 수 있습니다 *는* *데이터베이스* 외에 매개 변수는 **DSN** 연결 하려면 다른 데이터베이스입니다. 항상 포함 해야 하는 것이 좋습니다 *는* *데이터베이스* 사용 하는 경우 매개 변수는 **DSN**합니다. 이 방법을 사용 하면 마지막으로 확인 후 다른 사용자의 기본 데이터베이스 매개 변수를 변경 하는 경우 올바른 데이터베이스에 연결 된 **DSN** 정의 합니다.

## <a name="provider-specific-connection-properties"></a>공급자별 연결 속성
 하도록 여러 가지 속성을 추가 하는 OLE DB provider for ODBC는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 의 컬렉션은 **연결** 개체입니다. 다음 표에서 이러한 속성을 해당 OLE DB 속성 이름이 괄호 안에 나열합니다.

|속성 이름|Description|
|-------------------|-----------------|
|액세스 가능한 프로시저 (KAGPROP_ACCESSIBLEPROCEDURES)|저장된 프로시저에 대 한 액세스 권한이 있는지 여부를 나타냅니다.|
|액세스 가능한 테이블이 (KAGPROP_ACCESSIBLETABLES)|사용자에 게 데이터베이스 테이블에 대해 SELECT 문을 실행할 수 있는 권한이 있는지 여부를 나타냅니다.|
|활성 문 (KAGPROP_ACTIVESTATEMENTS)|ODBC 드라이버는 연결에서 지원할 수 있는 핸들 수를 나타냅니다.|
|드라이버 이름 (KAGPROP_DRIVERNAME)|ODBC 드라이버의 파일 이름을 나타냅니다.|
|드라이버 ODBC 버전 (KAGPROP_DRIVERODBCVER)|이 드라이버를 지원 하 고 있는 ODBC의 버전을 나타냅니다.|
|파일 사용 (KAGPROP_FILEUSAGE)|드라이버는 데이터 소스에 있는 파일을 처리 하는 방법을 나타냅니다. 테이블 또는 카탈로그입니다.|
|Like 이스케이프 절 (KAGPROP_LIKEESCAPECLAUSE)|WHERE 절에 LIKE 조건자에서 지원 하는지 여부는 드라이버 정 및 사용 하 여 이스케이프 문자 백분율 문자 (%)에 대 한 및 밑줄 문자 (_)을 나타냅니다.|
|Group By (KAGPROP_MAXCOLUMNSINGROUPBY)의 최대 열|SELECT 문의 GROUP BY 절에 나열 될 수 있는 열의 최대 수를 나타냅니다.|
|인덱스 (KAGPROP_MAXCOLUMNSININDEX)의 최대 열|인덱스에 포함 될 수 있는 열의 최대 수를 나타냅니다.|
|Order By (KAGPROP_MAXCOLUMNSINORDERBY)의 최대 열|SELECT 문의 ORDER BY 절에 나열 될 수 있는 열의 최대 수를 나타냅니다.|
|Select (KAGPROP_MAXCOLUMNSINSELECT)의 최대 열|SELECT 문의 SELECT 부분에 나열 될 수 있는 열의 최대 수를 나타냅니다.|
|테이블 (KAGPROP_MAXCOLUMNSINTABLE)의 최대 열|테이블에서 허용 하는 열의 최대 수를 나타냅니다.|
|숫자 함수 (KAGPROP_NUMERICFUNCTIONS)|ODBC 드라이버에서 지원 되는 숫자 함수를 나타냅니다. 함수 이름 및이 비트 마스크에 사용 되는 연결 된 값의 목록을 보려면 [부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), ODBC 설명서에 있습니다.|
|외부 조인 기능 (KAGPROP_OJCAPABILITY)|공급자에서 지 원하는 외부 조인 유형을 나타냅니다.|
|외부 조인 (KAGPROP_OUTERJOINS)|공급자에 외부 조인 지원 하는지 여부를 나타냅니다.|
|특수 문자 (KAGPROP_SPECIALCHARACTERS)|ODBC 드라이버에 대 한 특별 한 의미를 가지는 문자를 나타냅니다.|
|저장된 프로시저 (KAGPROP_PROCEDURES)|저장된 프로시저는이 ODBC 드라이버를 사용할 수 있는지 여부를 나타냅니다.|
|문자열 함수 (KAGPROP_STRINGFUNCTIONS)|ODBC 드라이버에서 지원 되는 문자열 함수를 나타냅니다. 함수 이름 및이 비트 마스크에 사용 되는 연결 된 값의 목록을 보려면 [부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), ODBC 설명서에 있습니다.|
|시스템 함수 (KAGPROP_SYSTEMFUNCTIONS)|ODBC 드라이버에서 지원 되는 시스템 함수를 나타냅니다. 함수 이름 및이 비트 마스크에 사용 되는 연결 된 값의 목록을 보려면 [부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), ODBC 설명서에 있습니다.|
|날짜/시간 함수 (KAGPROP_TIMEDATEFUNCTIONS)|ODBC 드라이버에서 지원 되는 날짜 및 시간 함수를 나타냅니다. 함수 이름 및이 비트 마스크에 사용 되는 연결 된 값의 목록을 보려면 [부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), ODBC 설명서에 있습니다.|
|SQL 문법 지원 (KAGPROP_ODBCSQLCONFORMANCE)|ODBC 드라이버에서 지 원하는 SQL 문법을 나타냅니다.|

## <a name="provider-specific-recordset-and-command-properties"></a>공급자 관련 레코드 집합과 명령 속성
 하도록 여러 가지 속성을 추가 하는 OLE DB provider for ODBC는 **속성** 의 컬렉션은 **레코드 집합** 및 **명령** 개체입니다. 다음 표에서 이러한 속성을 해당 OLE DB 속성 이름이 괄호 안에 나열합니다.

|속성 이름|Description|
|-------------------|-----------------|
|쿼리 기반 업데이트/삭제/삽입 (KAGPROP_QUERYBASEDUPDATES)|SQL 쿼리를 사용 하 여 업데이트, 삭제 및 삽입 수행 여부를 나타냅니다.|
|ODBC 동시성 유형을 (KAGPROP_CONCURRENCY)|데이터 원본에서 동일한 데이터를 동시에 액세스 하려는 두 사용자로 인 한 잠재적 문제를 줄이기 위해 사용 되는 메서드를 나타냅니다.|
|정방향 전용 커서 (KAGPROP_BLOBSONFOCURSOR)에서 BLOB 액세스 가능성|표시 여부 BLOB **필드** 정방향 전용 커서를 사용 하는 경우에 액세스할 수 있습니다.|
|QBU WHERE clauses (KAGPROP_INCLUDENONEXACT)에 SQL_FLOAT, SQL_DOUBLE, 및 SQL_REAL 포함|SQL_FLOAT, SQL_DOUBLE, 및 SQL_REAL 값 QBU WHERE 절에 포함 될 수 있는지 여부를 나타냅니다.|
|Insert (KAGPROP_POSITIONONNEWROW) 한 후 마지막 행에 위치|새 레코드를 테이블에 삽입 한 후 테이블의 마지막 행 않을 것인지 나타냅니다 현재 행에와 야 합니다.|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO)|나타냅니다 여부는 **IRowsetChange** 인터페이스 지원 확장된 정보를 제공 합니다.|
|ODBC 커서 유형 (KAGPROP_CURSOR)|사용 하는 커서의 유형을 나타냅니다는 **레코드 집합**합니다.|
|마샬링할 수 있는 행 집합을 생성 (KAGPROP_MARSHALLABLE)|ODBC 드라이버를 마샬링할 수 있는 레코드 집합 생성을 나타냅니다.|

## <a name="command-text"></a>명령 텍스트
 사용 하는 방법의 [명령](../../../ado/reference/ado-api/command-object-ado.md) 수락할 어떤 유형의 쿼리 또는 명령 문 및 개체는 주로 데이터 원본에 따라 다릅니다.

 ODBC 저장된 프로시저를 호출 하는 특정 구문을 제공 합니다. 에 대 한는 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성은 **명령** 개체는 *CommandText* 인수를는 **Execute** 메서드를 한 [ 연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 또는 *소스* 인수를는 **열려** 메서드를는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를이 구문 사용 하는 문자열에 전달.

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , … ]] ) ] }"
```

 각 **?** 개체를 참조는 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션입니다. 첫 번째 **?** 참조 **매개 변수**(0), 다음 **?** 참조 **매개 변수**(1) 등입니다.

 매개 변수 참조는 옵션이 며 저장된 프로시저의 구조에 따라 달라 집니다. 매개 변수를 정의 하는 저장된 프로시저를 호출 하려는 경우 문자열에는 다음과 같습니다.

```
"{ call procedure }"
```

 두 개의 쿼리 매개 변수를 설정한 경우 문자열에는 다음과 유사 합니다.

```
"{ call procedure ( ?, ? ) }"
```

 저장된 프로시저는 값을 반환 하는 경우 반환 값은 다른 매개 변수로 처리 됩니다. 쿼리 매개 변수가 없는 있지만 반환 값이 있는 경우 문자열에는 다음과 유사 합니다.

```
"{ ? = call procedure }"
```

 마지막으로, 반환 값을 갖는 두 개의 쿼리 매개 변수를 문자열에는 다음과 유사 합니다.

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>레코드 집합 동작
 다음 표에서 표준 ADO 메서드 및 속성에 사용할 수는 **레코드 집합** 이 공급자와 개체를 열입니다.

 에 대 한 자세한 내용을 보려면 **레코드 집합** 실행 공급자 구성에 대 한 동작은 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드 열거는 **속성** 의 컬렉션은 **레코드 집합** 공급자별 동적 속성은 있는지 여부를 확인 하려면.

 표준 ADO의 가용성을 **레코드 집합** 속성:

|속성|ForwardOnly|Dynamic|Keyset|정적|
|--------------|-----------------|-------------|------------|------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|사용할 수 없음|사용할 수 없음|읽기/쓰기|읽기/쓰기|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|사용할 수 없음|사용할 수 없음|읽기/쓰기|읽기/쓰기|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|읽기 전용|읽기 전용|읽기 전용|읽기 전용|
|[Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md)|사용할 수 없음|사용할 수 없음|읽기/쓰기|읽기/쓰기|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|읽기 전용|읽기 전용|읽기 전용|읽기 전용|
|[필터](../../../ado/reference/ado-api/filter-property.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|읽기/쓰기|사용할 수 없음|읽기 전용|읽기 전용|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|읽기/쓰기|사용할 수 없음|읽기 전용|읽기 전용|
|[원본](../../../ado/reference/ado-api/source-property-ado-recordset.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[State](../../../ado/reference/ado-api/state-property-ado.md)|읽기 전용|읽기 전용|읽기 전용|읽기 전용|
|[상태](../../../ado/reference/ado-api/status-property-ado-recordset.md)|읽기 전용|읽기 전용|읽기 전용|읽기 전용|

 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) 및 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 속성은 쓰기 전용 ADO ODBC 용 Microsoft OLE DB 공급자의 버전 1.0과 함께 사용 된 경우.

 표준 ADO의 가용성을 **레코드 집합** 메서드:

|메서드|ForwardOnly|Dynamic|Keyset|정적|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[취소](../../../ado/reference/ado-api/cancel-method-ado.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[복제](../../../ado/reference/ado-api/clone-method-ado.md)|아니요|아니오|사용자 계정 컨트롤|예|
|[닫기](../../../ado/reference/ado-api/close-method-ado.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[이동](../../../ado/reference/ado-api/move-method-ado.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|아니요|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|아니요|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)*|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[열기](../../../ado/reference/ado-api/open-method-ado-recordset.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[다시 쿼리](../../../ado/reference/ado-api/requery-method.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[다시 동기화](../../../ado/reference/ado-api/resync-method.md)|아니요|아니오|사용자 계정 컨트롤|예|
|[지원](../../../ado/reference/ado-api/supports-method.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[업데이트](../../../ado/reference/ado-api/update-method.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|예|사용자 계정 컨트롤|사용자 계정 컨트롤|예|

 * Microsoft Access 데이터베이스에 지원 되지 않습니다.

## <a name="dynamic-properties"></a>동적 속성
 에 여러 동적 속성을 삽입 하는 Microsoft OLE DB Provider for ODBC는 **속성** 컬렉션은 열려 있지 않은 [연결](../../../ado/reference/ado-api/connection-object-ado.md), [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 및 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다.

 다음 표는 각 동적 속성에 대 한 OLE DB 및 ADO 이름의 상호 인덱스입니다. "Description" 이라는 용어는 ADO 속성 이름을 나타내며 OLE DB 프로그래머 참조 OLE DB 프로그래머 참조에서 이러한 속성에 대 한 자세한 정보를 찾을 수 있습니다. 인덱스에서 OLE DB 속성 이름을 검색 하거나 참조 [부록 c: OLE DB 속성](http://msdn.microsoft.com/en-us/deded3ff-f508-4e1b-b2b1-fd9afd3bd292)합니다.

## <a name="connection-dynamic-properties"></a>연결의 동적 속성
 다음 속성에 추가 되는 **연결** 개체의 **속성** 컬렉션입니다.

|ADO 속성 이름|OLE DB 속성 이름|
|-----------------------|--------------------------|
|Active Sessions|DBPROP_ACTIVESESSIONS|
|비동기 가능 중단|DBPROP_ASYNCTXNABORT|
|비동기 가능 커밋|DBPROP_ASYNCTNXCOMMIT|
|격리 수준 자동 커밋|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|카탈로그 위치|DBPROP_CATALOGLOCATION과 같습니다|
|카탈로그 용어가|DBPROP_CATALOGTERM|
|열 정의|DBPROP_COLUMNDEFINITION|
|연결 제한 시간|DBPROP_INIT_TIMEOUT|
|현재 카탈로그|DBPROP_CURRENTCATALOG|
|데이터 원본|DBPROP_INIT_DATASOURCE|
|Data Source Name|DBPROP_DATASOURCENAME|
|데이터 소스 개체 스레딩 모델|DBPROP_DSOTHREADMODEL|
|DBMS 이름|DBPROP_DBMSNAME|
|DBMS 버전|DBPROP_DBMSVER|
|Extended Properties|DBPROP_INIT_PROVIDERSTRING|
|지원 기준으로 그룹화|DBPROP_GROUPBY와 같습니다|
|유형이 다른 테이블 지원|DBPROP_HETEROGENEOUSTABLES와 같습니다|
|식별자 대/소문자 구분|DBPROP_IDENTIFIERCASE|
|초기 카탈로그|DBPROP_INIT_CATALOG|
|격리 수준|DBPROP_SUPPORTEDTXNISOLEVELS|
|격리 보존|DBPROP_SUPPORTEDTXNISORETAIN|
|로캘 ID|DBPROP_INIT_LCID|
|위치|DBPROP_INIT_LOCATION|
|최대 인덱스 크기|DBPROP_MAXINDEXSIZE와 같습니다|
|최대 행 크기|DBPROP_MAXROWSIZE와 같습니다|
|BLOB 포함 최대 행 크기|DBPROP_MAXROWSIZEINCLUDESBLOB|
|SELECT의 최대 테이블|DBPROP_MAXTABLESINSELECT|
|모드|DBPROP_INIT_MODE|
|여러 매개 변수 집합|DBPROP_MULTIPLEPARAMSETS|
|여러 결과|DBPROP_MULTIPLERESULTS|
|여러 저장소 개체|DBPROP_MULTIPLESTORAGEOBJECTS|
|여러 테이블 업데이트|DBPROP_MULTITABLEUPDATE|
|NULL 데이터 정렬 순서|DBPROP_NULLCOLLATION과 같습니다|
|NULL 연결 동작|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB 서비스|DBPROP_INIT_OLEDBSERVICES|
|OLE DB 버전|DBPROP_PROVIDEROLEDBVER|
|OLE 개체 지원|DBPROP_OLEOBJECTS|
|열린 행 집합 지원|DBPROP_OPENROWSETSUPPORT|
|선택 목록의 열으로 정렬|DBPROP_ORDERBYCOLUMNSINSELECT|
|출력 매개 변수 가용성|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|암호|DBPROP_AUTH_PASSWORD|
|Ref 접근자로 전달|DBPROP_BYREFACCESSORS|
|보안 정보 유지|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
|영구 ID 유형|DBPROP_PERSISTENTIDTYPE|
|중단 동작 준비|DBPROP_PREPAREABORTBEHAVIOR와 같습니다|
|커밋 동작 준비|DBPROP_PREPARECOMMITBEHAVIOR와 같습니다|
|프로시저 용어가|DBPROP_PROCEDURETERM|
|프롬프트|DBPROP_INIT_PROMPT|
|공급자 이름|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|공급자 버전|DBPROP_PROVIDERVER|
|읽기 전용 데이터 원본|DBPROP_DATASOURCEREADONLY와 같습니다|
|명령 시 행 집합 변환|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|스키마 용어|DBPROP_SCHEMATERM|
|스키마 사용|DBPROP_SCHEMAUSAGE|
|SQL 지원|DBPROP_SQLSUPPORT|
|구조적된 저장소|DBPROP_STRUCTUREDSTORAGE|
|하위 쿼리 지원|DBPROP_SUBQUERIES|
|테이블 용어|DBPROP_TABLETERM|
|트랜잭션 DDL|DBPROP_SUPPORTEDTXNDDL|
|사용자 ID|DBPROP_AUTH_USERID|
|사용자 이름|DBPROP_USERNAME|
|창 핸들|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>레코드 집합 동적 속성
 다음 속성에 추가 되는 **레코드 집합** 개체의 **속성** 컬렉션입니다.

|ADO 속성 이름|OLE DB 속성 이름|
|-----------------------|--------------------------|
|액세스 순서|DBPROP_ACCESSORDER|
|저장소 개체 차단|DBPROP_BLOCKINGSTORAGEOBJECTS|
|책갈피 유형|DBPROP_BOOKMARKTYPE|
|책갈피를 설정할|DBPROP_IROWSETLOCATE|
|삽입 된 행 변경|DBPROP_CHANGEINSERTEDROWS|
|열 권한|DBPROP_COLUMNRESTRICT|
|열 집합 알림|DBPROP_NOTIFYCOLUMNSET|
|저장소 개체 업데이트 연기|DBPROP_DELAYSTORAGEOBJECTS|
|뒤로 페치|DBPROP_CANFETCHBACKWARDS|
|행 보관|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|부동 행|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|리터럴 책갈피|DBPROP_LITERALBOOKMARKS|
|리터럴 행 Id|DBPROP_LITERALIDENTITY|
|최대 열린 행 수|DBPROP_MAXOPENROWS|
|최대 보류 중인 행|DBPROP_MAXPENDINGROWS|
|최대 행 수|DBPROP_MAXROWS|
|알림 세분성|DBPROP_NOTIFICATIONGRANULARITY|
|알림 단계|DBPROP_NOTIFICATIONPHASES|
|트랜잭션 개체|DBPROP_TRANSACTEDOBJECT|
|내 변경 내용 표시|DBPROP_OWNUPDATEDELETE|
|직접 삽입 표시|DBPROP_OWNINSERT|
|중단 시 유지|DBPROP_ABORTPRESERVE|
|커밋 시 유지|DBPROP_COMMITPRESERVE|
|빠른 다시 시작|DBPROP_QUICKRESTART|
|재진입 이벤트|DBPROP_REENTRANTEVENTS|
|삭제 된 행 제거|DBPROP_REMOVEDELETED|
|여러 변경 내용 보고|DBPROP_REPORTMULTIPLECHANGES|
|보류 중인 삽입 반환|DBPROP_RETURNPENDINGINSERTS|
|행 삭제 알림|DBPROP_NOTIFYROWDELETE|
|행 처음 변경 알림|DBPROP_NOTIFYROWFIRSTCHANGE|
|행 삽입 알림|DBPROP_NOTIFYROWINSERT|
|행 권한|DBPROP_ROWRESTRICT|
|행 다시 동기화 알림|DBPROP_NOTIFYROWRESYNCH|
|행 스레딩 모델|DBPROP_ROWTHREADMODEL|
|행 변경 취소 알림|DBPROP_NOTIFYROWUNDOCHANGE|
|행 삭제 취소 알림|DBPROP_NOTIFYROWUNDODELETE|
|행 삽입 취소 알림|DBPROP_NOTIFYROWUNDOINSERT|
|행 업데이트 알림|DBPROP_NOTIFYROWUPDATE|
|행 집합 페치 위치 변경 알림|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|행 집합 릴리스 알림|DBPROP_NOTIFYROWSETRELEASE|
|뒤로 스크롤|DBPROP_CANSCROLLBACKWARDS|
|삭제 한 책갈피 건너뛰기|DBPROP_BOOKMARKSKIPPED|
|강력한 행 Id|DBPROP_STRONGITDENTITY|
|고유한 행|DBPROP_UNIQUEROWS|
|업데이트 허용|DBPROP_UPDATABILITY|
|책갈피를 사용 하 여|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>명령 동적 속성
 다음 속성에 추가 되는 **명령** 개체의 **속성** 컬렉션입니다.

|ADO 속성 이름|OLE DB 속성 이름|
|-----------------------|--------------------------|
|액세스 순서|DBPROP_ACCESSORDER|
|저장소 개체 차단|DBPROP_BLOCKINGSTORAGEOBJECTS|
|책갈피 유형|DBPROP_BOOKMARKTYPE|
|책갈피를 설정할|DBPROP_IROWSETLOCATE|
|삽입 된 행 변경|DBPROP_CHANGEINSERTEDROWS|
|열 권한|DBPROP_COLUMNRESTRICT|
|열 집합 알림|DBPROP_NOTIFYCOLUMNSET|
|저장소 개체 업데이트 연기|DBPROP_DELAYSTORAGEOBJECTS|
|뒤로 페치|DBPROP_CANFETCHBACKWARDS|
|행 보관|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|부동 행|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|리터럴 책갈피|DBPROP_LITERALBOOKMARKS|
|리터럴 행 Id|DBPROP_LITERALIDENTITY|
|최대 열린 행 수|DBPROP_MAXOPENROWS|
|최대 보류 중인 행|DBPROP_MAXPENDINGROWS|
|최대 행 수|DBPROP_MAXROWS|
|알림 세분성|DBPROP_NOTIFICATIONGRANULARITY|
|알림 단계|DBPROP_NOTIFICATIONPHASES|
|트랜잭션 개체|DBPROP_TRANSACTEDOBJECT|
|내 변경 내용 표시|DBPROP_OWNUPDATEDELETE|
|직접 삽입 표시|DBPROP_OWNINSERT|
|중단 시 유지|DBPROP_ABORTPRESERVE|
|커밋 시 유지|DBPROP_COMMITPRESERVE|
|빠른 다시 시작|DBPROP_QUICKRESTART|
|재진입 이벤트|DBPROP_REENTRANTEVENTS|
|삭제 된 행 제거|DBPROP_REMOVEDELETED|
|여러 변경 내용 보고|DBPROP_REPORTMULTIPLECHANGES|
|보류 중인 삽입 반환|DBPROP_RETURNPENDINGINSERTS|
|행 삭제 알림|DBPROP_NOTIFYROWDELETE|
|행 처음 변경 알림|DBPROP_NOTIFYROWFIRSTCHANGE|
|행 삽입 알림|DBPROP_NOTIFYROWINSERT|
|행 권한|DBPROP_ROWRESTRICT|
|행 다시 동기화 알림|DBPROP_NOTIFYROWRESYNCH|
|행 스레딩 모델|DBPROP_ROWTHREADMODEL|
|행 변경 취소 알림|DBPROP_NOTIFYROWUNDOCHANGE|
|행 삭제 취소 알림|DBPROP_NOTIFYROWUNDODELETE|
|행 삽입 취소 알림|DBPROP_NOTIFYROWUNDOINSERT|
|행 업데이트 알림|DBPROP_NOTIFYROWUPDATE|
|행 집합 페치 위치 변경 알림|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|행 집합 릴리스 알림|DBPROP_NOTIFYROWSETRELEASE|
|뒤로 스크롤|DBPROP_CANSCROLLBACKWARDS|
|삭제 한 책갈피 건너뛰기|DBPROP_BOOKMARKSKIP|
|강력한 행 Id|DBPROP_STRONGIDENTITY|
|업데이트 허용|DBPROP_UPDATABILITY|
|책갈피를 사용 하 여|DBPROP_BOOKMARKS|

 특정 구현 및 ODBC 용 Microsoft OLE DB Provider에 대 한 기능 정보에 대 한 자세한 내용은 참조는 [OLE DB 프로그래머 참조](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) 하거나 MSDN에서 데이터 액세스 및 저장소 개발자 센터 웹 사이트를 방문 하십시오.

## <a name="see-also"></a>관련 항목:
 [개체 (ADO) 명령](../../../ado/reference/ado-api/command-object-ado.md) [CommandText 속성 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [ConnectionString 속성 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [실행 메서드 (ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md) [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md) [Parameters 컬렉션 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md) [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [Provider 속성 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [(ADO) 레코드 집합 개체](../../../ado/reference/ado-api/recordset-object-ado.md) [메서드 지원](../../../ado/reference/ado-api/supports-method.md)
