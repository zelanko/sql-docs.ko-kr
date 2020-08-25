---
description: SQL Server 용 Microsoft OLE DB 공급자 개요
title: SQL Server 용 Microsoft OLE DB 공급자 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for SQL Server
- OLE DB provider for SQL Server [ADO]
- SQLOLEDB [ADO]
ms.assetid: 99bc40c4-9181-4ca1-a06f-9a1a914a0b7b
author: rothja
ms.author: jroth
ms.openlocfilehash: ffb627b0994afbe2b51f946e4ab7dca881e9a9a4
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806552"
---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>SQL Server 용 Microsoft OLE DB 공급자 개요
SQL Server에 대 한 Microsoft OLE DB 공급자 SQLOLEDB를 사용 하면 ADO에서 Microsoft SQL Server에 액세스할 수 있습니다.

> [!IMPORTANT]
> SQLOLEDB (Microsoft OLE DB Provider for SQL Server)는 더 이상 사용 되지 않으며 새로운 개발 작업에 사용 하지 않는 것이 좋습니다. 대신 최신 서버 기능으로 업데이트되는 새로운 [Microsoft OLE DB Driver for SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md)(MSOLEDBSQL)를 사용하세요.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결 하려면 *provider* 인수를 [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) 속성으로 설정 합니다.

```vb
SQLOLEDB
```

 이 값은 [공급자](../../reference/ado-api/provider-property-ado.md) 속성을 사용 하 여 설정 하거나 읽을 수도 있습니다.

## <a name="typical-connection-string"></a>일반 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은 다음과 같습니다.

```vb
"Provider=SQLOLEDB;Data Source=serverName;"
Initial Catalog=databaseName;
User ID=MyUserID;Password=MyPassword;"
```

 문자열은 다음과 같은 키워드로 구성 됩니다.

|키워드|설명|
|-------------|-----------------|
|**공급 기업**|SQL Server에 대 한 OLE DB 공급자를 지정 합니다.|
|**데이터 원본** 또는 **서버**|서버의 이름을 지정합니다.|
|**초기 카탈로그** 또는 **데이터베이스**|서버에 있는 데이터베이스의 이름을 지정 합니다.|
|**사용자 ID** 또는 **uid**|SQL Server 인증에 대 한 사용자 이름을 지정 합니다.|
|**암호** 또는 **pwd**|SQL Server 인증에 대 한 사용자 암호를 지정 합니다.|

> [!NOTE]
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 ID 및 암호 정보 대신 **Trusted_Connection = yes** 또는 **INTEGRATED Security = SSPI** 를 지정 해야 합니다.

## <a name="provider-specific-connection-parameters"></a>공급자별 연결 매개 변수
 공급자는 ADO에 의해 정의 된 매개 변수 외에도 여러 공급자별 연결 매개 변수를 지원 합니다. ADO 연결 속성과 마찬가지로 이러한 공급자별 속성은 [연결](../../reference/ado-api/connection-object-ado.md) 의 [속성](../../reference/ado-api/properties-collection-ado.md) 컬렉션을 통해 설정 하거나 **ConnectionString**의 일부로 설정할 수 있습니다.

|매개 변수|설명|
|---------------|-----------------|
|Trusted_Connection|사용자 인증 모드를 나타냅니다. **예** 또는 **아니요**로 설정할 수 있습니다. 기본값은 **No**입니다. 이 속성이 **예**로 설정 된 경우 SQLOLEDB는 MICROSOFT Windows NT 인증 모드를 사용 하 여 **Location** 및 [Datasource](../../reference/ado-api/datasource-property-ado.md) 속성 값으로 지정 된 SQL Server 데이터베이스에 대 한 사용자 액세스 권한을 부여 합니다. 이 속성이 **아니요**로 설정 된 경우 SQLOLEDB는 혼합 모드를 사용 하 여 SQL Server 데이터베이스에 대 한 사용자 액세스 권한을 부여 합니다. **사용자 Id** **및 암호 속성에** SQL Server 로그인 및 암호가 지정 됩니다.|
|현재 언어|SQL Server 언어 이름을 나타냅니다. 시스템 메시지 선택 및 서식 지정에 사용되는 언어를 식별합니다. 언어가 SQL Server에 설치 되어 있어야 합니다. 그렇지 않으면 연결을 열 수 없습니다.|
|네트워크 주소|**Location** 속성에 지정 된 SQL Server의 네트워크 주소를 나타냅니다.|
|Network Library|SQL Server와 통신 하는 데 사용 되는 네트워크 라이브러리 (DLL)의 이름을 나타냅니다. 이름에는 경로 또는 .dll 파일 확장명이 포함되면 안 됩니다. 기본값은 SQL Server 클라이언트 구성에서 제공 됩니다.|
|준비 절차 사용|**준비** 된 속성에 의해 명령이 준비 될 때 SQL Server 임시 저장 프로시저를 만들지 여부를 결정 합니다.|
|자동 번역|OEM/ANSI 문자를 변환할지 여부를 나타냅니다. 이 속성은 **True** 또는 **False**로 설정할 수 있습니다. 기본값은 **True**입니다. 이 속성이 **True**로 설정 된 경우에는 SQL Server 멀티 바이트 문자열을 검색 하거나 전송 될 때 SQLOLEDB에서 OEM/ANSI 문자 변환을 수행 합니다. 이 속성을 **False**로 설정 하면 SQLOLEDB는 멀티 바이트 문자열 데이터에서 OEM/ANSI 문자 변환을 수행 하지 않습니다.|
|패킷 크기|네트워크 패킷 크기 (바이트)를 나타냅니다. 패킷 크기 속성 값은 512에서 32767 사이 여야 합니다. 기본 SQLOLEDB 네트워크 패킷 크기는 4096입니다.|
|애플리케이션 이름|클라이언트 응용 프로그램 이름을 나타냅니다.|
|워크스테이션 ID|워크스테이션을 식별하는 문자열입니다.|

