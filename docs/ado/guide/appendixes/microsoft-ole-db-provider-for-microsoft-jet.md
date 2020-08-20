---
description: Microsoft Jet 용 microsoft OLE DB 공급자 개요
title: Microsoft Jet 용 microsoft OLE DB 공급자 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet provider for OLE DB [ADO]
- providers [ADO], OLE DB provider for Microsoft Jet
- OLE DB provider for Microsoft Jet [ADO]
ms.assetid: fd956da1-5203-40af-aa7e-fc13a6c6581f
author: rothja
ms.author: jroth
ms.openlocfilehash: 822c9f6ef6aebe5e32bb37e4c89a9bb4e6d7db68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454075"
---
# <a name="microsoft-ole-db-provider-for-microsoft-jet-overview"></a>Microsoft Jet 용 microsoft OLE DB 공급자 개요
Microsoft Jet 용 OLE DB 공급자를 사용 하 여 ADO에서 Microsoft Jet 데이터베이스에 액세스할 수 있습니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결 하려면 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성의 *공급자* 인수를 다음과 같이 설정 합니다.

```vb
Microsoft.Jet.OLEDB.4.0
```

 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 속성을 읽으면이 문자열도 반환 됩니다.

## <a name="typical-connection-string"></a>일반 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은 다음과 같습니다.

```vb
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=databaseName;User ID=MyUserID;Password=MyPassword;"
```

 문자열은 다음과 같은 키워드로 구성 됩니다.

|키워드|설명|
|-------------|-----------------|
|**공급자**|Microsoft Jet의 OLE DB 공급자를 지정 합니다.|
|**데이터 원본**|데이터베이스 경로와 파일 이름을 지정 합니다 (예: `c:\Northwind.mdb` ).|
|**사용자 ID**|사용자 이름을 지정합니다. 이 키워드를 지정 하지 않으면 `admin` 기본적으로 "" 문자열이 사용 됩니다.|
|**암호**|사용자 암호를 지정 합니다. 이 키워드를 지정 하지 않으면 기본적으로 빈 문자열 ("")이 사용 됩니다.|

> [!NOTE]
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 ID 및 암호 정보 대신 **Trusted_Connection = yes** 또는 **INTEGRATED Security = SSPI** 를 지정 해야 합니다.

## <a name="provider-specific-connection-parameters"></a>공급자별 연결 매개 변수
 Microsoft Jet 용 OLE DB 공급자는 ADO에 정의 된 속성 외에 여러 공급자별 동적 속성을 지원 합니다. 다른 모든 **연결** 매개 변수와 마찬가지로 연결 개체의 **Properties** 컬렉션을 사용 하 여 설정 **하거나 연결 문자열** 의 일부로 설정할 수 있습니다.

 다음 표에서는 이러한 속성을 해당 OLE DB 속성 이름과 함께 괄호 안에 나열 합니다.

