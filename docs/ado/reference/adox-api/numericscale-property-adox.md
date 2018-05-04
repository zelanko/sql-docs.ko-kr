---
title: NumericScale 속성 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fdf5ce61c1be2940b289fc188c9d01123aeffd48
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="numericscale-property-adox"></a>NumericScale 속성 (ADOX)
열에 숫자 값의 소수 자릿수를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하 고 반환 된 **바이트** 열에 있는 데이터 값의 소수 자릿수 값 때는 [형식](../../../ado/reference/adox-api/type-property-column-adox.md) 속성은 **adNumeric** 또는 **adDecimal**합니다. **NumericScale** 다른 모든 데이터 형식에 대해 무시 됩니다.  
  
## <a name="remarks"></a>주의  
 기본값은 영 (0).  
  
 **NumericScale** 는 대 한 읽기 전용 [열](../../../ado/reference/adox-api/column-object-adox.md) 컬렉션에 이미 추가 된 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Column 개체(ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ADOX 코드 예: NumericScale 및 전체 자릿수 속성 예제 (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [Type 속성(열)(ADOX)](../../../ado/reference/adox-api/type-property-column-adox.md)
