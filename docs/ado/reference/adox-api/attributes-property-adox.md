---
description: Attributes 속성(ADOX)
title: Attributes 속성 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::put_Attributes
- _Column::Attributes
- _Column::PutAttributes
- _Column::get_Attributes
- _Column::GetAttributes
helpviewer_keywords:
- Attributes property [ADOX]
ms.assetid: e3abb359-79a3-4c22-b3a8-2900817e0d23
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f4843dd8ad51f79a178df422ff1a3a3e58a8e94
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985324"
---
# <a name="attributes-property-adox"></a>Attributes 속성(ADOX)
열 특징을 설명 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **Long** 값을 설정 하거나 반환 합니다. [열](./column-object-adox.md) 개체가 나타내는 테이블의 특징을 지정 하는 값입니다. 값은 [ColumnAttributesEnum](./columnattributesenum.md) 상수를 조합 하 여 사용할 수 있습니다. 기본값은 영 (**0**)으로, **adcolfixed** 또는 **adcolfixed**이 아닙니다.  
  
## <a name="applies-to"></a>적용 대상  
  
- [열 개체(ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [Attributes 속성 예제(VB)](./attributes-property-example-vb.md)