|매개 변수|설명|
|---------------|-----------------|
|Jet OLEDB: 압축 여유 공간 크기 (DBPROP_JETOLEDB_COMPACTFREESPACESIZE)|데이터베이스를 압축 하 여 회수할 수 있는 공간의 예상 크기 (바이트)를 나타냅니다. 이 값은 데이터베이스 연결이 설정 된 후에만 유효 합니다.|
|Jet OLEDB: 연결 제어 (DBPROP_JETOLEDB_CONNECTIONCONTROL)|사용자가 데이터베이스에 연결할 수 있는지 여부를 나타냅니다.|
|Jet OLEDB: 시스템 데이터베이스 만들기 (DBPROP_JETOLEDB_CREATESYSTEMDATABASE)|새 데이터 원본을 만들 때 시스템 데이터베이스를 만들어야 하는지 여부를 나타냅니다.|
|Jet OLEDB: 데이터베이스 잠금 모드 (DBPROP_JETOLEDB_DATABASELOCKMODE)|이 데이터베이스의 잠금 모드를 나타냅니다. 데이터베이스를 여는 첫 번째 사용자는 데이터베이스를 열 때 사용 되는 모드를 결정 합니다.|
|Jet OLEDB: 데이터베이스 암호 (DBPROP_JETOLEDB_DATABASEPASSWORD)|데이터베이스 암호를 나타냅니다.|
|Jet OLEDB: Compact에서 로캘을 복사 하지 않음 (DBPROP_JETOLEDB_COMPACT_DONTCOPYLOCALE)|데이터베이스를 압축할 때 Jet에서 로캘 정보를 복사할지 여부를 나타냅니다.|
|Jet OLEDB: 데이터베이스 암호화 (DBPROP_JETOLEDB_ENCRYPTDATABASE)|압축 된 데이터베이스를 암호화할지 여부를 나타냅니다. 이 속성이 설정 되지 않은 경우 원본 데이터베이스가 암호화 된 경우에도 압축 된 데이터베이스는 암호화 됩니다.|
|Jet OLEDB: 엔진 유형 (DBPROP_JETOLEDB_ENGINE)|현재 데이터 저장소에 액세스 하는 데 사용 되는 저장소 엔진을 나타냅니다.|
|Jet OLEDB: 전용 비동기 지연 (DBPROP_JETOLEDB_EXCLUSIVEASYNCDELAY)|데이터베이스가 단독으로 열리는 경우 Jet에서 디스크에 대 한 비동기 쓰기를 지연할 수 있는 최대 시간 (밀리초)을 나타냅니다.<br /><br /> **JET OLEDB: Flush Transaction Timeout** 이 0으로 설정 되지 않은 경우이 속성은 무시 됩니다.|
|Jet OLEDB: 플러시 트랜잭션 시간 제한 (DBPROP_JETOLEDB_FLUSHTRANSACTIONTIMEOUT)|비동기 쓰기를 위해 캐시에 저장 된 데이터가 실제로 디스크에 기록 될 때까지 대기 하는 시간을 나타냅니다. 이 설정은 **JET oledb: Shared Async delay** 및 **Jet Oledb: 배타 비동기 지연**값을 재정의 합니다.|
|Jet OLEDB: 글로벌 대량 트랜잭션 (DBPROP_JETOLEDB_GLOBALBULKNOTRANSACTIONS)|SQL 대량 트랜잭션이 트랜잭션 되었는지 여부를 나타냅니다.|
|Jet OLEDB: 전역 부분 대량 Ops (DBPROP_JETOLEDB_GLOBALBULKPARTIAL)|데이터베이스를 여는 데 사용 된 암호를 나타냅니다.|
|Jet OLEDB: 암시적 커밋 동기화 (DBPROP_JETOLEDB_IMPLICITCOMMITSYNC)|내부 암시적 트랜잭션에서 수행 된 변경 내용을 동기 또는 비동기 모드로 쓸지 여부를 나타냅니다.|
|Jet OLEDB: 잠금 지연 (DBPROP_JETOLEDB_LOCKDELAY)|이전 시도가 실패 한 후 잠금을 얻으려고 시도할 때까지 대기 하는 시간 (밀리초)을 나타냅니다.|
|Jet OLEDB: 잠금 다시 시도 (DBPROP_JETOLEDB_LOCKRETRY)|잠긴 페이지에 대 한 액세스 시도가 반복 되는 횟수를 나타냅니다.|
|Jet OLEDB: 최대 버퍼 크기 (DBPROP_JETOLEDB_MAXBUFFERSIZE)|Jet가 변경 내용을 디스크에 플러시하기 전에 사용할 수 있는 최대 메모리 양 (kb)을 나타냅니다.|
|Jet OLEDB: 파일당 최대 잠금 수 (DBPROP_JETOLEDB_MAXLOCKSPERFILE)|Jet가 데이터베이스에 대해 수행할 수 있는 최대 잠금 수를 나타냅니다. 기본값은 9500입니다.|
|Jet OLEDB: 새 데이터베이스 암호 (DBPROP_JETOLEDB_NEWDATABASEPASSWORD)|이 데이터베이스에 대해 설정할 새 암호를 나타냅니다. 이전 암호는 **JET OLEDB: 데이터베이스 암호**에 저장 됩니다.|
|Jet OLEDB: ODBC 명령 제한 시간 (DBPROP_JETOLEDB_ODBCCOMMANDTIMEOUT)|Jet에서 원격 ODBC 쿼리가 시간 초과 될 때까지 걸리는 시간 (밀리초)을 나타냅니다.|
|Jet OLEDB: 페이지 잠금을 테이블 잠금으로 잠금 (DBPROP_JETOLEDB_PAGELOCKSTOTABLELOCK)|Jet에서 테이블 잠금으로 잠금을 승격 하려고 시도 하기 전에 트랜잭션 내에서 잠가야 하는 페이지 수를 나타냅니다. 이 값이 0 이면 잠금이 승격 되지 않습니다.|
|Jet OLEDB: 페이지 시간 제한 (DBPROP_JETOLEDB_PAGETIMEOUT)|데이터베이스 파일을 사용 하 여 캐시가 만료 되었는지 확인 하기 전에 Jet에서 대기 하는 시간 (밀리초)을 나타냅니다.|
|Jet OLEDB: 장기 값 페이지 재활용 (DBPROP_JETOLEDB_RECYCLELONGVALUEPAGES)|Jet가 해제 될 때 BLOB 페이지가 적극적으로 회수 되도록 할지 여부를 나타냅니다.|
|Jet OLEDB: 레지스트리 경로 (DBPROP_JETOLEDB_REGPATH)|Jet 데이터베이스 엔진에 대 한 값을 포함 하는 Windows 레지스트리 키를 나타냅니다.|
|Jet OLEDB: ISAM 통계 다시 설정 (DBPROP_JETOLEDB_RESETISAMSTATS)|스키마 **레코드 집합** DBSCHEMA_JETOLEDB_ISAMSTATS 성능 정보를 반환한 후 해당 성능 카운터를 다시 설정 해야 하는지 여부를 나타냅니다.|
|Jet OLEDB: 공유 비동기 지연 (DBPROP_JETOLEDB_SHAREDASYNCDELAY)|데이터베이스를 다중 사용자 모드로 열 때 Jet에서 디스크에 대 한 비동기 쓰기를 지연할 수 있는 최대 시간 (밀리초)을 나타냅니다.|
|Jet OLEDB: 시스템 데이터베이스 (DBPROP_JETOLEDB_SYSDBPATH)|작업 그룹 정보 파일 (시스템 데이터베이스)의 경로와 파일 이름을 나타냅니다.|
|Jet OLEDB: 트랜잭션 커밋 모드 (DBPROP_JETOLEDB_TXNCOMMITMODE)|트랜잭션이 커밋될 때 Jet에서 디스크에 데이터를 동기적으로 기록할지 또는 비동기적으로 기록할지를 나타냅니다.|
|Jet OLEDB: 사용자 커밋 동기화 (DBPROP_JETOLEDB_USERCOMMITSYNC)|트랜잭션에서 수행 된 변경 내용을 동기 또는 비동기 모드로 쓸지 여부를 나타냅니다.|

