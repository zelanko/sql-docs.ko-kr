---
title: ADO 동적 속성 인덱스 | Microsoft Docs
ms.prod: sql
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO], index
ms.assetid: 80d389dd-46ef-459f-b0d4-6f712fc4f32d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9eb88905f56abf9c1c702f5fd73cbe61a1bcde3d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921087"
---
# <a name="ado-dynamic-property-index"></a>ADO 동적 속성 인덱스
데이터 공급자, 서비스 공급자 및 서비스 구성 요소에는 동적 속성을 추가할 수는 **속성** 컬렉션을 아직 열지 않은 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 하 고 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 이러한 개체를 열 때 지정된 된 공급자 추가 속성을 삽입할 수도 수 있습니다. 에 나열 된 이러한 속성 중 일부는 [ADO 동적 속성](../../../ado/reference/ado-api/ado-dynamic-properties.md) 섹션입니다. 자세히가 특정 공급자에 나열 된 [부록 a: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md) 섹션입니다.  
  
 다음 표에서 각 표준 OLE DB 공급자 동적 속성에 대 한 OLE DB 및 ADO 이름의 cross-indexes 됩니다. 공급자는 여기 나열 된 것 보다 더 많은 속성을 추가할 수 있습니다. 공급자별 동적 속성에 대 한 자세한 내용은 공급자 설명서를 참조 하세요.  
  
 OLE DB 프로그래머 참조 이름을 참조 하는 ADO 속성 "설명 합니다." 라는 용어로 인덱스를 찾아보거나 검색 이러한 표준 속성에 대 한 자세한 내용은 합니다 [OLE DB 설명서](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)이름 사용 하 여 OLE DB 속성에 대 한 합니다.  
  
## <a name="connection-dynamic-properties"></a>연결의 동적 속성  
  
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
|Ref 접근자로 전달|DBPROP_BYREFACCESSORS|  
|암호|DBPROP_AUTH_PASSWORD|  
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
 합니다 **동적 속성** 의 **레코드 집합** 개체 (사용할 수 없게) 경우 범위 외부로 이동 합니다 **레코드 집합** 닫혀 합니다.  
  
