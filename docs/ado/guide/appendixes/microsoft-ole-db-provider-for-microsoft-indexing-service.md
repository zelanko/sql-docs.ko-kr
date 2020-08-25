---
description: Microsoft 인덱싱 서비스에 대 한 microsoft OLE DB 공급자 개요
title: Microsoft 인덱싱 서비스용 microsoft OLE DB 공급자 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Indexing Service provider [ADO]
- providers [ADO], OLE DB provider for Microsoft Indexing service
- OLE DB provider for Microsoft Indexing service [ADO]
ms.assetid: f86a0598-5097-471b-8318-d2c859d085f2
author: rothja
ms.author: jroth
ms.openlocfilehash: ec90db7109363cc017fd314dc674c143be01d185
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806624"
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Microsoft 인덱싱 서비스에 대 한 microsoft OLE DB 공급자 개요
Microsoft OLE DB Provider for Microsoft 인덱싱 서비스는 파일 시스템에 대 한 읽기 전용 액세스와 Microsoft 인덱싱 서비스에서 인덱싱된 웹 데이터에 대 한 읽기 전용 액세스를 제공 합니다. ADO 응용 프로그램은 SQL 쿼리를 실행 하 여 콘텐츠 및 파일 속성 정보를 검색할 수 있습니다.

 공급자는 자유 스레드된 및 유니코드를 사용할 수 있습니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결 하려면 **provider =** 인수를 [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md) 속성으로 설정 합니다.

```vb
MSIDXS
```

 [공급자](../../reference/ado-api/provider-property-ado.md) 속성을 읽으면이 문자열도 반환 됩니다.

## <a name="typical-connection-string"></a>일반 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은 다음과 같습니다.

