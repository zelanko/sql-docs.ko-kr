---
description: ODBC 용 Microsoft OLE DB 공급자 개요
title: ODBC 용 Microsoft OLE DB 공급자 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2dcd280098a5ca4075f424f12b0abdfede6b7653
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806649"
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>ODBC 용 Microsoft OLE DB 공급자 개요
ADO 또는 RDS 프로그래머는 모든 데이터 원본이 OLE DB 인터페이스를 노출 하는 것이 가장 좋습니다. 그러면 ADO에서 데이터 소스를 직접 호출할 수 있습니다. 점점 더 많은 데이터베이스 공급 업체가 OLE DB 인터페이스를 구현 하지만 일부 데이터 원본은 아직 이러한 방식으로 노출 되지 않습니다. 그러나 현재 사용 중인 대부분의 DBMS 시스템은 ODBC를 통해 액세스할 수 있습니다.

 Microsoft Access (Microsoft Jet 데이터베이스 엔진) 및 microsoft FoxPro를 Microsoft SQL Server 비롯 하 여 현재 사용 중인 모든 주요 DBMS에 대해 ODBC 드라이버를 사용할 수 있습니다. 여기에는 Oracle 등의 Microsoft 이외의 데이터베이스 제품도 있습니다.

 그러나 Microsoft ODBC 공급자를 사용 하면 ADO에서 ODBC 데이터 원본에 연결할 수 있습니다. 공급자는 자유 스레드된 및 유니코드를 사용할 수 있습니다.

 공급자는 다른 유형의 트랜잭션 지원 기능을 제공 하지만 다른 DBMS 엔진은 트랜잭션을 지원 합니다. 예를 들어 Microsoft Access는 중첩 된 트랜잭션을 최대 5 수준까지 지원 합니다.

 이는 ADO의 기본 공급자 이며 모든 공급자 종속 ADO 속성 및 메서드가 지원 됩니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결 하려면 [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) 속성의 **provider =** 인수를로 설정 합니다.

```
MSDASQL
```

 [공급자](../../reference/ado-api/provider-property-ado.md) 속성을 읽으면이 문자열도 반환 됩니다.

## <a name="typical-connection-string"></a>일반 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은 다음과 같습니다.

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 문자열은 다음과 같은 키워드로 구성 됩니다.

|키워드|설명|
|-------------|-----------------|
|**공급 기업**|ODBC에 대 한 OLE DB 공급자를 지정 합니다.|
|**DSN**|데이터 원본 이름을 지정 합니다.|
|**UID**|사용자 이름을 지정합니다.|
|**PWD**|사용자 암호를 지정 합니다.|
|**URL**|웹 폴더에 게시 된 파일 또는 디렉터리의 URL을 지정 합니다.|

 이는 ADO의 기본 공급자 이기 때문에 연결 문자열에서 **provider =** 매개 변수를 생략 하면 ADO는이 공급자에 대 한 연결을 설정 하려고 시도 합니다.

> [!NOTE]
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 ID 및 암호 정보 대신 **Trusted_Connection = yes** 또는 **INTEGRATED Security = SSPI** 를 지정 해야 합니다.

 공급자는 ADO에서 정의 된 매개 변수 외에 특정 연결 매개 변수를 지원 하지 않습니다. 그러나 공급자는 ADO가 아닌 연결 매개 변수를 ODBC 드라이버 관리자에 전달 합니다.

 **공급자** 매개 변수를 생략할 수 있으므로 동일한 데이터 원본에 대 한 ODBC 연결 문자열과 동일한 ADO 연결 문자열을 작성할 수 있습니다. ODBC 연결 문자열을 작성할 때와 동일한 매개 변수 이름 (**DRIVER =**, **DATABASE =**, **DSN =** 등), 값 및 구문을 사용 합니다. 미리 정의 된 DSN (데이터 원본 이름) 또는 FileDSN을 사용 하거나 사용 하지 않고 연결할 수 있습니다.

## <a name="syntax-with-a-dsn-or-filedsn"></a>DSN 또는 FileDSN을 사용 하는 구문:

```
"[Provider=MSDASQL;] { DSN=name | FileDSN=filename } ;
[DATABASE=database;] UID=user; PWD=password"
```

## <a name="syntax-without-a-dsn-dsn-less-connection"></a>DSN을 사용 하지 않는 구문 (DSN 없는 연결):

```
"[Provider=MSDASQL;] DRIVER=driver; SERVER=server;
DATABASE=database; UID=MyUserID; PWD=MyPassword"
```

## <a name="remarks"></a>설명
 **DSN** 또는 **filedsn**을 사용 하는 경우 Windows 제어판의 ODBC 데이터 원본 관리자를 통해 정의 해야 합니다. Microsoft Windows 2000에서 ODBC 관리자는 관리 도구 아래에 있습니다. 이전 버전의 Windows에서 ODBC 관리자 아이콘의 이름은 **32 비트 odbc** 또는 **odbc**만 지정 됩니다.

 **DSN**을 설정 하는 대신 ODBC 드라이버 (**드라이버 =**)를 지정할 수 있습니다 (예: "SQL Server;" 서버 이름 (**server =**)). 및 데이터베이스 이름 (**database =**).

 또한 사용자 계정 이름 (**UID =**) 및 사용자 계정에 대 한 암호 (**PWD =**)를 ODBC 관련 매개 변수 또는 표준 ADO 정의 *사용자* 및 *암호* 매개 변수에서 지정할 수 있습니다.

 **Dsn** 정의에서 이미 데이터베이스를 지정 하는 경우에는 **dsn** 외에도 *데이터베이스* 매개 변수 *를 지정 하* 여 다른 데이터베이스에 연결할 수 있습니다. **DSN**을 사용 하는 경우 항상 *데이터베이스* 매개 변수 *를 포함 하* 는 것이 좋습니다. 이렇게 하면 **DSN** 정의를 마지막으로 확인 한 이후 다른 사용자가 기본 데이터베이스 매개 변수를 변경한 경우 올바른 데이터베이스에 연결할 수 있습니다.

## <a name="provider-specific-connection-properties"></a>공급자별 연결 속성
 ODBC 용 OLE DB 공급자는 **연결** 개체의 [properties](../../reference/ado-api/properties-collection-ado.md) 컬렉션에 몇 가지 속성을 추가 합니다. 다음 표에서는 이러한 속성에 해당 하는 OLE DB 속성 이름을 괄호 안에 나열 합니다.

