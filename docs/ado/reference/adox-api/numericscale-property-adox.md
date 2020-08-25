---
description: NumericScale 속성(ADOX)
title: NumericScale 속성 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Column::PutNumericScale
- _Column::GetNumericScale
- _Column::NumericScale
- _Column::put_NumericScale
- _Column::get_NumericScale
helpviewer_keywords:
- NumericScale property [ADOX]
ms.assetid: 573ee5d1-57c7-4a27-be79-a0e12944ad9b
author: rothja
ms.author: jroth
ms.openlocfilehash: 3420a3e3d1e6ee06eaa63926604f3688b3f0590b
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769912"
---
# <a name="numericscale-property-adox"></a>NumericScale 속성(ADOX)
열에 있는 숫자 값의 소수 자릿수를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 [Type](./type-property-column-adox.md) 속성이 **Adnumeric** 또는 **adDecimal**인 경우 열에 있는 데이터 값의 소수 자릿수에 해당 하는 **바이트** 값을 설정 하 고 반환 합니다. 다른 모든 데이터 형식에 대해서는 **NumericScale** 이 무시 됩니다.  
  
## <a name="remarks"></a>설명  
 기본값은 영(0)입니다.  
  
 **NumericScale** 는 이미 컬렉션에 추가 된 [열](./column-object-adox.md) 개체에 대해 읽기 전용입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [열 개체(ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>참고 항목  
 [ADOX 코드 예제: NumericScale 및 Precision 속성 예제 (VB)](./adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Type 속성(열)(ADOX)](./type-property-column-adox.md)