---
description: Members 컬렉션(ADO MD)
title: Members 컬렉션 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
author: rothja
ms.author: jroth
ms.openlocfilehash: e0f12771ebb759a658d5e3c99244755c4daa99b0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986384"
---
# <a name="members-collection-ado-md"></a>Members 컬렉션(ADO MD)
수준 또는 축의 위치에서 [멤버](./member-object-ado-md.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 **Members** 컬렉션은 다음과 같은 멤버 유형을 포함 하는 데 사용 됩니다.  
  
-   큐브의 수준을 구성 하는 멤버입니다. 이러한 개체는 [수준](./level-object-ado-md.md) 개체의 **Members** 컬렉션에 포함 되어 있습니다. 예를 들어 [다차원 스키마 및 데이터 개요](../../guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)에서 샘플을 사용 하는 경우 국가 수준의 네 가지 구성원은 캐나다, USA, 영국 및 독일입니다.  
  
-   계층 내에 있는 특정 멤버의 자식인 멤버입니다. 이러한 멤버는 부모 **멤버** 개체의 [Children](./children-property-ado-md.md) 속성에 의해 반환 됩니다. 예를 들어 동일한 샘플을 다시 사용 하는 경우 캐나다 구성원의 두 자식은 캐나다 동부와 캐나다-서 부입니다.  
  
-   [셀 집합](./cellset-object-ado-md.md)의 축을 따라 특정 위치를 정의 하는 멤버입니다. 셀 집합을 사용 하 여 [다차원 데이터 작업](../../guide/multidimensional/working-with-multidimensional-data.md) 에서 x 축의 첫 번째 위치에 있는 두 멤버는 발렌타인 및 시애틀입니다. 이러한 멤버는 [Position](./position-object-ado-md.md) 개체의 **members** 컬렉션에 포함 됩니다.  
  
 **멤버** 는 표준 ADO 컬렉션입니다. 컬렉션의 속성과 메서드를 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Count](../ado-api/count-property-ado.md) 속성을 사용 하 여 컬렉션의 개체 수를 가져옵니다.  
  
-   기본 [항목](../ado-api/item-property-ado.md) 속성을 사용 하 여 컬렉션에서 개체를 반환 합니다.  
  
-   [Refresh](../ado-api/refresh-method-ado.md) 메서드를 사용 하 여 공급자에서 컬렉션의 개체를 업데이트 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [속성, 메서드 및 이벤트](./members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Members 예제 (VBScript)](./members-example-vbscript.md)   
 [Member 개체(ADO MD)](./member-object-ado-md.md)