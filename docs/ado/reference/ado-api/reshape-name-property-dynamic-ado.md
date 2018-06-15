---
title: 동적 속성 (ADO) 이름 만들기 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4752609469ecad3a3a6631584e120de8cc4a7575
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35281412"
---
# <a name="reshape-name-property-dynamic-ado"></a>동적 속성 (ADO) Name 모양 변경
에 대 한 이름을 지정는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다.  
  
## <a name="return-values"></a>반환 값  
 반환 된 **문자열** 값의 이름을 **레코드 집합**합니다.  
  
## <a name="remarks"></a>Remarks  
 동안 때까지 또는 연결의 이름을 유지는 **레코드 집합** 닫혀 있습니다.  
  
 **Name 모양 변경** 속성은 주로 다시 셰이핑의 함께 사용 된 [OLE DB에 대 한 Microsoft Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) 서비스 공급자입니다. 이름은 다시 모양 지정에 참여 하도록 고유 해야 합니다.  
  
 이 속성은 읽기 전용 이지만 설정할 수 있습니다 하지 직접 때는 **레코드 집합** 만들어집니다. 예를 들어 경우 절을 Shape 명령을 만듭니다는 **레코드 집합** 별칭 이름을 사용 하 여 제공 하 고는 **AS** 키워드, 별칭에 할당 된는 **Name 모양 변경** 속성입니다. 별칭이 없는 선언 된 경우는 **이름 변형** 속성 데이터를 셰이핑 서비스에 의해 생성 된 고유 이름이 할당 됩니다. 별칭 이름이 기존 이름과 동일한 경우 **레코드 집합**, 모두 **레코드 집합** 그 중 하나가 해제 될 때까지 모양을 변경할 수 있습니다. 고유한 이름을 설정 하 여 기본 동작을 변경할 수 있습니다는 [이름 변형](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md) 속성에 ADO 연결을 **True**합니다. 이 속성을 설정할 데이터 셰이핑 고유성을 보장 하기 위해 필요한 경우 할당 된 사용자 이름을 변경 하려면 서비스 권한을 제공 합니다. 모양 변경 하는 방법에 대 한 자세한 내용은 참조 [OLE DB (ADO 서비스 공급자)에 대 한 Microsoft Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)합니다.  
  
 사용 하 여는 **Name 모양 변경** 참조 하려는 경우이 속성을 **레코드 집합** Data Shaping Service에서 생성 되었으므로 이름을 알지 때나 Shape 명령입니다. 이 경우 명령에서 반환 된 문자열 앞뒤에 연결 하 여 SHAPE 명령을 생성할 수 있습니다는 **이름 변형** 속성입니다.  
  
 **이름 변형** 동적 속성에 추가 **레코드 집합** 개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션 때는 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성**adUseClient**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft 데이터를 셰이핑 OLE DB (ADO 서비스 공급자)에 대 한 서비스](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [일반적으로 shape 명령](../../../ado/guide/data/shape-commands-in-general.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
