---
title: Microsoft OLE DB Provider for ODBC | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for ODBC [ADO]
- providers [ADO], OLE DB provider for ODBC
ms.assetid: 2dc0372d-e74d-4d0f-9c8c-04e5a168c148
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fd8374eaa97ffc08528c245569ec7bff8499747a
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701323"
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>Microsoft OLE DB Provider for ODBC 개요
프로그래머는 ADO 또는 RDS 이상적인 환경에 게 모든 데이터 소스를 OLE DB 인터페이스를 노출 한 ADO 데이터 원본으로 직접 호출할 수 있도록 합니다. 점점 더 많은 데이터베이스 공급 업체는 OLE DB 인터페이스를 구현 하지만 일부 데이터 소스는이 이렇게를 아직 노출 되지 않습니다. 그러나 현재 사용 중인 대부분의 DBMS 시스템은 ODBC를 통해 액세스할 수 있습니다.

 ODBC 드라이버는 Oracle과 같은 타사 데이터베이스 제품 외에도 Microsoft SQL Server, Microsoft Access (Microsoft Jet 데이터베이스 엔진) 및 Microsoft FoxPro를 비롯 한 모든 주요 DBMS 현재 사용에서 수 있습니다.

 그러나 Microsoft ODBC 공급자에는 ADO를 모든 ODBC 데이터 원본에 연결할 수 있습니다. 공급자가 자유 스레드 및 유니코드를 사용할 수 있습니다.

 공급자는 서로 다른 DBMS 엔진 다양 한 유형의 트랜잭션 지원 제공 하지만 트랜잭션을 지원 합니다. 예를 들어, Microsoft Access에는 5 개 수준 깊이까지 중첩 된 트랜잭션을 지원합니다.

 ADO에 대 한 기본 공급자 이며 모든 공급자에 종속 된 ADO 속성 및 메서드 지원 됩니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결을 설정 합니다 **공급자 =** 인수를 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성을:

```
MSDASQL
```

 읽기를 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 이 문자열로 반환 됩니다.

## <a name="typical-connection-string"></a>일반적인 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은:

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 문자열을 이러한 키워드 이루어져 있습니다.

|키워드|설명|
|-------------|-----------------|
|**공급자**|ODBC 용 OLE DB 공급자를 지정합니다.|
|**DSN**|데이터 원본 이름을 지정합니다.|
|**UID**|사용자 이름을 지정합니다.|
|**PWD**|사용자 암호를 지정 합니다.|
|**URL**|파일 또는 웹 폴더에 게시 하는 디렉터리의 URL을 지정 합니다.|

 생략 하면 ADO에 대 한 기본 공급자를 이기 때문에 합니다 **공급자 =** ADO 연결 문자열에서 매개 변수는이 공급자에 대 한 연결을 설정 하려고 합니다.

> [!NOTE]
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, **Trusted_Connection = yes** 하거나 **Integrated Security = SSPI** 사용자 ID와 암호 대신 연결 문자열에 대 한 정보입니다.

 공급자는 ADO를 정의한 것 외에도 특정 연결 매개 변수를 지원 하지 않습니다. 그러나 공급자는 ODBC 드라이버 관리자에 게 비 ADO 연결 매개 변수를 전달 합니다.

 생략할 수 있으므로 합니다 **공급자** 매개 변수를 작성할 수 있습니다 따라서 동일한 데이터 원본에 대 한 ODBC 연결 문자열을 동일한 ADO 연결 문자열입니다. 동일한 매개 변수 이름을 사용 하 여 (**드라이버 =** , **데이터베이스 =** 합니다 **DSN =** 등), 값 및 구문으로는 ODBC 연결 문자열을 작성 하는 경우. 미리 정의 된 데이터 원본 이름 (DSN) 또는 FileDSN 없이 사용 하 여 연결할 수 있습니다.

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