## <a name="provider-specific-recordset-and-command-properties"></a>공급자별 레코드 집합 및 명령 속성
 또한 Jet 공급자는 여러 공급자별 **레코드 집합과** **명령** 속성을 지원 합니다. 이러한 속성에 액세스 하 여 **레코드 집합** 또는 **명령** 개체의 **속성** 컬렉션을 통해 설정 합니다. 표는 ADO 속성 이름 및 해당 OLE DB 속성 이름을 괄호 안에 나열 합니다.

|속성 이름|설명|
|-------------------|-----------------|
|Jet OLEDB: 대량 트랜잭션 (DBPROP_JETOLEDB_BULKNOTRANSACTIONS)|SQL 대량 작업이 트랜잭션 되었는지 여부를 나타냅니다. 리소스 지연으로 인해 트랜잭션이 트랜잭션 되었을 때 대규모 대량 작업이 실패할 수 있습니다.|
|Jet OLEDB: Fat 커서 사용 (DBPROP_JETOLEDB_ENABLEFATCURSOR)|원격 행 원본에 대해 레코드 집합을 채울 때 Jet에서 여러 행을 캐시 해야 하는지 여부를 나타냅니다.|
|Jet OLEDB: Fat 커서 캐시 크기 (DBPROP_JETOLEDB_FATCURSORMAXROWS)|원격 데이터 저장소 행 캐싱을 사용할 때 캐시할 행 수를 나타냅니다. **JET OLEDB: Fat 커서 사용** 이 True가 아니면이 값은 무시 됩니다.|
|Jet OLEDB: 일치 하지 않음 (DBPROP_JETOLEDB_INCONSISTENT)|쿼리 결과가 일치 하지 않는 업데이트를 허용 하는지 여부를 나타냅니다.|
|Jet OLEDB: 잠금 세분성 (DBPROP_JETOLEDB_LOCKGRANULARITY)|행 수준 잠금을 사용 하 여 테이블을 열지 여부를 나타냅니다.|
|Jet OLEDB: ODBC 통과 문 (DBPROP_JETOLEDB_ODBCPASSTHROUGH)|Jet에서 **명령** 개체의 SQL 텍스트를 변경 되지 않은 백 엔드에 전달 해야 함을 나타냅니다.|
|Jet OLEDB: 부분 대량 Ops (DBPROP_JETOLEDB_BULKPARTIAL)|SQL DML 작업이 실패할 때 Jet 동작을 나타냅니다.|
|Jet OLEDB: 통과 쿼리 대량 작업 (DBPROP_JETOLEDB_PASSTHROUGHBULKOP)|**레코드 집합** 을 반환 하지 않는 쿼리가 변경 되지 않은 상태로 데이터 원본에 전달 되는지 여부를 나타냅니다.|
|Jet OLEDB: 쿼리 연결 문자열 전달 (DBPROP_JETOLEDB_ODBCPASSTHROUGHCONNECTSTRING)|원격 데이터 저장소에 연결 하는 데 사용 되는 Jet 연결 문자열을 나타냅니다. **JET OLEDB: ODBC 통과 문이** True가 아니면이 값은 무시 됩니다.|
|Jet OLEDB: 저장 된 쿼리 (DBPROP_JETOLEDB_STOREDQUERY)|명령 텍스트를 SQL 명령 대신 저장 쿼리로 해석할지 여부를 나타냅니다.|
|Jet OLEDB: 집합에 대 한 규칙 유효성 검사 (DBPROP_JETOLEDB_VALIDATEONSET)|열 데이터가 설정 되거나 변경 내용이 데이터베이스에 커밋될 때 Jet 유효성 검사 규칙이 평가 되는지 여부를 나타냅니다.|

 기본적으로 Microsoft Jet 용 OLE DB 공급자는 읽기/쓰기 모드에서 Microsoft Jet 데이터베이스를 엽니다. 읽기 전용 모드로 데이터베이스를 열려면 ADO **연결** 개체의 [Mode](../../../ado/reference/ado-api/mode-property-ado.md) 속성을 **adModeRead**로 설정 합니다.

