---
title: Microsoft OLE DB Provider for SQL Server | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for SQL Server
- OLE DB provider for SQL Server [ADO]
- SQLOLEDB [ADO]
ms.assetid: 99bc40c4-9181-4ca1-a06f-9a1a914a0b7b
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41eae162370ed26a1d84428f1c4e6a5d7eb5e2c7
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980695"
---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>Microsoft OLE DB Provider for SQL Server 개요
Microsoft OLE DB Provider for SQL Server는 SQLOLEDB 통해 Microsoft SQL Server에 액세스 하는 ADO를 수 있습니다.

**참고:** 새로운 개발에 대 한이 드라이버를 사용 하는 것은 권장 되지 않습니다. 새 OLE DB 공급자가 호출 된 [Microsoft OLE DB Driver for SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) 앞으로 최신 서버 기능을 사용 하 여 업데이트 됩니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결을 설정 합니다 *공급자* 인수를 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성을:

```
SQLOLEDB
```

 이 값을 설정 하거나 사용 하 여 읽을 수도 있습니다는 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성입니다.

## <a name="typical-connection-string"></a>일반적인 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은:

```
"Provider=SQLOLEDB;Data Source=serverName;"
Initial Catalog=databaseName;
User ID=MyUserID;Password=MyPassword;"
```

 문자열을 이러한 키워드 이루어져 있습니다.

|키워드|Description|
|-------------|-----------------|
|**공급자**|OLE DB Provider for SQL Server 지정합니다.|
|**데이터 원본** 또는 **서버**|서버의 이름을 지정합니다.|
|**초기 카탈로그** 또는 **데이터베이스**|서버에서 데이터베이스의 이름을 지정합니다.|
|**사용자 ID** 또는 **uid**|(SQL Server 인증)에 대 한 사용자 이름을 지정합니다.|
|**암호** 또는 **pwd**|사용자 암호를 지정 합니다 (SQL Server 인증).|

> [!NOTE]
>  지정 해야 하는 경우 Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는, **Trusted_Connection = yes** 하거나 **Integrated Security = SSPI** 사용자 ID와 암호 대신 연결 문자열에 대 한 정보입니다.

## <a name="provider-specific-connection-parameters"></a>공급자별 연결 매개 변수
 공급자는 ADO를 정의한 것 외에도 여러 공급자별 연결 매개 변수를 지원 합니다. 으로 ADO 연결 속성을 이러한 공급자별 속성을 통해 설정할 수 있습니다 합니다 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 의 컬렉션을 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 의 일부로 설정할 수 있습니다는 **ConnectionString**.

|매개 변수|Description|
|---------------|-----------------|
|Trusted_Connection|사용자 인증 모드를 나타냅니다. 설정할 수 있습니다 **Yes** 또는 **No**합니다. 기본값은 **No**합니다. 이 속성 설정 된 경우 **예**, SQLOLEDB Microsoft Windows NT 인증 모드를 사용 하 여 지정한 SQL Server 데이터베이스에 대 한 사용자 액세스 권한을 부여 하는 **위치** 고 [데이터 원본 ](../../../ado/reference/ado-api/datasource-property-ado.md) 속성 값입니다. 이 속성 설정 된 경우 **No**, SQLOLEDB 혼합 모드를 사용 하 여 SQL Server 데이터베이스에 대 한 사용자 액세스 권한을 부여 합니다. 에 지정 된 SQL Server 로그인 및 암호를 **사용자 Id** 하 고 **암호** 속성입니다.|
|현재 언어|SQL Server 언어 이름을 나타냅니다. 시스템 메시지 선택 및 서식 지정에 사용되는 언어를 식별합니다. 언어를 SQL Server에 설치 해야이 고 그렇지 열기 연결이 실패 합니다.|
|네트워크 주소|지정 된 SQL Server의 네트워크 주소를 나타내는 합니다 **위치** 속성입니다.|
|네트워크 라이브러리|SQL Server와 통신 하는 데 사용 하는 네트워크 라이브러리 (DLL)의 이름을 나타냅니다. 이름에는 경로 또는 .dll 파일 확장명이 포함되면 안 됩니다. SQL Server 클라이언트 구성에서 기본 제공 됩니다.|
|준비 절차 사용|SQL Server 명령을 준비 하는 경우 임시 저장된 프로시저를 만드는 지 여부를 결정 (여는 **Prepared** 속성).|
|자동 변환|OEM/ANSI 문자로 변환 되는지 여부를 나타냅니다. 이 속성 설정할 수 있습니다 **True** 하거나 **False**합니다. 기본값은 **True**입니다. 이 속성 설정 된 경우 **True**, SQLOLEDB는 멀티 바이트 문자 문자열에서 검색 되거나 SQL Server에 전송 되는 경우 OEM/ANSI 문자 변환을 수행 합니다. 이 속성 설정 된 경우 **False**, SQLOLEDB 멀티 바이트 문자 문자열 데이터에서 OEM/ANSI 문자 변환을 수행 하지 않습니다.|
|패킷 크기|네트워크 패킷 크기를 (바이트) 나타냅니다. 패킷 크기 속성 값은 512에서 32767 사이 여야 합니다. 기본 SQLOLEDB 네트워크 패킷 크기는 4096입니다.|
|Application Name|클라이언트 응용 프로그램 이름을 나타냅니다.|
|워크스테이션 ID|워크스테이션을 식별하는 문자열입니다.|