## <a name="remarks"></a>Remarks
 사용 하는 경우는 **DSN** 하거나 **FileDSN**, Windows 제어판의 ODBC 데이터 원본 관리자를 통해 정의 되어야 합니다. Microsoft Windows 2000에서 ODBC 관리자 관리 도구 아래에 있습니다. 이전 버전의 Windows에서 ODBC 관리자 아이콘의 이름은 **32 비트 ODBC** 찾아보거나 **ODBC**합니다.

 설정 하는 대신 한 **DSN**, ODBC 드라이버를 지정할 수 있습니다 (**드라이버 =** ), "SQL Server;"와 같은 서버 이름 (**SERVER =** ); 및 데이터베이스 이름을 (**데이터베이스 =** ).

 사용자 계정 이름을 지정할 수도 있습니다 (**UID =** ), 사용자 계정의 암호 (**PWD =** ) 또는 표준 ODBC 관련 매개 변수에서 ADO 정의한 *사용자* 및 *암호* 매개 변수입니다.

 하지만 **DSN** 정의가 이미 데이터베이스를 지정 하는 경우 지정할 수 있습니다 *는* *데이터베이스* 외에 매개 변수를 **DSN** 연결 다른 데이터베이스입니다. 항상 포함 하는 것이 좋습니다 *는* *데이터베이스* 사용 하는 경우 매개 변수를 **DSN**합니다. 마지막으로 확인 되므로 다른 사용자가 기본 데이터베이스 매개 변수를 변경 하는 경우 올바른 데이터베이스에 연결 하는 것이 이렇게 합니다 **DSN** 정의 합니다.

## <a name="provider-specific-connection-properties"></a>공급자별 연결 속성
 여러 속성을 추가 하는 ODBC 용 OLE DB 공급자는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 의 컬렉션을 **연결** 개체입니다. 다음 표에서 해당 OLE DB 속성 이름 괄호로 사용 하 여 이러한 속성을 보여 줍니다.

|속성 이름|Description|
|-------------------|-----------------|
|액세스할 수 있는 절차 (KAGPROP_ACCESSIBLEPROCEDURES)|저장된 프로시저에 대 한 액세스 권한이 있는지 여부를 나타냅니다.|
|액세스 가능한 테이블이 (KAGPROP_ACCESSIBLETABLES)|사용자는 데이터베이스 테이블에 대해 SELECT 문을 실행할 수 있는 권한이 있는지 여부를 나타냅니다.|
|활성 문 (KAGPROP_ACTIVESTATEMENTS)|ODBC 드라이버는 연결에서 지원할 수 있는 핸들의 수를 나타냅니다.|
|드라이버 이름 (KAGPROP_DRIVERNAME)|ODBC 드라이버의 파일 이름을 나타냅니다.|
|드라이버 ODBC 버전 (KAGPROP_DRIVERODBCVER)|이 드라이버를 지 원하는 ODBC의 버전을 나타냅니다.|
|파일 사용량 (KAGPROP_FILEUSAGE)|드라이버 파일을 데이터 원본에서 처리 하는 방법을 나타냅니다. 테이블 또는 카탈로그입니다.|
|Like 이스케이프 절 (KAGPROP_LIKEESCAPECLAUSE)|드라이버 정 및 이스케이프 문자 사용 백분율 문자 (%)에 대 한 지원 하는지 여부를 나타냅니다. 고 WHERE 절에 LIKE 조건자에서 문자 (_) 밑줄을 표시 합니다.|
|Group By (KAGPROP_MAXCOLUMNSINGROUPBY)의 최대 열|SELECT 문의 GROUP BY 절에 나열 될 수 있는 열의 최대 수를 나타냅니다.|
|인덱스 (KAGPROP_MAXCOLUMNSININDEX)의 최대 열|인덱스에 포함 될 수 있는 열의 최대 수를 나타냅니다.|
|Order By (KAGPROP_MAXCOLUMNSINORDERBY)의 최대 열|SELECT 문의 ORDER BY 절에 나열 될 수 있는 열의 최대 수를 나타냅니다.|
|최대 열 선택 (KAGPROP_MAXCOLUMNSINSELECT)|SELECT 문의 SELECT 부분에 나열 될 수 있는 열의 최대 수를 나타냅니다.|
|테이블 (KAGPROP_MAXCOLUMNSINTABLE)의 최대 열|테이블에 허용 되는 열의 최대 수를 나타냅니다.|
|숫자 함수 (KAGPROP_NUMERICFUNCTIONS)|ODBC 드라이버에서 지원 되는 숫자 함수를 나타냅니다. 함수 이름 및이 비트 마스크에 사용 된 연결 된 값의 나열을 참조 하세요. [부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), ODBC 설명서에서.|
|외부 조인 기능 (KAGPROP_OJCAPABILITY)|공급자가 지 원하는 외부 조인 형식을 나타냅니다.|
|외부 조인 (KAGPROP_OUTERJOINS)|공급자 외부 연결을 지원 하는지 여부를 나타냅니다.|
|특수 문자 (KAGPROP_SPECIALCHARACTERS)|ODBC 드라이버에 대 한 특별 한 의미를 가지는 문자를 나타냅니다.|
|저장된 프로시저 (KAGPROP_PROCEDURES)|저장된 프로시저가 ODBC 드라이버를 사용 하 여 사용할 수 있는지 여부를 나타냅니다.|
|문자열 함수 (KAGPROP_STRINGFUNCTIONS)|ODBC 드라이버에서 지원 되는 문자열 함수를 나타냅니다. 함수 이름 및이 비트 마스크에 사용 된 연결 된 값의 나열을 참조 하세요. [부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), ODBC 설명서에서.|
|시스템 함수 (KAGPROP_SYSTEMFUNCTIONS)|ODBC 드라이버에서 지원 되는 시스템 함수를 나타냅니다. 함수 이름 및이 비트 마스크에 사용 된 연결 된 값의 나열을 참조 하세요. [부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), ODBC 설명서에서.|
|날짜/시간 함수 (KAGPROP_TIMEDATEFUNCTIONS)|ODBC 드라이버에서 지원 되는 날짜 및 시간 함수를 나타냅니다. 함수 이름 및이 비트 마스크에 사용 된 연결 된 값의 나열을 참조 하세요. [부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md), ODBC 설명서에서.|
|SQL 문법 지원 (KAGPROP_ODBCSQLCONFORMANCE)|ODBC 드라이버에서 지 원하는 SQL 문법을 나타냅니다.|

