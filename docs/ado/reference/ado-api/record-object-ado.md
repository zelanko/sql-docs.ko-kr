---
title: 개체 (ADO) 레코드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Record
helpviewer_keywords:
- Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 859bf3f53051a500e86742cb681885b8067f6a0c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712220"
---
# <a name="record-object-ado"></a>레코드 개체(ADO)
행을 나타내며를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 데이터 공급자 또는 파일 또는 디렉터리와 같은 반 구조화 된 데이터 공급자를 반환 하는 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 A **레코드** 개체는 데이터의 한 행을 나타냅니다 있고 한 행을 사용 하 여 개념적 느낄 **Recordset**합니다. 공급자 기능에 따라 **레코드** 개의 행 대신 공급자에서 직접 개체를 반환할 수 있습니다 **Recordset**예를 들어 경우 하나의 행을 선택 하는 SQL 쿼리, 실행 합니다. 또는, **레코드** 에서 직접 개체를 얻을 수는 **Recordset** 개체입니다. 또는, **레코드** Microsoft Exchange OLE DB 공급자와 같은 반 구조화 된 데이터 공급자에서 직접 반환 될 수 있습니다.  
  
 와 연결 된 필드를 볼 수는 **레코드** 의 방식으로 개체를 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에는 **레코드** 개체입니다. ADO 포함 하 여 개체 반환 열 수 있습니다 **레코드 집합**를 **SafeArray**, 및에서 스칼라 값을 **필드** 컬렉션 **레코드** 개체입니다.  
  
 경우는 **레코드** 개체의 행을 나타냅니다를 **레코드 집합**에 원본에 반환할 수 **레코드 집합** 사용 하 여를 [원본](../../../ado/reference/ado-api/source-property-ado-record.md) 속성입니다.  
  
 **레코드** 개체도 사용할 수 반 구조화 된 데이터 공급자와 같은 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md), 네임 스페이스 트리 구조를 모델링 합니다. 트리의 각 노드는 **레코드** 관련된 열이 있는 개체입니다. 열 특성을 해당 노드 및 기타 관련 정보를 나타낼 수 있습니다. 합니다 **레코드** 개체 트리 구조에서 리프가 아닌 노드 및 리프 노드를 나타낼 수 있습니다. 리프가 아닌 노드에 다른 노드 콘텐츠를 갖지만 리프 노드에 이러한 콘텐츠는 없습니다. 리프 노드는 일반적으로 이진 데이터 스트림이 포함 및 리프가 아닌 노드에 연결 하는 기본 이진 스트림이 있을 수도 있습니다. 속성을 **레코드** 개체 노드의 형식을 식별 합니다.  
  
 합니다 **레코드** 탐색 계층적으로 구성 된 데이터에 대 한도 개체 대체 방법을 나타냅니다. A **레코드** 큰 트리 구조에서 특정 하위 트리의 루트 나타내기 위해 생성 되 고 새 개체 수 있습니다 **레코드** 자식 노드를 나타내는 개체를 열 수 있습니다.  
  
 절대 URL에서 리소스 (예: 파일 또는 디렉터리)를 고유 하 게 식별할 수 있습니다. A [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체가 암시적으로 생성 되 고로 설정 합니다 **레코드** 개체 때를 **레코드** 절대 URL을 사용 하 여 합니다. A **연결** 개체 명시적으로 설정할 수 있습니다 합니다 **레코드** 를 통해 개체를 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성. 파일 및 디렉터리를 사용 하 여 액세스할 수 있는 **연결** 개체를 정의 합니다 *상황에 맞는* 는 **레코드** 작업이 발생할 수 있습니다.  
  
 데이터 수정 및 탐색 메서드를 합니다 **레코드** 개체는 또한 절대 URL을 사용 하 여 리소스를 찾습니다는 상대 URL 허용 또는 **연결** 시작 지점으로 개체 컨텍스트.  
  
> [!NOTE]
>  Http 체계를 사용 하 여 Url은 자동으로 호출 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
 A **연결** 개체가 연결 된 각 **레코드** 개체입니다. 따라서 **레코드** 개체 작업은 호출 하 여 트랜잭션의 일부일 수 **연결** 트랜잭션 메서드 개체입니다.  
  
 합니다 **레코드** 개체는 ADO 이벤트를 지원 하지 않으며 따라서 알림에 응답 하지 것입니다.  
  
 메서드 및 속성을 사용 하 여는 **레코드** 개체를 다음을 수행할 수 있습니다.  
  
-   설정 하거나 연결 된 반환 **연결** 개체를 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성입니다.  
  
-   사용 하 여 액세스 권한을 표시 합니다 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 속성입니다.  
  
-   디렉터리의 URL을 반환 하 여 표시 되는 리소스를 포함 하는 경우는 **레코드** 사용 하 여 합니다 [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) 속성입니다.  
  
-   상대 URL을 절대 URL을 나타내는 또는 **레코드 집합** 올를 **레코드** 사용 하 여 파생 되는 [원본](../../../ado/reference/ado-api/source-property-ado-record.md) 속성입니다.  
  
-   현재 상태를 나타내는 합니다 **레코드** 사용 하 여 합니다 [상태](../../../ado/reference/ado-api/state-property-ado.md) 속성입니다.  
  
-   유형을 나타냅니다 **레코드** - *단순*를 *컬렉션*, 또는 *구조화 된 문서* -는 [ RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)속성입니다.  
  
-   사용 하 여 비동기 작업의 실행을 중지 합니다 [취소](../../../ado/reference/ado-api/cancel-method-ado.md) 메서드.  
  
-   연결 해제 합니다 **레코드** 사용 하 여 데이터 원본에서 합니다 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 메서드.  
  
-   파일 또는 디렉터리를 나타내는 복사를 **레코드** 사용 하 여 다른 위치에는 [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) 메서드.  
  
-   파일 또는 디렉터리와 하위 디렉터리를 나타내는 삭제를 **레코드** 사용 하 여 합니다 [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md) 메서드.  
  
-   열기를 **레코드 집합** 나타내는 엔터티의 파일과 하위 디렉터리를 나타내는 행을 포함 하는 **레코드** 사용 하 여는 [GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md) 메서드.  
  
-   이동 (이름 바꾸기) 파일 또는 디렉터리와 하위 디렉터리를 나타내는 **레코드** 사용 하 여 다른 위치에는 [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) 메서드.  
  
-   연결 된 **레코드** 기존 데이터를 사용 하 여 소스 또는 새 파일 또는 디렉터리를 만듭니다를 [열기](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드.  
  
 합니다 **레코드** 개체가 스크립팅 작업에 안전 합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [Record 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [필드 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [레코드 및 스트림](../../../ado/guide/data/records-and-streams.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