## <a name="command-object-usage"></a>명령 개체 사용
 [Command](../../../ado/reference/ado-api/command-object-ado.md) 개체의 명령 텍스트는 MICROSOFT Jet SQL 언어를 사용 합니다. 명령 텍스트에서 행 반환 쿼리, 동작 쿼리 및 테이블 이름을 지정할 수 있습니다. 그러나 저장 프로시저는 지원 되지 않으므로 지정 하면 안 됩니다.

## <a name="recordset-behavior"></a>레코드 집합 동작
 Microsoft Jet 데이터베이스 엔진은 동적 커서를 지원 하지 않습니다. 따라서 Microsoft Jet 용 OLE DB 공급자는 **Adlockdynamic** 커서 유형을 지원 하지 않습니다. 동적 커서가 요청 될 때 공급자는 키 집합 커서를 반환 하 고 [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) 속성을 다시 설정 하 여 반환 되는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 의 유형을 표시 합니다. 또한 업데이트할 수 있는 **레코드 집합이** 요청 될 경우 **(LockType** is **adlockoptimistic**, **Adlockbatch낙관적**또는 **adlockoptimistic**) 공급자가 키 집합 커서를 반환 하 고 **CursorType** 속성을 다시 설정 합니다.

## <a name="dynamic-properties"></a>동적 속성
 Microsoft Jet 용 OLE DB 공급자는 열려 있는 [연결](../../../ado/reference/ado-api/connection-object-ado.md), [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)및 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체의 **properties** 컬렉션에 몇 가지 동적 속성을 삽입 합니다.

 다음 테이블은 각 동적 속성에 대 한 ADO 및 OLE DB 이름의 교차 인덱스입니다. OLE DB 프로그래머 참조는 "설명" 이라는 용어로 ADO 속성 이름을 참조 합니다. 이러한 속성에 대 한 자세한 내용은 OLE DB 프로그래머 참조에서 찾을 수 있습니다.

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
|현재 카탈로그|DBPROP_CURRENTCATALOG|
|데이터 원본|DBPROP_INIT_DATASOURCE|
|데이터 원본 이름|DBPROP_DATASOURCENAME|
|데이터 원본 개체 스레딩 모델|DBPROP_DSOTHREADMODEL|
|DBMS 이름|DBPROP_DBMSNAME|
|DBMS 버전|DBPROP_DBMSVER|
|지원 별 그룹화|DBPROP_GROUPBY|
|유형이 다른 테이블 지원|DBPROP_HETEROGENEOUSTABLES|
|식별자 대/소문자 구분|DBPROP_IDENTIFIERCASE|
|격리 수준|DBPROP_SUPPORTEDTXNISOLEVELS|
|격리 보존|DBPROP_SUPPORTEDTXNISORETAIN|
|로캘 ID|DBPROP_INIT_LCID|
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
|OLE DB 버전|DBPROP_PROVIDEROLEDBVER|
|OLE 개체 지원|DBPROP_OLEOBJECTS|
|열 행 집합 지원|DBPROP_OPENROWSETSUPPORT|
|Select 목록의 ORDER BY 열|DBPROP_ORDERBYCOLUMNSINSELECT|
|출력 매개 변수 가용성|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Ref 접근자로 전달|DBPROP_BYREFACCESSORS|
|암호|DBPROP_AUTH_PASSWORD|
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
|추가 전용 행 집합|DBPROP_APPENDONLY|
|저장소 개체 차단|DBPROP_BLOCKINGSTORAGEOBJECTS|
|책갈피 유형|DBPROP_BOOKMARKTYPE|
|책갈피 가능|DBPROP_IROWSETLOCATE|
|정렬 된 책갈피|DBPROP_ORDEREDBOOKMARKS|
|캐시 지연 열|DBPROP_CACHEDEFERRED|
|삽입 된 행 변경|DBPROP_CHANGEINSERTEDROWS|
|열 권한|DBPROP_COLUMNRESTRICT|
|열 집합 알림|DBPROP_NOTIFYCOLUMNSET|
|쓰기 가능 열|DBPROP_MAYWRITECOLUMN|
|열 지연|DBPROP_DEFERRED|
|저장소 개체 업데이트 지연|DBPROP_DELAYSTORAGEOBJECTS|
|뒤로 인출|DBPROP_CANFETCHBACKWARDS|
|행 유지|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Immobile 행|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|인해|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|리터럴 책갈피|DBPROP_LITERALBOOKMARKS|
|리터럴 행 Id|DBPROP_LITERALIDENTITY|
|최대 열린 행|DBPROP_MAXOPENROWS|
|최대 보류 중인 행|DBPROP_MAXPENDINGROWS|
|최대 행|DBPROP_MAXROWS|
|메모리 사용량|DBPROP_MEMORYUSAGE|
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
|삭제 된 책갈피 건너뛰기|DBPROP_BOOKMARKSKIPPED|
|강력한 행 Id|DBPROP_STRONGITDENTITY|
|업데이트 가능성|DBPROP_UPDATABILITY|
|책갈피 사용|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>명령 동적 속성
 다음 속성이 **Command** 개체의 **properties** 컬렉션에 추가 됩니다.

