---
description: ADO 동적 속성 인덱스
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a4777349384d372355a107cced1503d774ade4f7
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771742"
---
# <a name="ado-dynamic-property-index"></a>ADO 동적 속성 인덱스
데이터 공급자, 서비스 공급자 및 서비스 구성 요소는 열려 있지 않은 [연결](./connection-object-ado.md) 및 [레코드 집합](./recordset-object-ado.md) 개체의 **속성** 컬렉션에 동적 속성을 추가할 수 있습니다. 지정 된 공급자는 이러한 개체를 열 때 추가 속성을 삽입할 수도 있습니다. 이러한 속성 중 일부는 [ADO 동적 속성](./ado-dynamic-properties.md) 섹션에 나열 됩니다. 자세한 내용은 [부록 a: providers](../../guide/appendixes/appendix-a-providers.md) 섹션의 특정 공급자에 나열 되어 있습니다.  
  
 다음 표는 각 표준 OLE DB 공급자 동적 속성에 대 한 ADO 및 OLE DB 이름의 교차 인덱스입니다. 공급자는 여기에 나열 된 것 보다 더 많은 속성을 추가할 수 있습니다. 공급자별 동적 속성에 대 한 자세한 내용은 공급자 설명서를 참조 하십시오.  
  
 OLE DB 프로그래머 참조는 "설명" 이라는 용어를 통해 ADO 속성 이름을 참조 합니다. 이러한 표준 속성에 대 한 자세한 내용은 OLE DB 속성에 대 한 [OLE DB 설명서](/previous-versions/windows/desktop/ms722784(v=vs.85))에서 인덱스를 검색 하거나 해당 이름으로 이동 합니다.  
  
## <a name="connection-dynamic-properties"></a>연결 동적 속성  
  
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
 **레코드 집합 개체의** **동적 속성** 은 **레코드 집합** 을 닫을 때 범위 (사용할 수 없음)로 이동 합니다.  
  
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
|인해|DBPROP_ISTORAGE|  
|IStream|DBPROP_ISTREAM|  
|ISupportErrorInfo|DBPROP_ISUPPORTERRORINFO|  
|액세스 순서|DBPROP_ACCESSORDER|  
|추가 전용 행 집합|DBPROP_APPENDONLY|  
|비동기 행 집합 처리|DBPROP_ROWSET_ASYNCH|  
|자동 다시 계산|DBPROP_ADC_AUTORECALC|  
|백그라운드 페치 크기|DBPROP_ASYNCHFETCHSIZE|  
|백그라운드 스레드 우선 순위|DBPROP_ASYNCHTHREADPRIORITY|  
|Batch 크기|DBPROP_ADC_BATCHSIZE|  
|저장소 개체 차단|DBPROP_BLOCKINGSTORAGEOBJECTS|  
|책갈피 유형|DBPROP_BOOKMARKTYPE|  
|책갈피 가능|DBPROP_IROWSETLOCATE|  
|정렬 된 책갈피|DBPROP_ORDEREDBOOKMARKS|  
|자식 행 캐시|DBPROP_ADC_CACHECHILDROWS|  
|캐시 지연 열|DBPROP_CACHEDEFERRED|  
|삽입 된 행 변경|DBPROP_CHANGEINSERTEDROWS|  
|열 권한|DBPROP_COLUMNRESTRICT|  
|열 집합 알림|DBPROP_NOTIFYCOLUMNSET|  
|쓰기 가능 열|DBPROP_MAYWRITECOLUMN|  
|명령 제한 시간|DBPROP_COMMANDTIMEOUT|  
|커서 엔진 버전|DBPROP_ADC_CEVER|  
|열 지연|DBPROP_DEFERRED|  
|저장소 개체 업데이트 지연|DBPROP_DELAYSTORAGEOBJECTS|  
|뒤로 인출|DBPROP_CANFETCHBACKWARDS|  
|필터 작업|DBPROP_FILTERCOMPAREOPS|  
|찾기 작업|DBPROP_FINDCOMPAREOPS|  
|숨겨진 열 (개수)|DBPROP_HIDDENCOLUMNS|  
|행 유지|DBPROP_CANHOLDROWS|  
|Immobile 행|DBPROP_IMMOBILEROWS|  
|초기 인출 크기|DBPROP_ASYNCHPREFETCHSIZE|  
|리터럴 책갈피|DBPROP_LITERALBOOKMARKS|  
|리터럴 행 Id|DBPROP_LITERALIDENTITY|  
|변경 상태 유지|DBPROP_ADC_MAINTAINCHANGESTATUS|  
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
|Private1||  
|빠른 다시 시작|DBPROP_QUICKRESTART|  
|재진입 이벤트|DBPROP_REENTRANTEVENTS|  
|삭제 된 행 제거|DBPROP_REMOVEDELETED|  
|여러 변경 내용 보고|DBPROP_REPORTMULTIPLECHANGES|  
|이름 변경|DBPROP_ADC_RESHAPENAME|  
|다시 동기화 명령|DBPROP_ADC_CUSTOMRESYNCH|  
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
|삭제 된 책갈피 건너뛰기|DBPROP_BOOKMARKSKIPPED|  
|강력한 행 Id|DBPROP_STRONGIDENTITY|  
|고유 카탈로그|DBPROP_ADC_UNIQUECATALOG|  
|고유 행|DBPROP_UNIQUEROWS|  
|고유 스키마|DBPROP_ADC_UNIQUESCHEMA|  
|고유한 테이블|DBPROP_ADC_UNIQUETABLE|  
|업데이트 가능성|DBPROP_UPDATABILITY|  
|업데이트 조건|DBPROP_ADC_UPDATECRITERIA|  
|업데이트 다시 동기화|DBPROP_ADC_UPDATERESYNC|  
|책갈피 사용|DBPROP_BOOKMARKS|