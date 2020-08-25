---
description: 속성 개체(ADOX)
title: Property 개체 (ADOX) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 75a4722803e66527873f98fe469825d4af82ca33
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769542"
---
# <a name="property-object-adox"></a>속성 개체(ADOX)
ADOX 개체의 특징을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 ADOX 개체에는 기본 제공 및 동적 속성의 두 가지 유형이 있습니다.  
  
 기본 제공 속성은 MyObject 속성 구문을 사용 하 여 새 개체에 즉시 사용할 수 있는 속성입니다. 이러한 속성은 개체의 [속성 컬렉션](../ado-api/properties-collection-ado.md)에 속성 개체로 표시 되지 않으므로 해당 값을 변경할 수 있지만 특성을 수정할 수는 없습니다.  
  
 동적 속성은 기본 데이터 공급자에 의해 정의 되 고 해당 ADOX 개체의 Properties 컬렉션에 표시 됩니다.  동적 속성은 MyObject 속성 (0) 또는 MyObject 속성 ("Name") 구문을 사용 하 여 컬렉션을 통해서만 참조할 수 있습니다.  
  
 두 종류의 속성을 모두 삭제할 수는 없습니다.  
  
 동적 속성 개체에는 자체의 기본 제공 속성 4 개가 있습니다.  
  
 [Name](../ado-api/name-property-ado.md) 속성은 속성을 식별 하는 문자열입니다.  
  
 [Type](../ado-api/type-property-ado.md) 속성은 속성 데이터 형식을 지정 하는 정수입니다.  
  
 [Value](../ado-api/value-property-ado.md) 속성은 속성 설정을 포함 하는 변형입니다. Value는 속성 개체의 기본 속성입니다.  
  
 [Attributes](../ado-api/attributes-property-ado.md) 속성은 공급자와 관련 된 속성의 특징을 나타내는 long 값입니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [ADOX 속성 개체 속성, 메서드 및 이벤트](./adox-property-object-properties-methods-and-events.md)