|ADO 속성 이름|OLE DB 속성 이름|
|-----------------------|--------------------------|
|액세스 순서|DBPROP_ACCESSORDER|
|추가 전용 행 집합|DBPROP_APPENDONLY|
|저장소 개체 차단|DBPROP_BLOCKINGSTORAGEOBJECTS|
|책갈피 유형|DBPROP_BOOKMARKTYPE|
|책갈피 가능|DBPROP_IROWSETLOCATE|
|삽입 된 행 변경|DBPROP_CHANGEINSERTEDROWS|
|열 권한|DBPROP_COLUMNRESTRICT|
|열 집합 알림|DBPROP_NOTIFYCOLUMNSET|
|열 지연|DBPROP_DEFERRED|
|저장소 개체 업데이트 지연|DBPROP_DELAYSTORAGEOBJECTS|
|뒤로 인출|DBPROP_CANFETCHBACKWARDS|
|행 유지|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Immobile 행|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|인해|DBPROP_IStorage|
|IStream|DBPROP_IStream|
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
|삽입 시 서버 데이터|DBPROP_SERVERDATAONINSERT|
|삭제 된 책갈피 건너뛰기|DBPROP_BOOKMARKSKIP|
|강력한 행 Id|DBPROP_STRONGIDENTITY|
|업데이트 가능성|DBPROP_UPDATABILITY|
|책갈피 사용|DBPROP_BOOKMARKS|

 Microsoft Jet 용 OLE DB 공급자에 대 한 특정 구현 세부 정보 및 기능 정보는 OLE DB 설명서의 [Jet 공급자](https://msdn.microsoft.com/library/windows/desktop/ms722791.aspx) 를 참조 하십시오.
