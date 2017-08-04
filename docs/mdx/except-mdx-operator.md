---
title: "- (제외) (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '-'
dev_langs:
- kbMDX
helpviewer_keywords:
- Except operator [MDX]
- '- (except operator)'
ms.assetid: 8971a09d-b254-4c4c-a099-103664783589
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d06de38c64dda440d04d49c498653bcb52f8c6fa
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="except-mdx-operator"></a>(MDX) 연산자를 제외 하 고
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  중복된 멤버를 제거하고 두 집합 간의 차집합을 반환하는 집합 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set_Expression - Set_Expression  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 지정된 두 매개 변수에서 공유되지 않는 멤버가 포함된 집합입니다.  
  
## <a name="remarks"></a>주의  
 **-(제외)** 연산자는 기능적으로 동일는 [제외한](../mdx/except-mdx-function.md) 함수입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 이 연산자의 사용 방법을 보여 줍니다.  
  
```  
// This query shows the quantity of orders for all product categories  
// with the exception of Components.  
SELECT   
   [Measures].[Order Quantity] ON COLUMNS,  
   [Product].[Product Categories].[All].Children   
   - [Product].[Product Categories].[Components] ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 연산자 참조 &#40; Mdx&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