## <a name="command-object-usage"></a>명령 개체 사용
 SQLOLEDB는 ODBC, ANSI 및 SQL Server 관련 Transact-sql을 유효한 구문으로 amalgam 받아들입니다. 예를 들어 다음 SQL 문은 ODBC SQL 이스케이프 시퀀스를 사용하여 LCASE 문자열 함수를 지정합니다.

```sql
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE는 문자열을 반환하고 모든 대문자를 소문자로 변환합니다. ANSI SQL 문자열 함수 LOWER는 동일한 작업을 수행 하기 때문에 다음 SQL 문은 앞에서 설명한 ODBC 문에 해당 하는 ANSI와 동일 합니다.

```sql
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB는 명령에 대 한 텍스트로 지정 된 경우 문의 형태 중 하나를 성공적으로 처리 합니다.

## <a name="stored-procedures"></a>저장 프로시저
 SQLOLEDB 명령을 사용 하 여 SQL Server 저장 프로시저를 실행 하는 경우 명령 텍스트에서 ODBC 프로시저 호출 이스케이프 시퀀스를 사용 합니다. 그러면 SQLOLEDB는 SQL Server의 원격 프로시저 호출 메커니즘을 사용 하 여 명령 처리를 최적화 합니다. 예를 들어 다음 ODBC SQL 문은 Transact-sql 형식에 대 한 기본 명령 텍스트입니다.

## <a name="odbc-sql"></a>ODBC SQL

```vb
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```sql
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>SQL Server 기능
 SQL Server에서 ADO는 **명령** 입력에 xml을 사용 하 고 **레코드 집합** 개체가 아닌 xml 스트림 형식으로 결과를 검색할 수 있습니다. 자세한 내용은 [명령 입력에 스트림 사용](../data/command-streams.md) 및 [결과 집합을 스트림으로 검색](../data/retrieving-resultsets-into-streams.md)을 참조 하세요.

### <a name="accessing-sql_variant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>MDAC 2.7, MDAC 2.8 또는 Windows DAC 6.0를 사용 하 여 sql_variant 데이터에 액세스
 Microsoft SQL Server에는 **sql_variant**라는 데이터 형식이 있습니다. OLE DB의 **DBTYPE_VARIANT**와 마찬가지로 **sql_variant** 데이터 형식에는 여러 가지 유형의 데이터를 저장할 수 있습니다. 그러나 **DBTYPE_VARIANT** 와 **sql_variant**간에는 몇 가지 중요 한 차이점이 있습니다. 또한 ADO는 **sql_variant** 값으로 저장 된 데이터를 다른 데이터 형식 처리 방법과 다르게 처리 합니다. 다음 목록에서는 **sql_variant**형식의 열에 저장 된 SQL Server 데이터에 액세스할 때 고려해 야 할 문제에 대해 설명 합니다.

-   MDAC 2.7, MDAC 2.8 및 windows DAC (Windows Data Access Components) 6.0에서 SQL Server의 OLE DB 공급자는 **sql_variant** 형식을 지원 합니다. ODBC 용 OLE DB 공급자는 그렇지 않습니다.

-   **Sql_variant** 형식이 **DBTYPE_VARIANT** 데이터 형식과 정확 하 게 일치 하지 않습니다.  **Sql_variant** 유형은 **GUID**, **ANSI** (비유니코드) 문자열 및 **BIGINT**를 비롯 하 여 **DBTYPE_VARIANT** 에서 지원 되지 않는 몇 가지 새 하위 유형을 지원 합니다. 앞에 나열 된 것과 다른 하위 유형을 사용 하면 제대로 작동 합니다.