## <a name="command-object-usage"></a>명령 개체 사용
 SQLOLEDB는 ODBC, ANSI 및 SQL Server 관련 TRANSACT-SQL으로 이루어져 유효한 구문으로 허용합니다. 예를 들어 다음 SQL 문은 ODBC SQL 이스케이프 시퀀스를 사용하여 LCASE 문자열 함수를 지정합니다.

```
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE는 문자열을 반환하고 모든 대문자를 소문자로 변환합니다. ANSI SQL 문자열 함수 LOWER SQL 문 앞에서 살펴보았던 ODBC 문에 해당 하는 ANSI 이므로 동일한 작업을 수행 합니다.

```
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB 명령 텍스트로 지정 하는 경우 문의 형식 중 하나를 성공적으로 처리 합니다.

## <a name="stored-procedures"></a>저장 프로시저
 SQL Server 저장 프로시저 실행 시 SQLOLEDB 명령을 사용 하 여, 명령 텍스트에 ODBC 프로시저 호출 이스케이프 시퀀스를 사용 합니다. 다음 SQLOLEDB SQL Server의 원격 프로시저 호출 메커니즘을 사용 하 여 명령 처리를 최적화 합니다. 예를 들어, 다음 ODBC SQL 문은 TRANSACT-SQL 폼 스타일러스가 기본 명령 텍스트:

## <a name="odbc-sql"></a>ODBC SQL

