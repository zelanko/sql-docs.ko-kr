---
title: Microsoft 인덱싱 서비스용 Microsoft OLE DB Provider | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: dea7ec95efc1f560a2279868b2116d02d7ad6fef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701211"
---
# <a name="microsoft-ole-db-provider-for-microsoft-indexing-service-overview"></a>Microsoft OLE DB Provider for Microsoft 인덱싱 서비스 개요
Microsoft OLE DB Provider for Microsoft Indexing Service가 파일 시스템 및 Microsoft 인덱싱 서비스에 의해 인덱싱된 웹 데이터에 대 한 프로그래밍 방식으로 읽기 전용 액세스를 제공 합니다. ADO 응용 프로그램 콘텐츠 및 파일 속성 정보를 검색 하는 SQL 쿼리를 실행할 수 있습니다.

 공급자가 자유 스레드 및 유니코드를 사용할 수 있습니다.

## <a name="connection-string-parameters"></a>연결 문자열 매개 변수
 이 공급자에 연결을 설정 합니다 **공급자 =** 인수를 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성을:

```vb
MSIDXS
```

 읽기를 [공급자](../../../ado/reference/ado-api/provider-property-ado.md) 이 문자열로 반환 됩니다.

## <a name="typical-connection-string"></a>일반적인 연결 문자열
 이 공급자에 대 한 일반적인 연결 문자열은:

```vb
"Provider=MSIDXS;Data Source=myCatalog;Locale Identifier=nnnn;"
```

 문자열을 이러한 키워드 이루어져 있습니다.

|키워드|설명|
|-------------|-----------------|
|**공급자**|Microsoft 인덱싱 서비스용 OLE DB Provider를 지정합니다. 일반적으로 이것은 유일한 키워드 연결 문자열에 지정 합니다.|
|**데이터 원본**|인덱싱 서비스 카탈로그 이름을 지정합니다. 이 키워드를 지정 하지 않으면 기본 시스템 카탈로그가 사용 됩니다.|
|**로캘 ID**|(예: 1033) 사용자의 언어와 관련 된 기본 설정을 지정 하는 고유한 32 비트 숫자를 지정 합니다. 이 키워드를 지정 하지 않으면 기본 시스템 로캘 식별자를 사용 됩니다.|

## <a name="command-text"></a>명령 텍스트
 인덱싱 서비스 SQL 쿼리 구문이 SQL-92에 대 한 확장으로 이루어져 **선택** 문 및 해당 **FROM** 하 고 **여기서** 절. ADO에서 사용 하 고으로 조작할 수 있는 OLE DB 행 집합을 통해 쿼리 결과가 반환 됩니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.

 정확한 단어 또는 구를 검색할 수도 있고 와일드 카드를 사용 하 여 패턴 또는 단어의 형태소 분석을 검색할 수 있습니다. 검색 논리는 부울을 결정, 가중치 단어 또는 다른 단어에 근접을 기반으로 사용할 수 있습니다. 기반으로 정확한 단어가 아닌 의미를 일치 항목을 찾습니다. "자유 텍스트" 하 여 검색할 수 있습니다.

 인덱싱 서비스 설명서에 대 한 쿼리 언어에서 특정 명령 설명 완벽 하 게 됩니다.

 저장된 프로시저 호출 또는 간단한 테이블 이름을 공급자 허용 하지 않습니다 (예를 들어 합니다 [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) 속성은 항상 **adCmdText**).

## <a name="recordset-behavior"></a>레코드 집합 동작
 다음 표에서 사용할 수 있는 기능을 **레코드 집합** 개체를이 공급자를 사용 하 여 열입니다. 정적 커서 형식에만 (**adOpenStatic**)를 사용할 수 있습니다.

 정보에 대 한 자세한 **레코드 집합** 실행 공급자 구성에 대 한 동작을 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드를 열거 하 고는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션은 **레코드 집합** 공급자별 동적 속성 존재 여부를 확인할 수 있습니다.

 **표준 ADO 레코드 집합 속성의 사용 가능:**

|속성|가용성|
|--------------|------------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|읽기/쓰기|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|읽기/쓰기|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|읽기 전용|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|읽기 전용|
|[Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md)*|읽기/쓰기|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|읽기/쓰기|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|always **adUseServer**|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|always **adOpenStatic**|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|always **adEditNone**|
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|읽기 전용|
|[Assert](../../../ado/reference/ado-api/filter-property.md)|읽기/쓰기|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|읽기/쓰기|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|사용할 수 없음|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|읽기/쓰기|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|읽기 전용|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|읽기/쓰기|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|읽기 전용|
|[원본](../../../ado/reference/ado-api/source-property-ado-recordset.md)|읽기/쓰기|
|[State](../../../ado/reference/ado-api/state-property-ado.md)|읽기 전용|
|[상태](../../../ado/reference/ado-api/status-property-ado-recordset.md)|읽기 전용|

 \*책갈피에 없거나이 기능에 대 한 순서로 공급자에서 사용할 수 있어야 합니다 **레코드 집합**합니다.

 **표준 ADO 레코드 집합 메서드 사용 가능:**

|메서드|사용 가능 여부|
|------------|----------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|아니요|
|[취소](../../../ado/reference/ado-api/cancel-method-ado.md)|사용자 계정 컨트롤|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|아니요|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|아니요|
|[복제](../../../ado/reference/ado-api/clone-method-ado.md)|사용자 계정 컨트롤|
|[닫기](../../../ado/reference/ado-api/close-method-ado.md)|사용자 계정 컨트롤|
|[Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|아니요|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|사용자 계정 컨트롤|
|[이동](../../../ado/reference/ado-api/move-method-ado.md)|사용자 계정 컨트롤|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|사용자 계정 컨트롤|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|사용자 계정 컨트롤|
|[파일](../../../ado/reference/ado-api/open-method-ado-recordset.md)|사용자 계정 컨트롤|
|[다시 쿼리](../../../ado/reference/ado-api/requery-method.md)|사용자 계정 컨트롤|
|[Resync](../../../ado/reference/ado-api/resync-method.md)|사용자 계정 컨트롤|
|[지원](../../../ado/reference/ado-api/supports-method.md)|사용자 계정 컨트롤|
|[Update](../../../ado/reference/ado-api/update-method.md)|아니요|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|아니요|

 특정 구현 세부 정보 및 Microsoft 인덱싱 서비스용 Microsoft OLE DB Provider에 대 한 기능 정보에 대 한 참조를 [OLE DB Programmer's Guide](https://msdn.microsoft.com/library/windows/desktop/ms713643.aspx), Windows NT Server 웹의 웹 서비스 페이지를 방문 또는 사이트입니다.

## <a name="see-also"></a>관련 항목
 [CommandType 속성 (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md) [ConnectionString 속성 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [공급자 속성 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [ 레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [메서드 지원](../../../ado/reference/ado-api/supports-method.md)
