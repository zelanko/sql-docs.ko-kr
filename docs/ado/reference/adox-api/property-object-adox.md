---
title: 속성 개체 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Property object [ADOX]
ms.assetid: 6a56def6-dbe6-4ccc-a491-8d076889f019
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2f07d14d30f3fd87be8fc61552716a931ed86d68
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705956"
---
# <a name="property-object-adox"></a>속성 개체(ADOX)
ADOX 개체의 특성을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 ADOX 개체에는 두 가지 유형의 속성: 기본 제공 및 동적입니다.  
  
 기본 제공 속성은 해당 속성을 즉시 MyObject.Property 구문을 사용 하 여 모든 새 개체를 사용할 수 있습니다. 개체의 속성 개체로 표시 되지 않습니다 [속성 컬렉션](../../../ado/reference/ado-api/properties-collection-ado.md)이므로 해당 값을 변경할 수 있지만 해당 특성을 수정할 수 없습니다.  
  
 동적 속성은 기본 데이터 공급자가 정의 된 및 적절 한 ADOX 개체에 대 한 속성 컬렉션에 표시 합니다.  동적 속성 MyObject.Properties(0) 또는 MyObject.Properties("Name") 구문을 사용 하 여 컬렉션을 통해서만 참조할 수 있습니다.  
  
 두 가지 속성을 삭제할 수 없습니다.  
  
 동적 속성 개체에는 자체의 네 가지 기본 제공 속성:  
  
 합니다 [이름을](../../../ado/reference/ado-api/name-property-ado.md) 속성은 속성을 식별 하는 문자열입니다.  
  
 합니다 [형식](../../../ado/reference/ado-api/type-property-ado.md) 속성은 속성 데이터 형식을 지정 하는 정수입니다.  
  
 합니다 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성이 속성 설정이 포함 된 변형입니다. 값은 속성 개체에 대 한 기본 속성입니다.  
  
 합니다 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성은 공급자와 관련 된 속성의 특성을 나타내는 long 값입니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [ADOX Property 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/adox-property-object-properties-methods-and-events.md)