|속성 이름|설명|
|-------------------|-----------------|
|액세스 가능한 프로시저 (KAGPROP_ACCESSIBLEPROCEDURES)|사용자에 게 저장 프로시저에 대 한 액세스 권한이 있는지 여부를 나타냅니다.|
|액세스 가능한 테이블 (KAGPROP_ACCESSIBLETABLES)|사용자에 게 데이터베이스 테이블에 대해 SELECT 문을 실행할 수 있는 권한이 있는지 여부를 나타냅니다.|
|활성 문 (KAGPROP_ACTIVESTATEMENTS)|ODBC 드라이버가 연결에서 지원할 수 있는 핸들 수를 나타냅니다.|
|드라이버 이름 (KAGPROP_DRIVERNAME)|ODBC 드라이버의 파일 이름을 나타냅니다.|
|Driver ODBC 버전 (KAGPROP_DRIVERODBCVER)|이 드라이버에서 지 원하는 ODBC 버전을 나타냅니다.|
|파일 사용 (KAGPROP_FILEUSAGE)|드라이버가 데이터 원본에서 파일을 처리 하는 방법을 나타냅니다. 테이블이 나 카탈로그로|
|Like Escape 절 (KAGPROP_LIKEESCAPECLAUSE)|드라이버가% 문자 (%)의 이스케이프 문자 정의와 사용을 지원 하는지 여부를 나타냅니다. WHERE 절의 LIKE 조건자에서 밑줄 문자 (_)를 표시 합니다.|
|Group By의 최대 열 (KAGPROP_MAXCOLUMNSINGROUPBY)|SELECT 문의 GROUP BY 절에 나열 될 수 있는 최대 열 수를 나타냅니다.|
|인덱스의 최대 열 (KAGPROP_MAXCOLUMNSININDEX)|인덱스에 포함할 수 있는 최대 열 수를 나타냅니다.|
|Order By의 최대 열 (KAGPROP_MAXCOLUMNSINORDERBY)|SELECT 문의 ORDER BY 절에 나열할 수 있는 최대 열 수를 나타냅니다.|
|Select의 최대 열 (KAGPROP_MAXCOLUMNSINSELECT)|SELECT 문의 SELECT 부분에 나열 될 수 있는 최대 열 수를 나타냅니다.|
|테이블의 최대 열 (KAGPROP_MAXCOLUMNSINTABLE)|테이블에 허용 되는 최대 열 수를 나타냅니다.|
|숫자 함수 (KAGPROP_NUMERICFUNCTIONS)|ODBC 드라이버에서 지원 되는 숫자 함수를 나타냅니다. 함수 이름 및이 비트 마스크에서 사용 되는 연결 된 값 목록은 ODBC 설명서에서 [부록 E: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)를 참조 하세요.|
|외부 조인 기능 (KAGPROP_OJCAPABILITY)|공급자가 지 원하는 외부 조인의 유형을 나타냅니다.|
|외부 조인 (KAGPROP_OUTERJOINS)|공급자가 외부 조인을 지원 하는지 여부를 나타냅니다.|
|특수 문자 (KAGPROP_SPECIALCHARACTERS)|ODBC 드라이버에 대 한 특별 한 의미를 갖는 문자를 나타냅니다.|
|저장 프로시저 (KAGPROP_PROCEDURES)|이 ODBC 드라이버에서 저장 프로시저를 사용할 수 있는지 여부를 나타냅니다.|
|문자열 함수 (KAGPROP_STRINGFUNCTIONS)|ODBC 드라이버에서 지원 되는 문자열 함수를 나타냅니다. 함수 이름 및이 비트 마스크에서 사용 되는 연결 된 값 목록은 ODBC 설명서에서 [부록 E: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)를 참조 하세요.|
|시스템 함수 (KAGPROP_SYSTEMFUNCTIONS)|ODBC 드라이버에서 지원 되는 시스템 함수를 나타냅니다. 함수 이름 및이 비트 마스크에서 사용 되는 연결 된 값 목록은 ODBC 설명서에서 [부록 E: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)를 참조 하세요.|
|시간/날짜 함수 (KAGPROP_TIMEDATEFUNCTIONS)|ODBC 드라이버에서 지원 되는 시간 및 날짜 함수를 나타냅니다. 함수 이름 및이 비트 마스크에서 사용 되는 연결 된 값 목록은 ODBC 설명서에서 [부록 E: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)를 참조 하세요.|
|SQL 문법 지원 (KAGPROP_ODBCSQLCONFORMANCE)|ODBC 드라이버가 지 원하는 SQL 문법을 나타냅니다.|

## <a name="provider-specific-recordset-and-command-properties"></a>공급자별 레코드 집합 및 명령 속성
 ODBC 용 OLE DB 공급자는 **레코드 집합** 및 **명령** 개체의 **properties** 컬렉션에 몇 가지 속성을 추가 합니다. 다음 표에서는 이러한 속성에 해당 하는 OLE DB 속성 이름을 괄호 안에 나열 합니다.