## <a name="provider-specific-recordset-and-command-properties"></a>공급자 관련 레코드 집합 및 명령 속성
 여러 속성을 추가 하는 ODBC 용 OLE DB 공급자는 **속성** 의 컬렉션을 **레코드 집합** 및 **명령** 개체입니다. 다음 표에서 해당 OLE DB 속성 이름 괄호로 사용 하 여 이러한 속성을 보여 줍니다.

|속성 이름|Description|
|-------------------|-----------------|
|쿼리 기반 업데이트/삭제/삽입 (KAGPROP_QUERYBASEDUPDATES)|업데이트, 삭제 및 삽입 SQL 쿼리를 사용 하 여 수행할 수 있는지 여부를 나타냅니다.|
|ODBC 동시성 유형을 (KAGPROP_CONCURRENCY)|데이터 원본에서 동시에 동일한 데이터에 액세스 하려고 하는 두 사용자로 인 한 잠재적인 문제를 줄이는 데 사용할 메서드를 나타냅니다.|
|정방향 전용 커서 (KAGPROP_BLOBSONFOCURSOR)에서 BLOB 액세스 가능성|나타냅니다 여부 BLOB **필드** 정방향 전용 커서를 사용 하는 경우에 액세스할 수 있습니다.|
|SQL_FLOAT, 등 SQL_DOUBLE, SQL_REAL QBU WHERE 절 (KAGPROP_INCLUDENONEXACT)에서|SQL_FLOAT, SQL_DOUBLE, 및 SQL_REAL 값 QBU WHERE 절에 포함 될 수 있는지 여부를 나타냅니다.|
|마지막 행 삽입 (KAGPROP_POSITIONONNEWROW) 후에 위치|새 레코드를 테이블에 삽입 한 후 테이블의 마지막 행 수를 나타냅니다. 현재 행을 제공 합니다.|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO)|나타냅니다 여부는 **IRowsetChange** 인터페이스 지원 확장된 정보를 제공 합니다.|
|ODBC 커서 유형 (KAGPROP_CURSOR)|사용 되는 커서의 형식을 나타내는 합니다 **레코드 집합**합니다.|
|마샬링할 수 있는 행 집합을 생성 (KAGPROP_MARSHALLABLE)|마샬링할 수 있는 레코드 집합을 생성 하는 ODBC 드라이버를 나타냅니다.|