```vb
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 문자열은 다음과 같은 키워드로 구성 됩니다.

|키워드|설명|
|-------------|-----------------|
|**공급 기업**|Microsoft 인덱싱 서비스용 OLE DB 공급자를 지정 합니다. 일반적으로이 키워드는 연결 문자열에 지정 된 유일한 키워드입니다.|
|**데이터 원본**|인덱싱 서비스 카탈로그 이름을 지정 합니다. 이 키워드를 지정 하지 않으면 기본 시스템 카탈로그가 사용 됩니다.|
|**로캘 ID**|사용자 언어와 관련 된 기본 설정을 지정 하는 고유한 32 비트 숫자 (예: 1033)를 지정 합니다. 이 키워드를 지정 하지 않으면 기본 시스템 로캘 식별자가 사용 됩니다.|

## <a name="command-text"></a>명령 텍스트
 인덱싱 서비스 SQL 쿼리 구문은 SQL-92 **SELECT** 문과 **FROM** 및 **WHERE** 절에 대 한 확장으로 구성 됩니다. 쿼리 결과는 ADO에서 사용 하 고 [레코드 집합](../../reference/ado-api/recordset-object-ado.md) 개체로 조작 될 수 있는 OLE DB 행 집합을 통해 반환 됩니다.

 정확한 단어나 구를 검색 하거나 와일드 카드를 사용 하 여 단어의 패턴이 나 형태소를 검색할 수 있습니다. 검색 논리는 부울 결정, 가중치가 적용 된 용어 또는 다른 단어에 근접 하는 것을 기반으로 할 수 있습니다. 정확한 단어가 아닌 의미를 기준으로 일치 항목을 찾는 "자유 텍스트"로 검색할 수도 있습니다.

 특정 명령 언어는 인덱싱 서비스 설명서에 대 한 쿼리 언어에 자세히 설명 되어 있습니다.

 공급자는 저장 프로시저 호출 또는 간단한 테이블 이름을 허용 하지 않습니다. 예를 들어, [CommandType](../../reference/ado-api/commandtype-property-ado.md) 속성은 항상 **adcmdtext**입니다.

## <a name="recordset-behavior"></a>레코드 집합 동작
 다음 표에서는이 공급자를 사용 하 여 연 **레코드 집합** 개체에 사용할 수 있는 기능을 나열 합니다. 정적 커서 유형 (**Adopenstatic**)만 사용할 수 있습니다.

 공급자 구성의 **레코드 집합** 동작에 대 한 자세한 내용을 보려면 [Supports](../../reference/ado-api/supports-method.md) 메서드를 실행 하 고 **레코드 집합** 의 [속성](../../reference/ado-api/properties-collection-ado.md) 컬렉션을 열거 하 여 공급자별 동적 속성이 있는지 여부를 확인 합니다.

 **표준 ADO 레코드 집합 속성의 가용성:**

|속성|가용성|
|--------------|------------------|
|[AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md)|읽기/쓰기|
|[AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md)|읽기/쓰기|
|[ActiveConnection](../../reference/ado-api/activeconnection-property-ado.md)|읽기 전용|
|[BOF](../../reference/ado-api/bof-eof-properties-ado.md)|읽기 전용|
|[책갈피](../../reference/ado-api/bookmark-property-ado.md)*|읽기/쓰기|
|[CacheSize](../../reference/ado-api/cachesize-property-ado.md)|읽기/쓰기|
|[CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md)|항상 **Aduseserver**|
|[CursorType](../../reference/ado-api/cursortype-property-ado.md)|항상 **Adopenstatic**|
|[EditMode](../../reference/ado-api/editmode-property.md)|항상 **adEditNone**|
|[객체](../../reference/ado-api/bof-eof-properties-ado.md)|읽기 전용|
|[Filter](../../reference/ado-api/filter-property.md)|읽기/쓰기|
|[LockType](../../reference/ado-api/locktype-property-ado.md)|읽기/쓰기|
|[MarshalOptions](../../reference/ado-api/marshaloptions-property-ado.md)|사용할 수 없음|
|[Records](../../reference/ado-api/maxrecords-property-ado.md)|읽기/쓰기|
|[PageCount](../../reference/ado-api/pagecount-property-ado.md)|읽기 전용|
|[PageSize](../../reference/ado-api/pagesize-property-ado.md)|읽기/쓰기|
|[RecordCount](../../reference/ado-api/recordcount-property-ado.md)|읽기 전용|
|[원본](../../reference/ado-api/source-property-ado-recordset.md)|읽기/쓰기|
|[State](../../reference/ado-api/state-property-ado.md)|읽기 전용|
|[상태](../../reference/ado-api/status-property-ado-recordset.md)|읽기 전용|

 \*이 기능이 **레코드 집합**에 존재 하려면 공급자에서 책갈피를 사용 하도록 설정 해야 합니다.

 **표준 ADO 레코드 집합 메서드의 가용성:**

|방법|사용 가능 여부|
|------------|----------------|
|[AddNew](../../reference/ado-api/addnew-method-ado.md)|아니요|
|[취소](../../reference/ado-api/cancel-method-ado.md)|예|
|[CancelBatch](../../reference/ado-api/cancelbatch-method-ado.md)|아니요|
|[CancelUpdate](../../reference/ado-api/cancelupdate-method-ado.md)|아니요|
|[복제](../../reference/ado-api/clone-method-ado.md)|예|
|[닫기](../../reference/ado-api/close-method-ado.md)|예|
|[Delete](../../reference/ado-api/delete-method-ado-recordset.md)|아니요|
|[GetRows](../../reference/ado-api/getrows-method-ado.md)|예|
|[이동](../../reference/ado-api/move-method-ado.md)|예|
|[MoveFirst](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|예|
|[NextRecordset](../../reference/ado-api/nextrecordset-method-ado.md)|예|
|[열기](../../reference/ado-api/open-method-ado-recordset.md)|예|
|[매크로](../../reference/ado-api/requery-method.md)|예|
|[다시 동기화](../../reference/ado-api/resync-method.md)|예|
|[지원](../../reference/ado-api/supports-method.md)|예|
|[Update](../../reference/ado-api/update-method.md)|아니요|
|[UpdateBatch](../../reference/ado-api/updatebatch-method.md)|아니요|

 Microsoft 인덱싱 서비스용 Microsoft OLE DB 공급자에 대 한 특정 구현 세부 정보 및 기능 정보는 [OLE DB 프로그래머 가이드](/previous-versions/windows/desktop/ms713643(v=vs.85))를 참조 하거나 Windows NT Server 웹 사이트의 웹 서비스 페이지를 방문 하십시오.

## <a name="see-also"></a>참고 항목
 [CommandType 속성 (](../../reference/ado-api/commandtype-property-ado.md) ado) [ConnectionString 속성](../../reference/ado-api/connectionstring-property-ado.md) (ado) [속성 컬렉션 (](../../reference/ado-api/properties-collection-ado.md) ado) [공급자 속성 (](../../reference/ado-api/provider-property-ado.md) ado) [레코드 집합 개체 (](../../reference/ado-api/recordset-object-ado.md) ado)는 [메서드를 지원 합니다](../../reference/ado-api/supports-method.md) .