```
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>SQL Server 기능
 SQL Server와 함께 ADO에 대 한 XML을 사용할 수 **명령** 입력 및 검색 결과를 XML 스트림 형식 대신 **Recordset** 개체입니다. 자세한 내용은 참조 하세요. [사용 하 여 명령 입력 스트림을](../../../ado/guide/data/command-streams.md) 및 [스트림을에 결과 집합 검색](../../../ado/guide/data/retrieving-resultsets-into-streams.md)합니다.

### <a name="accessing-sqlvariant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>MDAC 2.7, MDAC 2.8 또는 Windows DAC 6.0을 사용 하 여 sql_variant 데이터 액세스
 Microsoft SQL Server 데이터 형식이 호출 **sql_variant**합니다. OLE DB의 비슷합니다 **DBTYPE_VARIANT**서 **sql_variant** 데이터 형식은 여러 종류의 데이터를 저장할 수 있습니다. 그러나 간의 주요 차이점을 몇 가지 **DBTYPE_VARIANT** 하 고 **sql_variant**합니다. ADO는도로 저장 된 데이터 처리를 **sql_variant** 다른 데이터 형식을 처리 하는 방법을 다른 방식으로 값입니다. 다음 목록에서는 형식의 열에 저장 된 SQL Server 데이터에 액세스할 때 고려해 야 할 문제 **sql_variant**합니다.

-   MDAC 2.7, MDAC 2.8 및 Windows Data Access Components (Windows DAC) 6.0에서 OLE DB Provider for SQL Server를 지원 합니다 **sql_variant** 형식입니다. OLE DB Provider for ODBC 그렇지 않습니다.

-   합니다 **sql_variant** 형식이 정확히 일치 하지 않는 합니다 **DBTYPE_VARIANT** 데이터 형식입니다.  **sql_variant** 형식에서 지원 되지 않습니다 하는 몇 가지 새로운 하위 유형이 지원 **DBTYPE_VARIANT,** 포함 하 여 **GUID**하십시오 **ANSI** (비유니코드) 문자열 및 **BIGINT**합니다. 이외의 하위 형식을 사용 하 여 이전에 나열 된 올바르게 작동 합니다.

-   합니다 **sql_variant** 하위 **숫자** 일치 하지 않습니다는 **DBTYPE_DECIMAL** 크기에서입니다.

-   일치 하지 않는 형식에서 여러 데이터 형식 강제 변환 됩니다. 예를 들어 강제 변환를 **sql_variant** 의 하위 형식을 사용 하 여 **GUID** 에 **DBTYPE_VARIANT** 의 하위 형식에 발생 합니다 **safearray**(바이트) . 이 형식으로 변환 된 **sql_variant** 의 새 하위 하면 **배열**(바이트).

-   **레코드 집합** 포함 된 필드 **sql_variant** 데이터를 원격으로 연결할 수 (마샬링) 또는 경우에만 유지 합니다 **sql_variant** 특정 하위 유형이 포함 합니다. 원격 지원 되지 않는 다음을 사용 하 여 데이터를 유지 하거나 하위 하면 런타임 오류가 발생 (지원 되지 않는 변환) Microsoft 지 속성 공급자 (MSPersist)에서: **VT_VARIANT**, **VT_RECORD**, **VT_ILLEGAL**합니다 **VT_UNKNOWN**를 **VT_BSTR**, 및 **VT_DISPATCH 합니다.**

-   OLE DB Provider for SQL Server MDAC 2.7, MDAC 2.8 및 Windows DAC 6.0 속성이 동적 호출 **네이티브 변형을 허용** , 이름에서 알 수 있듯이 허용 하는 개발자가 액세스할 수 합니다 **sql_variant** 에서 와 반대로 해당 네이티브 형식에 **DBTYPE_VARIANT**합니다. 이 속성을 설정 하는 경우 **Recordset** Client Cursor Engine을 사용 하 여 열릴 (**adUseClient**), **Recordset.Open** 호출 하지 못합니다. 이 속성을 설정 하는 경우 **Recordset** 서버 커서를 사용 하 여 열릴 (**가 adUseServer**), **Recordset.Open** 호출이 성공 한다는 형식의열에액세스하지만**sql_variant** 오류가 생성 됩니다.

-   MDAC 2.5를 사용 하는 클라이언트 응용 프로그램에서 **sql_variant** Microsoft SQL Server에 대 한 쿼리를 사용 하 여 데이터를 사용할 수 있습니다. 그러나 값을 **sql_variant** 데이터 문자열로 처리 됩니다. 이러한 클라이언트 응용 프로그램 MDAC 2.7, MDAC 2.8 또는 Windows DAC 6.0 업그레이드 해야 합니다.

## <a name="recordset-behavior"></a>레코드 집합 동작
 SQLOLEDB는 많은 명령을 통해 생성 된 여러 결과 지원 하기 위해 SQL Server 커서를 사용할 수 없습니다. SQL Server 커서 지원을 요구 하면서 레코드 집합을 요청 하는 소비자를 사용 하는 명령 텍스트를 해당 결과로 단일 레코드 집합 보다 많은 생성 하는 경우는 오류가 발생 합니다.

 SQLOLEDB 레코드 집합을 스크롤할 수 있는 SQL Server 커서에서 지원 됩니다. SQL Server 데이터베이스의 다른 사용자가 변경한 내용의 영향을 받는 커서에 제한이 있습니다. 특히 일부 커서의 행을 정렬할 수 없습니다 및 SQL ORDER BY 절을 포함 하는 명령을 사용 하 여 레코드 집합을 만들려고 시도 실패할 수 있습니다.

## <a name="dynamic-properties"></a>동적 속성
 Microsoft OLE DB Provider for SQL Server에 여러 동적 속성을 삽입 합니다 **속성** 를 아직 열지 않은 컬렉션 [연결](../../../ado/reference/ado-api/connection-object-ado.md), [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 및 [ 명령](../../../ado/reference/ado-api/command-object-ado.md) 개체입니다.

 다음 테이블은 각 동적 속성에 대 한 OLE DB 및 ADO 이름의 상호는 인덱스입니다. OLE DB 프로그래머 참조 이름을 참조 하는 ADO 속성 "설명 합니다." 라는 용어로 OLE DB 프로그래머 참조에서 이러한 속성에 대 한 자세한 정보를 찾을 수 있습니다. 인덱스의 OLE DB 속성 이름을 검색 하거나 참조 [부록 c: OLE DB 속성](http://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292)합니다.

## <a name="connection-dynamic-properties"></a>연결의 동적 속성
 다음 속성에 추가 됩니다는 **속성** 의 컬렉션을 **연결** 개체입니다.

|ADO 속성 이름|OLE DB 속성 이름|
|-----------------------|--------------------------|
|Active Sessions|DBPROP_ACTIVESESSIONS|
|비동기 가능 중단|DBPROP_ASYNCTXNABORT|
|비동기 가능 커밋|DBPROP_ASYNCTNXCOMMIT|
|격리 수준 자동 커밋|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|카탈로그 위치|DBPROP_CATALOGLOCATION과 같습니다|
|카탈로그 용어|DBPROP_CATALOGTERM|
|열 정의|DBPROP_COLUMNDEFINITION|
|연결 제한 시간|DBPROP_INIT_TIMEOUT|
|현재 카탈로그|DBPROP_CURRENTCATALOG|
|데이터 원본|DBPROP_INIT_DATASOURCE|
|Data Source Name|DBPROP_DATASOURCENAME|
|데이터 소스 개체 스레딩 모델|DBPROP_DSOTHREADMODEL|
|DBMS 이름|DBPROP_DBMSNAME|
|DBMS 버전|DBPROP_DBMSVER|
|Extended Properties|DBPROP_INIT_PROVIDERSTRING|
|GROUP BY 지원|DBPROP_GROUPBY와 같습니다|
|유형이 다른 테이블 지원|DBPROP_HETEROGENEOUSTABLES와 같습니다|
|식별자 대/소문자 구분|DBPROP_IDENTIFIERCASE|
|초기 카탈로그|DBPROP_INIT_CATALOG|
|격리 수준|DBPROP_SUPPORTEDTXNISOLEVELS|
|격리 보존|DBPROP_SUPPORTEDTXNISORETAIN|
|로캘 ID|DBPROP_INIT_LCID|
|최대 인덱스 크기|DBPROP_MAXINDEXSIZE와 같습니다|
|최대 행 크기|DBPROP_MAXROWSIZE와 같습니다|
|BLOB 포함 최대 행 크기|DBPROP_MAXROWSIZEINCLUDESBLOB|
|SELECT의 최대 테이블|DBPROP_MAXTABLESINSELECT|
|여러 매개 변수 집합|DBPROP_MULTIPLEPARAMSETS|
|여러 결과|DBPROP_MULTIPLERESULTS|
|여러 저장소 개체|DBPROP_MULTIPLESTORAGEOBJECTS|
|여러 테이블 업데이트|DBPROP_MULTITABLEUPDATE|
|NULL 정렬 순서|DBPROP_NULLCOLLATION과 같습니다|
|NULL 연결 동작|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB 버전|DBPROP_PROVIDEROLEDBVER|
|OLE 개체 지원|DBPROP_OLEOBJECTS|
|행 집합 열기 지원|DBPROP_OPENROWSETSUPPORT|
|선택 목록의 열을 기준으로 정렬|DBPROP_ORDERBYCOLUMNSINSELECT|
|출력 매개 변수 가용성|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Ref 접근자로 전달|DBPROP_BYREFACCESSORS|
|암호|DBPROP_AUTH_PASSWORD|
|보안 정보 유지|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
|영구 ID 형식|DBPROP_PERSISTENTIDTYPE|
|중단 동작 준비|DBPROP_PREPAREABORTBEHAVIOR와 같습니다|
|커밋 동작 준비|DBPROP_PREPARECOMMITBEHAVIOR와 같습니다|
|프로시저 용어|DBPROP_PROCEDURETERM|
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
 다음 속성에 추가 됩니다는 **속성** 의 컬렉션을 **레코드 집합** 개체입니다.

|ADO 속성 이름|OLE DB 속성 이름|
|-----------------------|--------------------------|
|액세스 순서|DBPROP_ACCESSORDER|
|저장소 개체 차단|DBPROP_BLOCKINGSTORAGEOBJECTS|
|책갈피 형식|DBPROP_BOOKMARKTYPE|
|책갈피를 설정할|DBPROP_IROWSETLOCATE|
|삽입된 행 변경|DBPROP_CHANGEINSERTEDROWS|
|열 권한|DBPROP_COLUMNRESTRICT|
|열 설정 알림|DBPROP_NOTIFYCOLUMNSET|
|명령 시간 제한|DBPROP_COMMANDTIMEOUT|
|열 지연|DBPROP_DEFERRED|
|저장소 개체 업데이트 연기|DBPROP_DELAYSTORAGEOBJECTS|
|뒤로 페치|DBPROP_CANFETCHBACKWARDS|
|행 고정|DBPROP_CANHOLDROWS|
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
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
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
|다른 사용자 변경 내용 표시|DBPROP_OTHERUPDATEDELETE|
|다른 사용자 삽입 내용 표시|DBPROP_OTHERINSERT|
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
|서버 커서|DBPROP_SERVERCURSOR|
|삭제 한 책갈피 건너뛰기|DBPROP_BOOKMARKSKIPPED|
|강력한 행 Id|DBPROP_STRONGITDENTITY|
|고유한 행|DBPROP_UNIQUEROWS|
|업데이트 허용|DBPROP_UPDATABILITY|
|책갈피 사용|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>명령 동적 속성
 다음 속성에 추가 됩니다는 **속성** 의 컬렉션을 **명령** 개체입니다.

|ADO 속성 이름|OLE DB 속성 이름|
|-----------------------|--------------------------|
|액세스 순서|DBPROP_ACCESSORDER|
|기본 경로|SSPROP_STREAM_BASEPATH|
|저장소 개체 차단|DBPROP_BLOCKINGSTORAGEOBJECTS|
|책갈피 형식|DBPROP_BOOKMARKTYPE|
|책갈피를 설정할|DBPROP_IROWSETLOCATE|
|삽입된 행 변경|DBPROP_CHANGEINSERTEDROWS|
|열 권한|DBPROP_COLUMNRESTRICT|
|열 설정 알림|DBPROP_NOTIFYCOLUMNSET|
|내용 유형|SSPROP_STREAM_CONTENTTYPE|
|커서 자동 인출|SSPROP_CURSORAUTOFETCH|
|열 지연|DBPROP_DEFERRED|
|지연 준비|SSPROP_DEFERPREPARE|
|저장소 개체 업데이트 연기|DBPROP_DELAYSTORAGEOBJECTS|
|뒤로 페치|DBPROP_CANFETCHBACKWARDS|
|행 고정|DBPROP_CANHOLDROWS|
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
|IRowsetResynch|DBPROP_IRowsetResynch|
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|리터럴 책갈피|DBPROP_LITERALBOOKMARKS|
|리터럴 행 Id|DBPROP_LITERALIDENTITY|
|잠금 모드|DBPROP_LOCKMODE|
|최대 열린 행 수|DBPROP_MAXOPENROWS|
|최대 보류 중인 행|DBPROP_MAXPENDINGROWS|
|최대 행 수|DBPROP_MAXROWS|
|알림 단위|DBPROP_NOTIFICATIONGRANULARITY|
|알림 단계|DBPROP_NOTIFICATIONPHASES|
|트랜잭션 개체|DBPROP_TRANSACTEDOBJECT|
|다른 사용자 변경 내용 표시|DBPROP_OTHERUPDATEDELETE|
|다른 사용자 삽입 내용 표시|DBPROP_OTHERINSERT|
|출력 인코딩 속성|DBPROP_OUTPUTENCODING|
|Output Stream 속성|DBPROP_OUTPUTSTREAM|
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
|서버 커서|DBPROP_SERVERCURSOR|
|삽입의 서버 데이터|DBPROP_SERVERDATAONINSERT|
|삭제 한 책갈피 건너뛰기|DBPROP_BOOKMARKSKIP|
|강력한 행 Id|DBPROP_STRONGIDENTITY|
|업데이트 허용|DBPROP_UPDATABILITY|
|책갈피 사용|DBPROP_BOOKMARKS|
|XML 루트|SSPROP_STREAM_XMLROOT|
|XSL|SSPROP_STREAM_XSL|

 특정 구현 세부 정보 및 Microsoft SQL Server OLE DB 공급자에 대 한 기능 정보에 대 한 참조를 [SQL Server 공급자](http://msdn.microsoft.com/adf1d6c4-5930-444a-9248-ff1979729635)합니다.

## <a name="see-also"></a>관련 항목
 [ConnectionString 속성 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [Provider 속성 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
