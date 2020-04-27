---
title: Record 개체 (ADO) | Microsoft Docs
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
ms.openlocfilehash: 5ffc515350bfff4307da382c05aae50ed1930802
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917366"
---
# <a name="record-object-ado"></a>레코드 개체(ADO)
파일이 나 디렉터리와 같이 반 구조화 된 데이터 공급자가 반환 하는 개체 또는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 또는 데이터 공급자의 행을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 **Record** 개체는 하나의 데이터 행을 나타내며 단일 행 **레코드 집합과**개념적인 유사성을 갖습니다. 공급자의 기능에 따라 행을 하나만 선택 하는 SQL 쿼리가 실행 되는 경우와 같이 한 행의 레코드 **집합**대신 공급자에서 직접 **Record** 개체가 반환 될 수도 있습니다. 또는 **레코드** 개체를 레코드 **집합** 개체에서 직접 가져올 수 있습니다. 또는 공급자에서 Microsoft Exchange OLE DB 공급자와 같은 반 구조화 된 데이터로 직접 **레코드** 를 반환할 수 있습니다.  
  
 Record **개체의** [fields](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션을 통해 **record** 개체와 연결 된 필드를 볼 수 있습니다. ADO에서는 **Record** 개체의 **Fields** 컬렉션에서 **레코드 집합**, **SafeArray**및 스칼라 값을 포함 하는 개체 반환 열을 사용할 수 있습니다.  
  
 **Record** 개체가 레코드 **집합**의 행을 나타내는 경우 [원본](../../../ado/reference/ado-api/source-property-ado-record.md) 속성을 사용 하 여 해당 원본 **레코드 집합** 으로 돌아갈 수 있습니다.  
  
 [Microsoft OLE DB 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)와 같은 반 구조화 된 데이터 공급자가 **Record** 개체를 사용 하 여 트리 구조 네임 스페이스를 모델링할 수도 있습니다. 트리의 각 노드는 연결 된 열이 있는 **Record** 개체입니다. 열은 해당 노드의 특성과 기타 관련 정보를 나타낼 수 있습니다. **Record** 개체는 트리 구조에서 리프 노드와 리프가 아닌 노드를 모두 나타낼 수 있습니다. 리프가 아닌 노드는 다른 노드를 콘텐츠로 갖지만 리프 노드에는 이러한 내용이 없습니다. 리프 노드에는 일반적으로 데이터의 이진 스트림이 포함 되 고 리프가 아닌 노드에는 기본 이진 스트림도 연결 되어 있을 수 있습니다. **Record** 개체의 속성은 노드 유형을 식별 합니다.  
  
 **Record** 개체는 계층적으로 구성 된 데이터를 탐색 하는 다른 방법을 나타냅니다. 대량 트리 구조에서 특정 하위 트리의 루트를 나타내는 **record** 개체를 만들 수 있으며, 자식 노드를 나타내기 위해 새 **record** 개체가 열릴 수 있습니다.  
  
 리소스 (예: 파일 또는 디렉터리)는 절대 URL로 고유 하 게 식별할 수 있습니다. 절대 URL을 사용 하 여 **레코드** 를 열 때 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체가 암시적으로 생성 되 고 **record** 개체로 설정 됩니다. **Connection** 개체는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성을 통해 **Record** 개체에 명시적으로 설정할 수 있습니다. **연결** 개체를 사용 하 여 액세스할 수 있는 파일 및 디렉터리는 **레코드** 작업이 발생할 수 있는 *컨텍스트* 를 정의 합니다.  
  
 **Record** 개체의 데이터 수정 및 탐색 메서드에도 절대 Url 또는 **연결** 개체 컨텍스트를 시작 점으로 사용 하 여 리소스를 찾는 상대 url을 사용할 수 있습니다.  
  
> [!NOTE]
>  Http 체계를 사용 하는 Url은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
 **연결** 개체는 각 **Record** 개체와 연결 됩니다. 따라서 **Record** 개체 작업은 **연결** 개체 트랜잭션 메서드를 호출 하 여 트랜잭션의 일부일 수 있습니다.  
  
 **Record** 개체는 ADO 이벤트를 지원 하지 않기 때문에 알림에 응답 하지 않습니다.  
  
 **Record** 개체의 메서드 및 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성을 사용 하 여 연결 된 **연결** 개체를 설정 하거나 반환 합니다.  
  
-   [Mode](../../../ado/reference/ado-api/mode-property-ado.md) 속성을 사용 하 여 액세스 권한을 표시 합니다.  
  
-   [Parenturl](../../../ado/reference/ado-api/parenturl-property-ado.md) 속성을 사용 하 여 **레코드가** 나타내는 리소스를 포함 하는 디렉터리의 URL (있는 경우)을 반환 합니다.  
  
-   [원본](../../../ado/reference/ado-api/source-property-ado-record.md) 속성을 사용 하 여 **레코드가** 파생 되는 절대 url, 상대 url 또는 **레코드 집합** 을 표시 합니다.  
  
-   [상태](../../../ado/reference/ado-api/state-property-ado.md) 속성을 사용 하 여 **레코드** 의 현재 상태를 표시 합니다.  
  
-   [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)속성을 사용 하 여*단순*, *컬렉션*또는 *구조화 된 문서* **레코드** - 의 유형을 지정 합니다.  
  
-   [Cancel](../../../ado/reference/ado-api/cancel-method-ado.md) 메서드를 사용 하 여 비동기 작업의 실행을 중지 합니다.  
  
-   [Close](../../../ado/reference/ado-api/close-method-ado.md) 메서드를 사용 하 여 데이터 소스에서 **레코드** 를 분리 합니다.  
  
-   **레코드가** 나타내는 파일이 나 디렉터리를 [copyrecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) 메서드를 사용 하 여 다른 위치로 복사 합니다.  
  
-   [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md) 메서드를 사용 하 여 **레코드로** 표시 되는 파일, 디렉터리 및 하위 디렉터리를 삭제 합니다.  
  
-   [Getchildren](../../../ado/reference/ado-api/getchildren-method-ado.md) 메서드를 사용 하 여 **레코드가** 나타내는 엔터티의 하위 디렉터리 및 파일을 나타내는 행이 포함 된 **레코드 집합** 을 엽니다.  
  
-   [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) 메서드를 사용 하 여 **레코드로** 표시 되는 파일, 디렉터리 및 하위 디렉터리를 다른 위치로 이동 (이름 바꾸기) 합니다.  
  
-   기존 데이터 원본에 **레코드** 를 연결 하거나 [Open](../../../ado/reference/ado-api/open-method-ado-record.md) 메서드로 새 파일이 나 디렉터리를 만듭니다.  
  
 **Record** 개체는 스크립팅에 안전 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Record 개체 속성, 메서드 및 이벤트](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Fields 컬렉션 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties 컬렉션 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [레코드 및 스트림](../../../ado/guide/data/records-and-streams.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