|속성 이름|설명|
|-------------------|-----------------|
|쿼리 기반 업데이트/삭제/삽입 (KAGPROP_QUERYBASEDUPDATES)|SQL 쿼리를 사용 하 여 업데이트, 삭제 및 삽입을 수행할 수 있는지 여부를 나타냅니다.|
|ODBC 동시성 유형 (KAGPROP_CONCURRENCY)|두 사용자가 동시에 데이터 소스에서 동일한 데이터에 액세스 하려고 할 때 발생 하는 잠재적인 문제를 줄이는 데 사용 되는 방법을 나타냅니다.|
|앞 으로만 이동 가능한 커서의 BLOB 접근성 (KAGPROP_BLOBSONFOCURSOR)|앞 으로만 이동 가능한 커서를 사용할 때 BLOB **필드** 에 액세스할 수 있는지 여부를 나타냅니다.|
|QBU WHERE 절에 SQL_FLOAT, SQL_DOUBLE 및 SQL_REAL 포함 (KAGPROP_INCLUDENONEXACT)|SQL_FLOAT, SQL_DOUBLE 및 SQL_REAL 값을 QBU WHERE 절에 포함할 수 있는지 여부를 나타냅니다.|
|삽입 후 마지막 행의 위치 (KAGPROP_POSITIONONNEWROW)|테이블에 새 레코드를 삽입 한 후 테이블의 마지막 행이 현재 행으로 이동 함을 나타냅니다.|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO)|**IRowsetChange** 인터페이스가 확장 된 정보 지원을 제공 하는지 여부를 나타냅니다.|
|ODBC 커서 유형 (KAGPROP_CURSOR)|**레코드 집합**에서 사용 하는 커서의 유형을 나타냅니다.|
|마샬링될 수 있는 행 집합 생성 (KAGPROP_MARSHALLABLE)|ODBC 드라이버가 마샬링할 수 있는 레코드 집합을 생성 함을 나타냅니다.|