-   **Sql_variant** 하위 형식 **숫자가** **DBTYPE_DECIMAL** 크기와 일치 하지 않습니다.

-   여러 데이터 형식 강제 변환으로 인해 형식이 일치 하지 않습니다. 예를 들어, **DBTYPE_VARIANT** **GUID** 의 하위 형식으로 **sql_variant** 강제 변환를 사용 하면 **safearray**(바이트)의 하위 유형이 생성 됩니다. 이 형식을 다시 **sql_variant** 으로 변환 하면 **배열의**새 하위 형식 (바이트)이 발생 합니다.

-   **Sql_variant** 데이터를 포함 하는 **레코드 집합** 필드는 **sql_variant** 특정 하위 유형을 포함 하는 경우에만 원격 (마샬링) 또는 지속 될 수 있습니다. 지원 되지 않는 다음 하위 형식으로 원격 또는 데이터를 유지 하려고 시도 하면 Microsoft 지 속성 공급자 (MSPersist): **VT_VARIANT**, **VT_RECORD**, **VT_ILLEGAL**, **VT_UNKNOWN**, **VT_BSTR**및 **VT_DISPATCH** 에서 런타임 오류 (지원 되지 않는 변환)가 발생 합니다.

-   MDAC 2.7, MDAC 2.8 및 Windows DAC 6.0의 SQL Server에 대 한 OLE DB 공급자에는 이름이 암시 하는 것 처럼 **네이티브 변형 허용** 이라는 동적 속성이 있습니다 .이 속성을 사용 하면 개발자는 **DBTYPE_VARIANT**와는 달리 네이티브 형식으로 **sql_variant** 에 액세스할 수 있습니다. 이 속성을 설정 하 고 클라이언트 커서 엔진 (**adUseClient**)을 사용 하 여 **레코드 집합** 을 연 경우에는 **recordset. 열기** 호출이 실패 합니다. 이 속성을 설정 하 고 서버 커서 (**Aduseserver**)를 사용 하 여 **레코드 집합** 을 연 경우에는 **recordset. 열기** 호출이 성공 하지만 **sql_variant** 형식의 열에 액세스 하면 오류가 발생 합니다.

-   MDAC 2.5를 사용 하는 클라이언트 응용 프로그램에서 **sql_variant** 데이터를 Microsoft SQL Server에 대 한 쿼리와 함께 사용할 수 있습니다. 그러나 **sql_variant** 데이터의 값은 문자열로 처리 됩니다. 이러한 클라이언트 응용 프로그램은 MDAC 2.7, MDAC 2.8 또는 Windows DAC 6.0로 업그레이드 해야 합니다.

## <a name="recordset-behavior"></a>레코드 집합 동작
 SQLOLEDB는 SQL Server 커서를 사용 하 여 여러 명령으로 생성 된 다중 결과를 지원할 수 없습니다. 소비자가 SQL Server 커서를 지원 해야 하는 레코드 집합을 요청 하는 경우 사용 된 명령 텍스트에서 단일 레코드 집합을 결과로 생성 하면 오류가 발생 합니다.

 스크롤 가능한 SQLOLEDB 레코드 집합은 SQL Server 커서에서 지원 됩니다. SQL Server는 데이터베이스의 다른 사용자가 변경한 내용에 영향을 주는 커서에 제한을 적용 합니다. 특히 일부 커서의 행은 순서를 지정할 수 없으며 SQL ORDER BY 절이 포함 된 명령을 사용 하 여 레코드 집합을 만들려고 하면 실패할 수 있습니다.