## <a name="command-text"></a>명령 텍스트
 사용 하는 방법을 합니다 [명령](../../../ado/reference/ado-api/command-object-ado.md) 주로 데이터 원본에 개체에 종속 되 고 쿼리 또는 명령 문의 유형을 허용 합니다.

 ODBC 저장된 프로시저를 호출 하는 것에 대 한 특정 구문을 제공 합니다. 에 대 한는 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 의 속성을 **명령** 개체를 *CommandText* 인수를를 **Execute** 메서드를를 [ 연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 또는 *원본* 인수를 합니다 **열기** 메서드를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를이 구문 사용 하 여 문자열로 전달:

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , ... ]] ) ] }"
```

 Each **?** 개체를 참조 합니다 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션입니다. 첫 번째 **?** 참조 **매개 변수**(0), 다음 **?** 참조 **매개 변수**(1), 등입니다.

 매개 변수 참조는 선택 사항 및 저장된 프로시저의 구조에 따라 달라 집니다. 매개 변수를 정의 하는 저장된 프로시저를 호출 하려는 경우에 문자열에 다음과 같이 보입니다.

```
"{ call procedure }"
```

 두 개의 매개 변수가 없으면 문자열에는 다음과 같습니다.

```
"{ call procedure ( ?, ? ) }"
```

 저장된 프로시저는 값을 반환 하는 경우 반환 값은 다른 매개 변수로 처리 됩니다. 쿼리 매개 변수가 없는 없지만 반환 값이 있는 경우에 문자열은 다음과 같습니다.

```
"{ ? = call procedure }"
```

 마지막으로, 반환 값이 있는 쿼리 두 매개 변수를 문자열에는 다음과 같습니다.

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>레코드 집합 동작
 다음 표에서 표준 ADO 메서드 및에서 사용할 수 있는 속성을 **레코드 집합** 개체를이 공급자를 사용 하 여 열입니다.

 정보에 대 한 자세한 **레코드 집합** 실행 공급자 구성에 대 한 동작을 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드를 열거 하 고는 **속성** 컬렉션은 **레코드 집합** 공급자별 동적 속성 존재 여부를 확인할 수 있습니다.

 표준 ADO의 사용 가능성 **레코드 집합** 속성:

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
|[Assert](../../../ado/reference/ado-api/filter-property.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|읽기/쓰기|사용할 수 없음|읽기 전용|읽기 전용|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|읽기/쓰기|사용할 수 없음|읽기 전용|읽기 전용|
|[원본](../../../ado/reference/ado-api/source-property-ado-recordset.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[State](../../../ado/reference/ado-api/state-property-ado.md)|읽기 전용|읽기 전용|읽기 전용|읽기 전용|
|[상태](../../../ado/reference/ado-api/status-property-ado-recordset.md)|읽기 전용|읽기 전용|읽기 전용|읽기 전용|

 합니다 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) 하 고 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 속성은 쓰기 전용 ADO ODBC 용 Microsoft OLE DB 공급자의 버전 1.0과 함께 사용 될 때입니다.

 표준 ADO의 사용 가능성 **레코드 집합** 메서드:

|메서드|ForwardOnly|Dynamic|Keyset|정적|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[취소](../../../ado/reference/ado-api/cancel-method-ado.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[복제](../../../ado/reference/ado-api/clone-method-ado.md)|아니요|아니요|예|사용자 계정 컨트롤|
|[닫기](../../../ado/reference/ado-api/close-method-ado.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[이동](../../../ado/reference/ado-api/move-method-ado.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|아니요|예|예|사용자 계정 컨트롤|
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|아니요|예|예|사용자 계정 컨트롤|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)*|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[파일](../../../ado/reference/ado-api/open-method-ado-recordset.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[다시 쿼리](../../../ado/reference/ado-api/requery-method.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[Resync](../../../ado/reference/ado-api/resync-method.md)|아니요|아니요|예|사용자 계정 컨트롤|
|[지원](../../../ado/reference/ado-api/supports-method.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[Update](../../../ado/reference/ado-api/update-method.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|사용자 계정 컨트롤|예|예|사용자 계정 컨트롤|

 * Microsoft Access 데이터베이스에 대 한 지원 되지 않습니다.

## <a name="dynamic-properties"></a>동적 속성
 Microsoft OLE DB Provider for ODBC에 여러 동적 속성을 삽입 합니다 **속성** 컬렉션을 아직 열지 않은 [연결](../../../ado/reference/ado-api/connection-object-ado.md), [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 및 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다.

 다음 테이블은 각 동적 속성에 대 한 OLE DB 및 ADO 이름의 상호는 인덱스입니다. OLE DB 프로그래머 참조 이름을 참조 하는 ADO 속성 라는 용어로, "Description"로 지정 합니다. OLE DB 프로그래머 참조에서 이러한 속성에 대 한 자세한 정보를 찾을 수 있습니다. 인덱스의 OLE DB 속성 이름을 검색 하거나 참조 [부록 c: OLE DB 속성](https://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292)합니다.

## <a name="connection-dynamic-properties"></a>연결의 동적 속성
 에 다음 속성을 추가 합니다 **연결** 개체의 **속성** 컬렉션입니다.

|ADO 속성 이름|OLE DB 속성 이름|
|-----------------------|--------------------------|
|Active Sessions|DBPROP_ACTIVESESSIONS|
|비동기 가능 중단|DBPROP_ASYNCTXNABORT|
|비동기 가능 커밋|DBPROP_ASYNCTNXCOMMIT|
|격리 수준 자동 커밋|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|카탈로그 위치|DBPROP_CATALOGLOCATION|
|카탈로그 용어|DBPROP_CATALOGTERM|
|열 정의|DBPROP_COLUMNDEFINITION|
|연결 제한 시간|DBPROP_INIT_TIMEOUT|
|현재 카탈로그|DBPROP_CURRENTCATALOG|
|데이터 원본|DBPROP_INIT_DATASOURCE|
|Data Source Name|DBPROP_DATASOURCENAME|
|데이터 소스 개체 스레딩 모델|DBPROP_DSOTHREADMODEL|
|DBMS 이름|DBPROP_DBMSNAME|
|DBMS 버전|DBPROP_DBMSVER|
|확장 속성|DBPROP_INIT_PROVIDERSTRING|
|GROUP BY 지원|DBPROP_GROUPBY|
|유형이 다른 테이블 지원|DBPROP_HETEROGENEOUSTABLES|
|식별자 대/소문자 구분|DBPROP_IDENTIFIERCASE|
|Initial Catalog|DBPROP_INIT_CATALOG|
|격리 수준|DBPROP_SUPPORTEDTXNISOLEVELS|
|격리 보존|DBPROP_SUPPORTEDTXNISORETAIN|
|로캘 ID|DBPROP_INIT_LCID|
|위치|DBPROP_INIT_LOCATION|
|최대 인덱스 크기|DBPROP_MAXINDEXSIZE|
|최대 행 크기|DBPROP_MAXROWSIZE|
|BLOB 포함 최대 행 크기|DBPROP_MAXROWSIZEINCLUDESBLOB|
|SELECT의 최대 테이블|DBPROP_MAXTABLESINSELECT|
|모드|DBPROP_INIT_MODE|
|여러 매개 변수 집합|DBPROP_MULTIPLEPARAMSETS|
|여러 결과|DBPROP_MULTIPLERESULTS|
|여러 저장소 개체|DBPROP_MULTIPLESTORAGEOBJECTS|
|여러 테이블 업데이트|DBPROP_MULTITABLEUPDATE|
|NULL 정렬 순서|DBPROP_NULLCOLLATION|
|NULL 연결 동작|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB 서비스|DBPROP_INIT_OLEDBSERVICES|
|OLE DB 버전|DBPROP_PROVIDEROLEDBVER|
|OLE 개체 지원|DBPROP_OLEOBJECTS|
|행 집합 열기 지원|DBPROP_OPENROWSETSUPPORT|
|선택 목록의 열을 기준으로 정렬|DBPROP_ORDERBYCOLUMNSINSELECT|
|출력 매개 변수 가용성|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|암호|DBPROP_AUTH_PASSWORD|
|Ref 접근자로 전달|DBPROP_BYREFACCESSORS|
|Persist Security Info|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
|영구 ID 형식|DBPROP_PERSISTENTIDTYPE|
|중단 동작 준비|DBPROP_PREPAREABORTBEHAVIOR|
|커밋 동작 준비|DBPROP_PREPARECOMMITBEHAVIOR|
|프로시저 용어|DBPROP_PROCEDURETERM|
|프롬프트|DBPROP_INIT_PROMPT|
|공급자 이름|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|공급자 버전|DBPROP_PROVIDERVER|
|읽기 전용 데이터 원본|DBPROP_DATASOURCEREADONLY|
|명령 시 행 집합 변환|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|스키마 용어|DBPROP_SCHEMATERM|
|스키마 사용|DBPROP_SCHEMAUSAGE|
|SQL 지원|DBPROP_SQLSUPPORT|
|구조적된 저장소|DBPROP_STRUCTUREDSTORAGE|
|하위 쿼리 지원|DBPROP_SUBQUERIES|
|테이블 용어|DBPROP_TABLETERM|
|트랜잭션 DDL|DBPROP_SUPPORTEDTXNDDL|
|User ID|DBPROP_AUTH_USERID|
|사용자 이름|DBPROP_USERNAME|
|창 핸들|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>레코드 집합 동적 속성
 에 다음 속성을 추가 합니다 **레코드 집합** 개체의 **속성** 컬렉션입니다.

|ADO 속성 이름|OLE DB 속성 이름|
|-----------------------|--------------------------|
|액세스 순서|DBPROP_ACCESSORDER|
|저장소 개체 차단|DBPROP_BLOCKINGSTORAGEOBJECTS|
|책갈피 형식|DBPROP_BOOKMARKTYPE|
|책갈피를 설정할|DBPROP_IROWSETLOCATE|
|삽입된 행 변경|DBPROP_CHANGEINSERTEDROWS|
|열 권한|DBPROP_COLUMNRESTRICT|
|열 설정 알림|DBPROP_NOTIFYCOLUMNSET|
|저장소 개체 업데이트 연기|DBPROP_DELAYSTORAGEOBJECTS|
|뒤로 페치|DBPROP_CANFETCHBACKWARDS|
|행 고정|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Immobile Rows|DBPROP_IMMOBILEROWS|
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
|알림 단위|DBPROP_NOTIFICATIONGRANULARITY|
|알림 단계|DBPROP_NOTIFICATIONPHASES|
|트랜잭션 개체|DBPROP_TRANSACTEDOBJECT|
|내 변경 내용 표시|DBPROP_OWNUPDATEDELETE|
|내 삽입 내용 표시|DBPROP_OWNINSERT|
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
|책갈피 사용|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>명령 동적 속성
 에 다음 속성을 추가 합니다 **명령** 개체의 **속성** 컬렉션입니다.

|ADO 속성 이름|OLE DB 속성 이름|
|-----------------------|--------------------------|
|액세스 순서|DBPROP_ACCESSORDER|
|저장소 개체 차단|DBPROP_BLOCKINGSTORAGEOBJECTS|
|책갈피 형식|DBPROP_BOOKMARKTYPE|
|책갈피를 설정할|DBPROP_IROWSETLOCATE|
|삽입된 행 변경|DBPROP_CHANGEINSERTEDROWS|
|열 권한|DBPROP_COLUMNRESTRICT|
|열 설정 알림|DBPROP_NOTIFYCOLUMNSET|
|저장소 개체 업데이트 연기|DBPROP_DELAYSTORAGEOBJECTS|
|뒤로 페치|DBPROP_CANFETCHBACKWARDS|
|행 고정|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Immobile Rows|DBPROP_IMMOBILEROWS|
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
|알림 단위|DBPROP_NOTIFICATIONGRANULARITY|
|알림 단계|DBPROP_NOTIFICATIONPHASES|
|트랜잭션 개체|DBPROP_TRANSACTEDOBJECT|
|내 변경 내용 표시|DBPROP_OWNUPDATEDELETE|
|내 삽입 내용 표시|DBPROP_OWNINSERT|
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
|책갈피 사용|DBPROP_BOOKMARKS|

 특정 구현 기능에 대 한 정보와 Microsoft OLE DB Provider for ODBC에 대 한 자세한 내용은 참조는 [OLE DB Programmer's Reference](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8) 하거나 MSDN에서 Data Access and Storage Developer Center 웹 사이트를 방문 합니다.

## <a name="see-also"></a>관련 항목
 [개체 (ADO)를 명령](../../../ado/reference/ado-api/command-object-ado.md) [CommandText 속성 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [ConnectionString 속성 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [실행 메서드 (ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md) [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md) [Parameters 컬렉션 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md) [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [공급자 속성 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [메서드 지원](../../../ado/reference/ado-api/supports-method.md)
