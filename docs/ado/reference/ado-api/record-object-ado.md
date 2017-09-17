---
title: "개체 (ADO) 레코드 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Record
helpviewer_keywords:
- Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 26840ff89f61bc3c37cee2fd88c1f53e393528bf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="record-object-ado"></a>Record 개체 (ADO)
행을 나타냅니다는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) , 데이터 공급자 또는 파일 또는 디렉터리와 같은 반 구조화 된 데이터 공급자를 반환 하는 개체입니다.  
  
## <a name="remarks"></a>주의  
 A **레코드** 개체의 데이터를 한 행을 나타내며 한 행으로 개념적 비슷하지만 몇 **레코드 집합**합니다. 공급자 기능에 따라 **레코드** 한 행 대신 공급자에서 직접 개체를 반환할 수 있습니다 **레코드 집합**, 예를 들어 경우 하나의 행을 선택 하는 SQL 쿼리 실행 됩니다. 또는, **레코드** 에서 직접 개체를 가져올 수는 **레코드 집합** 개체입니다. 또는, **레코드** 반 구조화 된 데이터를 Microsoft Exchange OLE DB 공급자와 같은 공급자에서 직접 반환 될 수 있습니다.  
  
 와 연결 된 필드를 볼 수는 **레코드** 개체는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에는 **레코드** 개체입니다. ADO를 포함 하는 개체 값 열을 사용 하면 **레코드 집합**, **SafeArray**, 및에서 스칼라 값의 **필드** 컬렉션 **레코드** 개체입니다.  
  
 경우는 **레코드** 개체의 행을 나타냅니다는 **레코드 집합**, 즉 원래에 반환할 수 **레코드 집합** 와 [소스](../../../ado/reference/ado-api/source-property-ado-record.md) 속성입니다.  
  
 **레코드** 개체 사용할 수도 있습니다 반 구조화 된 데이터 공급자와 같은 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md), 트리 구조 네임 스페이스를 모델링할 수 있습니다. 트리의 각 노드는 한 **레코드** 관련된 열이 있는 개체입니다. 열 특성을 해당 노드 및 기타 관련 정보를 나타낼 수 있습니다. **레코드** 개체는 리프 노드 및 비-리프 노드는 트리 구조의 모두 나타낼 수 있습니다. 비-리프 노드에 해당 콘텐츠를 다른 노드가 있지만 리프 노드가 포함 되지 않습니다. 리프 노드에 일반적으로 이진 데이터 스트림이 포함 있으며 리프가 아닌 노드 수 연관 하는 기본 이진 스트림이 수도 있습니다. 속성에는 **레코드** 개체 유형의 노드를 식별 합니다.  
  
 **레코드** 탐색 계층적으로 구성 된 데이터에 대 한도 개체는 다른 방법으로 나타냅니다. A **레코드** 개체 수 있습니다. 큰 트리 구조에서 특정 하위 트리의 루트 나타내기 위해 만든 새 **레코드** 자식 노드를 나타내는 개체를 열 수 있습니다.  
  
 절대 url (예를 들어 파일 또는 디렉터리) 리소스를 고유 하 게 식별할 수 있습니다. A [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체가 암시적으로 생성 되 고로 설정 된 **레코드** 개체 때는 **레코드** 절대 URL을 사용 하 여 합니다. A **연결** 개체로 명시적으로 설정할 수 있습니다는 **레코드** 통해 개체는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성입니다. 파일 및 디렉터리를 사용 하 여 액세스할 수 있는 **연결** 개체 정의 *컨텍스트* 는 **레코드** 작업이 발생할 수 있습니다.  
  
 데이터 수정 및 탐색 메서드를는 **레코드** 개체 변수도 절대 URL을 사용 하 여 리소스를 찾습니다는 상대 URL 또는 **연결** 시작 지점으로 개체 컨텍스트에서 합니다.  
  
> [!NOTE]
>  Url은 http 체계를 사용 하 여 자동으로 호출 됩니다는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 참조 [절대 경로 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
 A **연결** 개체가 각각와 연결 된 **레코드** 개체입니다. 따라서 **레코드** 개체 작업은 호출 하 여 트랜잭션의 일부일 수 **연결** 트랜잭션 메서드 개체입니다.  
  
 **레코드** 개체는 ADO 이벤트를 지원 하지 않으며 따라서 알림 응답 하지 것입니다.  
  
 메서드 및 속성을 사용 하 여 한 **레코드** 개체를 다음을 수행할 수 있습니다.  
  
-   설정 하거나 반환할 연결 된 **연결** 개체는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성입니다.  
  
-   사용 하는 액세스 권한을 나타냅니다는 [모드](../../../ado/reference/ado-api/mode-property-ado.md) 속성입니다.  
  
-   디렉터리의 URL을 반환 하 여 표시 되는 리소스를 포함 하는 있는 경우는 **레코드** 와 [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) 속성입니다.  
  
-   절대 URL 상대 URL을 나타내는 또는 **레코드 집합** 입니다는 **레코드** 으로 파생 되는 [소스](../../../ado/reference/ado-api/source-property-ado-record.md) 속성입니다.  
  
-   현재 상태를 나타내는 **레코드** 와 [상태](../../../ado/reference/ado-api/state-property-ado.md) 속성입니다.  
  
-   유형을 지정 **레코드** - *간단한*, *컬렉션*, 또는 *구조적된 문서* -와 [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)속성입니다.  
  
-   포함 된 비동기 작업의 실행을 중지는 [취소](../../../ado/reference/ado-api/cancel-method-ado.md) 메서드.  
  
-   한 연결을 끊을 **레코드** 사용 데이터 원본에서의 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 메서드.  
  
-   파일 또는 디렉터리를 나타내는 복사는 **레코드** 와 함께 다른 위치로 [범위란](../../../ado/reference/ado-api/copyrecord-method-ado.md) 메서드.  
  
-   파일 또는 디렉터리와 하위 디렉터리를 나타내는 삭제는 **레코드** 와 [참여할 수 있는](../../../ado/reference/ado-api/deleterecord-method-ado.md) 메서드.  
  
-   열기는 **레코드 집합** 가 나타내는 엔터티 파일과 하위 디렉터리를 나타내는 행을 포함 하는 **레코드** 와 [GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md) 메서드.  
  
-   이동 (rename) 파일 또는 디렉터리와 하위 디렉터리를 나타내는 **레코드** 와 함께 다른 위치로 [범위란](../../../ado/reference/ado-api/moverecord-method-ado.md) 메서드.  
  
-   연결의 **레코드** 기존 데이터와 원본 또는 새 파일 또는 디렉터리를 만들는 [열려](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드.  
  
 **레코드** 개체는 스크립팅 작업에 안전 합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [Record 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Fields 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [레코드 및 스트림](../../../ado/guide/data/records-and-streams.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