## <a name="dynamic-properties"></a>동적 속성
 SQL Server 용 Microsoft OLE DB 공급자는 열려 있는 [연결](../../reference/ado-api/connection-object-ado.md), [레코드 집합](../../reference/ado-api/recordset-object-ado.md)및 [명령](../../reference/ado-api/command-object-ado.md) 개체의 **properties** 컬렉션에 몇 가지 동적 속성을 삽입 합니다.

 다음 테이블은 각 동적 속성에 대 한 ADO 및 OLE DB 이름의 교차 인덱스입니다. OLE DB 프로그래머 참조는 "설명" 이라는 용어를 통해 ADO 속성 이름을 참조 합니다. 이러한 속성에 대 한 자세한 내용은 OLE DB 프로그래머 참조에서 찾을 수 있습니다. 인덱스에서 OLE DB 속성 이름을 검색 하거나 [부록 C: OLE DB 속성](/previous-versions/windows/desktop/ms723130(v=vs.85))을 참조 하세요.

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
|최대 인덱스 크기|DBPROP_MAXINDEXSIZE|
|최대 행 크기|DBPROP_MAXROWSIZE|
|최대 행 크기에 BLOB 포함|DBPROP_MAXROWSIZEINCLUDESBLOB|
|SELECT의 최대 테이블|DBPROP_MAXTABLESINSELECT|
|여러 매개 변수 집합|DBPROP_MULTIPLEPARAMSETS|
|여러 결과|DBPROP_MULTIPLERESULTS|
|여러 저장소 개체|DBPROP_MULTIPLESTORAGEOBJECTS|
|다중 테이블 업데이트|DBPROP_MULTITABLEUPDATE|
|NULL 데이터 정렬 순서|DBPROP_NULLCOLLATION|
|NULL 연결 동작|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB 버전|DBPROP_PROVIDEROLEDBVER|
|OLE 개체 지원|DBPROP_OLEOBJECTS|
|열 행 집합 지원|DBPROP_OPENROWSETSUPPORT|
|Select 목록의 ORDER BY 열|DBPROP_ORDERBYCOLUMNSINSELECT|
|출력 매개 변수 가용성|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Ref 접근자로 전달|DBPROP_BYREFACCESSORS|
|암호|DBPROP_AUTH_PASSWORD|
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
|명령 제한 시간|DBPROP_COMMANDTIMEOUT|
|열 지연|DBPROP_DEFERRED|
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
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
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
|기타 변경 내용 표시|DBPROP_OTHERUPDATEDELETE|
|다른 사용자 삽입 내용 표시|DBPROP_OTHERINSERT|
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
|서버 커서|DBPROP_SERVERCURSOR|
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
|기본 경로|SSPROP_STREAM_BASEPATH|
|저장소 개체 차단|DBPROP_BLOCKINGSTORAGEOBJECTS|
|책갈피 유형|DBPROP_BOOKMARKTYPE|
|책갈피 가능|DBPROP_IROWSETLOCATE|
|삽입 된 행 변경|DBPROP_CHANGEINSERTEDROWS|
|열 권한|DBPROP_COLUMNRESTRICT|
|열 집합 알림|DBPROP_NOTIFYCOLUMNSET|
|콘텐츠 유형|SSPROP_STREAM_CONTENTTYPE|
|커서 자동 인출|SSPROP_CURSORAUTOFETCH|
|열 지연|DBPROP_DEFERRED|
|지연 준비|SSPROP_DEFERPREPARE|
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
|IRowsetResynch|DBPROP_IRowsetResynch|
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|리터럴 책갈피|DBPROP_LITERALBOOKMARKS|
|리터럴 행 Id|DBPROP_LITERALIDENTITY|
|잠금 모드|DBPROP_LOCKMODE|
|최대 열린 행|DBPROP_MAXOPENROWS|
|최대 보류 중인 행|DBPROP_MAXPENDINGROWS|
|최대 행|DBPROP_MAXROWS|
|알림 세분성|DBPROP_NOTIFICATIONGRANULARITY|
|알림 단계|DBPROP_NOTIFICATIONPHASES|
|트랜잭션 된 개체|DBPROP_TRANSACTEDOBJECT|
|기타 변경 내용 표시|DBPROP_OTHERUPDATEDELETE|
|다른 사용자 삽입 내용 표시|DBPROP_OTHERINSERT|
|출력 인코딩 속성|DBPROP_OUTPUTENCODING|
|출력 스트림 속성|DBPROP_OUTPUTSTREAM|
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
|서버 커서|DBPROP_SERVERCURSOR|
|삽입 시 서버 데이터|DBPROP_SERVERDATAONINSERT|
|삭제 된 책갈피 건너뛰기|DBPROP_BOOKMARKSKIP|
|강력한 행 Id|DBPROP_STRONGIDENTITY|
|업데이트 가능성|DBPROP_UPDATABILITY|
|책갈피 사용|DBPROP_BOOKMARKS|
|XML 루트|SSPROP_STREAM_XMLROOT|
|XSL|SSPROP_STREAM_XSL|

 Microsoft SQL Server OLE DB 공급자에 대 한 특정 구현 세부 정보 및 기능 정보는 [SQL Server 공급자](/previous-versions/windows/desktop/ms720897(v=vs.85))를 참조 하세요.

## <a name="see-also"></a>참고 항목
 [ConnectionString 속성 (ado)](../../reference/ado-api/connectionstring-property-ado.md) [공급자 속성 (](../../reference/ado-api/provider-property-ado.md) Ado) [레코드 집합 개체 (ado)](../../reference/ado-api/recordset-object-ado.md)