## <a name="command-text"></a>명령 텍스트
 [명령](../../reference/ado-api/command-object-ado.md) 개체를 사용 하는 방법은 데이터 원본에 따라 달라 지 며, 사용할 쿼리 또는 명령 문의 유형에 따라 달라 집니다.

 ODBC에서는 저장 프로시저를 호출 하기 위한 특정 구문을 제공 합니다. **명령** 개체의 [commandtext](../../reference/ado-api/commandtext-property-ado.md) 속성에 대해 [연결](../../reference/ado-api/connection-object-ado.md) 개체의 **Execute** 메서드에 대 한 *commandtext* 인수 또는 [레코드 집합](../../reference/ado-api/recordset-object-ado.md) 개체의 **Open** 메서드에 대 한 *소스* 인수는 다음 구문을 사용 하 여 문자열을 전달 합니다.

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , ... ]] ) ] }"
```

 **?** [Parameters](../../reference/ado-api/parameters-collection-ado.md) 컬렉션에서 개체를 참조 합니다. 첫 번째 **?** **매개 변수**(0)를 참조 **하** 고 다음을 참조 하십시오. **매개 변수**(1) 등을 참조 합니다.

 매개 변수 참조는 선택 사항이 며 저장 프로시저의 구조에 따라 달라 집니다. 매개 변수를 정의 하지 않는 저장 프로시저를 호출 하려는 경우 문자열은 다음과 같습니다.

```
"{ call procedure }"
```

 두 개의 쿼리 매개 변수가 있는 경우 문자열은 다음과 유사 합니다.

```
"{ call procedure ( ?, ? ) }"
```

 저장 프로시저에서 값을 반환 하면 반환 값은 다른 매개 변수로 처리 됩니다. 쿼리 매개 변수가 없지만 반환 값이 있는 경우 문자열은 다음과 유사 합니다.

```
"{ ? = call procedure }"
```

 마지막으로 반환 값과 두 개의 쿼리 매개 변수가 있는 경우 문자열은 다음과 유사 합니다.

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>레코드 집합 동작
 다음 표에서는이 공급자를 사용 하 여 연 **레코드 집합** 개체에 사용할 수 있는 표준 ADO 메서드 및 속성을 나열 합니다.

 공급자 구성의 **레코드 집합** 동작에 대 한 자세한 내용을 보려면 [Supports](../../reference/ado-api/supports-method.md) 메서드를 실행 하 고 **레코드 집합** 의 **속성** 컬렉션을 열거 하 여 공급자별 동적 속성이 있는지 여부를 확인 합니다.

 표준 ADO **레코드 집합** 속성의 가용성:

|속성|ForwardOnly|동적|Keyset|정적|
|--------------|-----------------|-------------|------------|------------|
|[AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md)|사용할 수 없음|사용할 수 없음|읽기/쓰기|읽기/쓰기|
|[AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md)|사용할 수 없음|사용할 수 없음|읽기/쓰기|읽기/쓰기|
|[ActiveConnection](../../reference/ado-api/activeconnection-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[BOF](../../reference/ado-api/bof-eof-properties-ado.md)|읽기 전용|읽기 전용|읽기 전용|읽기 전용|
|[책갈피](../../reference/ado-api/bookmark-property-ado.md)|사용할 수 없음|사용할 수 없음|읽기/쓰기|읽기/쓰기|
|[CacheSize](../../reference/ado-api/cachesize-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[CursorType](../../reference/ado-api/cursortype-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[EditMode](../../reference/ado-api/editmode-property.md)|읽기 전용|읽기 전용|읽기 전용|읽기 전용|
|[Filter](../../reference/ado-api/filter-property.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[LockType](../../reference/ado-api/locktype-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[MarshalOptions](../../reference/ado-api/marshaloptions-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[Records](../../reference/ado-api/maxrecords-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[PageCount](../../reference/ado-api/pagecount-property-ado.md)|읽기/쓰기|사용할 수 없음|읽기 전용|읽기 전용|
|[PageSize](../../reference/ado-api/pagesize-property-ado.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[RecordCount](../../reference/ado-api/recordcount-property-ado.md)|읽기/쓰기|사용할 수 없음|읽기 전용|읽기 전용|
|[원본](../../reference/ado-api/source-property-ado-recordset.md)|읽기/쓰기|읽기/쓰기|읽기/쓰기|읽기/쓰기|
|[State](../../reference/ado-api/state-property-ado.md)|읽기 전용|읽기 전용|읽기 전용|읽기 전용|
|[상태](../../reference/ado-api/status-property-ado-recordset.md)|읽기 전용|읽기 전용|읽기 전용|읽기 전용|

 [AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md) 및 [ABSOLUTEPAGE](../../reference/ado-api/absolutepage-property-ado.md) 속성은 ADO가 MICROSOFT OLE DB Provider for ODBC의 1.0 버전에서 사용 되는 경우 쓰기 전용입니다.

 표준 ADO **레코드 집합** 메서드의 가용성:

|방법|ForwardOnly|동적|Keyset|정적|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../reference/ado-api/addnew-method-ado.md)|예|예|예|예|
|[취소](../../reference/ado-api/cancel-method-ado.md)|예|예|예|예|
|[CancelBatch](../../reference/ado-api/cancelbatch-method-ado.md)|예|예|예|예|
|[CancelUpdate](../../reference/ado-api/cancelupdate-method-ado.md)|예|예|예|예|
|[복제](../../reference/ado-api/clone-method-ado.md)|아니요|아니요|예|예|
|[닫기](../../reference/ado-api/close-method-ado.md)|예|예|예|예|
|[Delete](../../reference/ado-api/delete-method-ado-recordset.md)|예|예|예|예|
|[GetRows](../../reference/ado-api/getrows-method-ado.md)|예|예|예|예|
|[이동](../../reference/ado-api/move-method-ado.md)|예|예|예|예|
|[MoveFirst](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|예|예|예|예|
|[MoveLast](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|아니요|예|예|예|
|[MoveNext](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|예|예|예|예|
|[MovePrevious](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|아니요|예|예|예|
|[NextRecordset](../../reference/ado-api/nextrecordset-method-ado.md)*|예|예|예|예|
|[열기](../../reference/ado-api/open-method-ado-recordset.md)|예|예|예|예|
|[매크로](../../reference/ado-api/requery-method.md)|예|예|예|예|
|[다시 동기화](../../reference/ado-api/resync-method.md)|아니요|아니요|예|예|
|[지원](../../reference/ado-api/supports-method.md)|예|예|예|예|
|[Update](../../reference/ado-api/update-method.md)|예|예|예|예|
|[UpdateBatch](../../reference/ado-api/updatebatch-method.md)|예|예|예|예|

 * Microsoft Access 데이터베이스에 대해서는 지원 되지 않습니다.

## <a name="dynamic-properties"></a>동적 속성
 ODBC 용 Microsoft OLE DB 공급자는 열려 있는 [연결](../../reference/ado-api/connection-object-ado.md), [레코드 집합](../../reference/ado-api/recordset-object-ado.md)및 [명령](../../reference/ado-api/command-object-ado.md) 개체의 **properties** 컬렉션에 몇 가지 동적 속성을 삽입 합니다.

 다음 테이블은 각 동적 속성에 대 한 ADO 및 OLE DB 이름의 교차 인덱스입니다. OLE DB 프로그래머 참조는 "설명" 이라는 용어로 ADO 속성 이름을 참조 합니다. 이러한 속성에 대 한 자세한 내용은 OLE DB 프로그래머 참조에서 찾을 수 있습니다. 인덱스에서 OLE DB 속성 이름을 검색 하거나 [부록 C: OLE DB 속성](/previous-versions/windows/desktop/ms723130(v=vs.85))을 참조 하세요.

## <a name="connection-dynamic-properties"></a>연결 동적 속성
 다음 속성이 **Connection** 개체의 **properties** 컬렉션에 추가 됩니다.

|ADO 속성 이름|OLE DB 속성 이름|
|-----------------------|--------------------------|
|Active Sessions|DBPROP_ACTIVESESSIONS|
|비동기 가능 Abort|DBPROP_ASYNCTXNABORT|
|비동기 가능 커밋|DBPROP_ASYNCTNXCOMMIT|
|격리 수준 자동 커밋|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|카탈로그 위치|DBPROP_CATALOGLOCATION|
|카탈로그 용어|DBPROP_CATALOGTERM|
|열 정의|DBPROP_COLUMNDEFINITION|
|연결 제한 시간|DBPROP_INIT_TIMEOUT|
|현재 카탈로그|DBPROP_CURRENTCATALOG|
|데이터 원본|DBPROP_INIT_DATASOURCE|
|데이터 원본 이름|DBPROP_DATASOURCENAME|
|데이터 원본 개체 스레딩 모델|DBPROP_DSOTHREADMODEL|
|DBMS 이름|DBPROP_DBMSNAME|
|DBMS 버전|DBPROP_DBMSVER|
|Extended Properties|DBPROP_INIT_PROVIDERSTRING|
|지원 별 그룹화|DBPROP_GROUPBY|
|유형이 다른 테이블 지원|DBPROP_HETEROGENEOUSTABLES|
|식별자 대/소문자 구분|DBPROP_IDENTIFIERCASE|
|초기 카탈로그|DBPROP_INIT_CATALOG|
|격리 수준|DBPROP_SUPPORTEDTXNISOLEVELS|
|격리 보존|DBPROP_SUPPORTEDTXNISORETAIN|
|로캘 ID|DBPROP_INIT_LCID|
|위치|DBPROP_INIT_LOCATION|
|최대 인덱스 크기|DBPROP_MAXINDEXSIZE|
|최대 행 크기|DBPROP_MAXROWSIZE|
|최대 행 크기에 BLOB 포함|DBPROP_MAXROWSIZEINCLUDESBLOB|
|SELECT의 최대 테이블|DBPROP_MAXTABLESINSELECT|
|Mode|DBPROP_INIT_MODE|
|여러 매개 변수 집합|DBPROP_MULTIPLEPARAMSETS|
|여러 결과|DBPROP_MULTIPLERESULTS|
|여러 저장소 개체|DBPROP_MULTIPLESTORAGEOBJECTS|
|다중 테이블 업데이트|DBPROP_MULTITABLEUPDATE|
|NULL 데이터 정렬 순서|DBPROP_NULLCOLLATION|
|NULL 연결 동작|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB 서비스|DBPROP_INIT_OLEDBSERVICES|
|OLE DB 버전|DBPROP_PROVIDEROLEDBVER|
|OLE 개체 지원|DBPROP_OLEOBJECTS|
|열 행 집합 지원|DBPROP_OPENROWSETSUPPORT|
|Select 목록의 ORDER BY 열|DBPROP_ORDERBYCOLUMNSINSELECT|
|출력 매개 변수 가용성|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|암호|DBPROP_AUTH_PASSWORD|
|Ref 접근자로 전달|DBPROP_BYREFACCESSORS|
|보안 정보 유지|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
|영구 ID 유형|DBPROP_PERSISTENTIDTYPE|
|중단 동작 준비|DBPROP_PREPAREABORTBEHAVIOR|
|커밋 동작 준비|DBPROP_PREPARECOMMITBEHAVIOR|
|프로시저 용어|DBPROP_PROCEDURETERM|
|prompt|DBPROP_INIT_PROMPT|
|공급자 이름|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|공급자 버전|DBPROP_PROVIDERVER|
|읽기 전용 데이터 원본|DBPROP_DATASOURCEREADONLY|
|명령에 대 한 행 집합 변환|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|스키마 용어|DBPROP_SCHEMATERM|
|스키마 사용|DBPROP_SCHEMAUSAGE|
|SQL 지원|DBPROP_SQLSUPPORT|
|구조적 저장소|DBPROP_STRUCTUREDSTORAGE|
|하위 쿼리 지원|DBPROP_SUBQUERIES|
|테이블 용어|DBPROP_TABLETERM|
|트랜잭션 DDL|DBPROP_SUPPORTEDTXNDDL|
|사용자 ID|DBPROP_AUTH_USERID|
|사용자 이름|DBPROP_USERNAME|
|창 핸들|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>레코드 집합 동적 속성
 다음 속성이 **레코드 집합** 개체의 **properties** 컬렉션에 추가 됩니다.

|ADO 속성 이름|OLE DB 속성 이름|
|-----------------------|--------------------------|
|액세스 순서|DBPROP_ACCESSORDER|
|저장소 개체 차단|DBPROP_BLOCKINGSTORAGEOBJECTS|
|책갈피 유형|DBPROP_BOOKMARKTYPE|
|책갈피 가능|DBPROP_IROWSETLOCATE|
|삽입 된 행 변경|DBPROP_CHANGEINSERTEDROWS|
|열 권한|DBPROP_COLUMNRESTRICT|
|열 집합 알림|DBPROP_NOTIFYCOLUMNSET|
|저장소 개체 업데이트 지연|DBPROP_DELAYSTORAGEOBJECTS|
|뒤로 인출|DBPROP_CANFETCHBACKWARDS|
|행 유지|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Immobile 행|DBPROP_IMMOBILEROWS|
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
|최대 열린 행|DBPROP_MAXOPENROWS|
|최대 보류 중인 행|DBPROP_MAXPENDINGROWS|
|최대 행|DBPROP_MAXROWS|
|알림 세분성|DBPROP_NOTIFICATIONGRANULARITY|
|알림 단계|DBPROP_NOTIFICATIONPHASES|
|트랜잭션 된 개체|DBPROP_TRANSACTEDOBJECT|
|자체 변경 내용 표시|DBPROP_OWNUPDATEDELETE|
|자체 삽입 표시|DBPROP_OWNINSERT|
|중단 시 유지|DBPROP_ABORTPRESERVE|
|커밋 시 유지|DBPROP_COMMITPRESERVE|
|빠른 다시 시작|DBPROP_QUICKRESTART|
|재진입 이벤트|DBPROP_REENTRANTEVENTS|
|삭제 된 행 제거|DBPROP_REMOVEDELETED|
|여러 변경 내용 보고|DBPROP_REPORTMULTIPLECHANGES|
|보류 중인 삽입 반환|DBPROP_RETURNPENDINGINSERTS|
|행 삭제 알림|DBPROP_NOTIFYROWDELETE|
|행 우선 변경 알림|DBPROP_NOTIFYROWFIRSTCHANGE|
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
|삭제 된 책갈피 건너뛰기|DBPROP_BOOKMARKSKIPPED|
|강력한 행 Id|DBPROP_STRONGITDENTITY|
|고유 행|DBPROP_UNIQUEROWS|
|업데이트 가능성|DBPROP_UPDATABILITY|
|책갈피 사용|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>명령 동적 속성
 다음 속성이 **Command** 개체의 **properties** 컬렉션에 추가 됩니다.

|ADO 속성 이름|OLE DB 속성 이름|
|-----------------------|--------------------------|
|액세스 순서|DBPROP_ACCESSORDER|
|저장소 개체 차단|DBPROP_BLOCKINGSTORAGEOBJECTS|
|책갈피 유형|DBPROP_BOOKMARKTYPE|
|책갈피 가능|DBPROP_IROWSETLOCATE|
|삽입 된 행 변경|DBPROP_CHANGEINSERTEDROWS|
|열 권한|DBPROP_COLUMNRESTRICT|
|열 집합 알림|DBPROP_NOTIFYCOLUMNSET|
|저장소 개체 업데이트 지연|DBPROP_DELAYSTORAGEOBJECTS|
|뒤로 인출|DBPROP_CANFETCHBACKWARDS|
|행 유지|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Immobile 행|DBPROP_IMMOBILEROWS|
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
|최대 열린 행|DBPROP_MAXOPENROWS|
|최대 보류 중인 행|DBPROP_MAXPENDINGROWS|
|최대 행|DBPROP_MAXROWS|
|알림 세분성|DBPROP_NOTIFICATIONGRANULARITY|
|알림 단계|DBPROP_NOTIFICATIONPHASES|
|트랜잭션 된 개체|DBPROP_TRANSACTEDOBJECT|
|자체 변경 내용 표시|DBPROP_OWNUPDATEDELETE|
|자체 삽입 표시|DBPROP_OWNINSERT|
|중단 시 유지|DBPROP_ABORTPRESERVE|
|커밋 시 유지|DBPROP_COMMITPRESERVE|
|빠른 다시 시작|DBPROP_QUICKRESTART|
|재진입 이벤트|DBPROP_REENTRANTEVENTS|
|삭제 된 행 제거|DBPROP_REMOVEDELETED|
|여러 변경 내용 보고|DBPROP_REPORTMULTIPLECHANGES|
|보류 중인 삽입 반환|DBPROP_RETURNPENDINGINSERTS|
|행 삭제 알림|DBPROP_NOTIFYROWDELETE|
|행 우선 변경 알림|DBPROP_NOTIFYROWFIRSTCHANGE|
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
|삭제 된 책갈피 건너뛰기|DBPROP_BOOKMARKSKIP|
|강력한 행 Id|DBPROP_STRONGIDENTITY|
|업데이트 가능성|DBPROP_UPDATABILITY|
|책갈피 사용|DBPROP_BOOKMARKS|

 Microsoft OLE DB Provider for ODBC에 대 한 특정 구현 및 기능 정보에 대 한 자세한 내용은 [OLE DB 프로그래머 참조](/previous-versions/windows/desktop/ms713643(v=vs.85)) 를 참조 하거나 MSDN에서 데이터 액세스 및 저장소 개발자 센터 웹 사이트를 방문 하세요.

## <a name="see-also"></a>참고 항목
 [명령 개체 (](../../reference/ado-api/command-object-ado.md) ado) [CommandText 속성 (](../../reference/ado-api/commandtext-property-ado.md) ado) [연결 개체 (](../../reference/ado-api/connection-object-ado.md) ado) ConnectionString 속성 (ado) [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) 속성 [(ado)](../../reference/ado-api/execute-method-ado-command.md) [Open 메서드 (ado 레코드 집합)](../../reference/ado-api/open-method-ado-recordset.md) [Parameters 컬렉션](../../reference/ado-api/parameters-collection-ado.md) (ado) [속성 컬렉션](../../reference/ado-api/properties-collection-ado.md) (ado) [공급자 속성 (](../../reference/ado-api/provider-property-ado.md) [ado)](../../reference/ado-api/recordset-object-ado.md) [지원 메서드](../../reference/ado-api/supports-method.md)