|ADO 속성 이름|OLE DB 속성 이름|  
|-----------------------|--------------------------|  
|IAccessor|DBPROP_IACCESSOR|  
|IChapteredRowset||  
|IColumnsInfo|DBPROP_ICOLUMNSINFO|  
|IColumnsRowset|DBPROP_ICOLUMNSROWSET|  
|IConnectionPointContainer|DBPROP_ICONNECTIONPOINTCONTAINER|  
|IConvertType||  
|ILockBytes|DBPROP_ILOCKBYTES|  
|IRowset|DBPROP_IROWSET|  
|IDBAsynchStatus|DBPROP_IDBASYNCHSTATUS|  
|IParentRowset||  
|IRowsetChange|DBPROP_IROWSETCHANGE|  
|IRowsetExactScroll||  
|IRowsetFind|DBPROP_IROWSETFIND|  
|IRowsetIdentity|DBPROP_IROWSETIDENTITY|  
|IRowsetInfo|DBPROP_IROWSETINFO|  
|IRowsetLocate|DBPROP_IROWSETLOCATE|  
|IRowsetRefresh|DBPROP_IROWSETREFRESH|  
|IRowsetResynch||  
|IRowsetScroll|DBPROP_IROWSETSCROLL|  
|IRowsetUpdate|DBPROP_IROWSETUPDATE|  
|IRowsetView|DBPROP_IROWSETVIEW|  
|IRowsetIndex|DBPROP_IROWSETINDEX|  
|ISequentialStream|DBPROP_ISEQUENTIALSTREAM|  
|IStorage|DBPROP_ISTORAGE|  
|IStream|DBPROP_ISTREAM|  
|ISupportErrorInfo|DBPROP_ISUPPORTERRORINFO|  
|액세스 순서|DBPROP_ACCESSORDER|  
|추가 전용 행 집합|DBPROP_APPENDONLY|  
|비동기 행 집합 처리|DBPROP_ROWSET_ASYNCH|  
|자동 다시 계산|DBPROP_ADC_AUTORECALC|  
|백그라운드 페치 크기|DBPROP_ASYNCHFETCHSIZE|  
|백그라운드 스레드 우선 순위|DBPROP_ASYNCHTHREADPRIORITY|  
|일괄 처리 크기|DBPROP_ADC_BATCHSIZE|  
|저장소 개체 차단|DBPROP_BLOCKINGSTORAGEOBJECTS|  
|책갈피 형식|DBPROP_BOOKMARKTYPE|  
|책갈피를 설정할|DBPROP_IROWSETLOCATE|  
|순서 있는 책갈피|DBPROP_ORDEREDBOOKMARKS|  
|자식 행을 캐시|DBPROP_ADC_CACHECHILDROWS|  
|지연 된 열을 캐시 합니다.|DBPROP_CACHEDEFERRED|  
|삽입된 행 변경|DBPROP_CHANGEINSERTEDROWS|  
|열 권한|DBPROP_COLUMNRESTRICT|  
|열 설정 알림|DBPROP_NOTIFYCOLUMNSET|  
|쓰기 가능한 열|DBPROP_MAYWRITECOLUMN|  
|명령 시간 제한|DBPROP_COMMANDTIMEOUT|  
|커서 엔진 버전|DBPROP_ADC_CEVER|  
|열 지연|DBPROP_DEFERRED|  
|저장소 개체 업데이트 연기|DBPROP_DELAYSTORAGEOBJECTS|  
|뒤로 페치|DBPROP_CANFETCHBACKWARDS|  
|필터 작업|DBPROP_FILTERCOMPAREOPS|  
|찾기 작업|DBPROP_FINDCOMPAREOPS|  
|숨겨진된 열 (개수)|DBPROP_HIDDENCOLUMNS|  
|행 고정|DBPROP_CANHOLDROWS|  
|부동 행|DBPROP_IMMOBILEROWS|  
|초기 반입 크기|DBPROP_ASYNCHPREFETCHSIZE|  
|리터럴 책갈피|DBPROP_LITERALBOOKMARKS|  
|리터럴 행 Id|DBPROP_LITERALIDENTITY|  
|변경 상태를 유지 관리|DBPROP_ADC_MAINTAINCHANGESTATUS|  
|최대 열린 행 수|DBPROP_MAXOPENROWS|  
|최대 보류 중인 행|DBPROP_MAXPENDINGROWS|  
|최대 행 수|DBPROP_MAXROWS|  
|메모리 사용량|DBPROP_MEMORYUSAGE|  
|알림 단위|DBPROP_NOTIFICATIONGRANULARITY|  
|알림 단계|DBPROP_NOTIFICATIONPHASES|  
|트랜잭션 개체|DBPROP_TRANSACTEDOBJECT|  
|다른 사용자 변경 내용 표시|DBPROP_OTHERUPDATEDELETE|  
|다른 사용자 삽입 내용 표시|DBPROP_OTHERINSERT|  
|내 변경 내용 표시|DBPROP_OWNUPDATEDELETE|  
|내 삽입 내용 표시|DBPROP_OWNINSERT|  
|중단 시 유지|DBPROP_ABORTPRESERVE|  
|커밋 시 유지|DBPROP_COMMITPRESERVE|  
|Private1||  
|빠른 다시 시작|DBPROP_QUICKRESTART|  
|재진입 이벤트|DBPROP_REENTRANTEVENTS|  
|삭제 된 행 제거|DBPROP_REMOVEDELETED|  
|여러 변경 내용 보고|DBPROP_REPORTMULTIPLECHANGES|  
|변형 이름|DBPROP_ADC_RESHAPENAME|  
|다시 동기화 명령|DBPROP_ADC_CUSTOMRESYNCH|  
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
|삭제 한 책갈피 건너뛰기|DBPROP_BOOKMARKSKIPPED|  
|강력한 행 Id|DBPROP_STRONGIDENTITY|  
|고유 카탈로그|DBPROP_ADC_UNIQUECATALOG|  
|고유한 행|DBPROP_UNIQUEROWS|  
|고유한 스키마|DBPROP_ADC_UNIQUESCHEMA|  
|고유한 테이블|DBPROP_ADC_UNIQUETABLE|  
|업데이트 허용|DBPROP_UPDATABILITY|  
|업데이트 기준|DBPROP_ADC_UPDATECRITERIA|  
|다시 동기화를 업데이트 합니다.|DBPROP_ADC_UPDATERESYNC|  
|책갈피 사용|DBPROP_BOOKMARKS|
