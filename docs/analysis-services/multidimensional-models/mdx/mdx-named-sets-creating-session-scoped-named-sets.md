---
title: 명명 된 집합 (MDX) 세션 범위 만들기 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fdf177cedcd73069e73c1ec7b4c7db5cfb497969
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-named-sets---creating-session-scoped-named-sets"></a>명명 된 집합에서 만드는 세션 범위 MDX 명명 된 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  MDX 세션에서 사용할 수 있는 명명된 집합을 만들려면 [CREATE SET](../../../mdx/mdx-data-definition-create-set.md) 문을 사용하세요. CREATE SET 문으로 작성한 명명된 집합은 MDX 세션이 종료된 뒤에도 제거되지 않습니다.  
  
 이 항목에서 설명되겠지만 WITH 키워드의 구문은 간단하며 사용하기 쉽습니다.  
  
> [!NOTE]  
>  명명된 집합에 대한 자세한 내용은 [명명된 집합을 MDX로 작성&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md)을 참조하세요.  
  
## <a name="create-set-syntax"></a>CREATE SET 구문  
 CREATE SET 문의 구문은 다음과 같습니다.  
  
```  
CREATE SESSION SET [CURRENTCUBE. | <cube name>.]<Set Identifier> AS <Set Expression>  
```  
  
 CREATE SET 구문에서 `cube name` 매개 변수는 명명된 집합의 멤버를 포함하는 큐브의 이름을 포함합니다. `cube name` 매개 변수를 지정하지 않으면 명명된 집합의 멤버를 포함하는 큐브로 현재 큐브를 사용합니다. 또한 `Set_Identifier` 매개 변수는 명명된 집합의 별칭을 포함하며 `Set_Expression` 매개 변수는 명명된 집합 별칭이 참조할 집합 식을 포함합니다.  
  
## <a name="create-set-example"></a>CREATE SET 예  
 다음 예에서는 CREATE SET 문을 사용하여 Store 큐브를 바탕으로 `SetCities_2_3` 으로 명명된 집합을 만듭니다. City 2 및 City 3의 상점이 `SetCities_2_3` 으로 명명된 집합의 멤버가 됩니다.  
  
```  
create Session set [Store].[SetCities_2_3] as  
{[Data Stores].[ByLocation].[State].&[CA].&[City 02],  
[Data Stores].[ByLocation].[State].&[NH].&[City 03]}  
```  
  
 CREATE SET 문을 사용하여 정의한 `SetCities_2_3` 명명된 집합은 현재 MDX 세션이 유지되는 동안 사용할 수 있습니다. 다음 예는 City 2 및 City 3 멤버를 반환하는 유효한 쿼리이며 `SetCities_2_3` 으로 명명된 집합을 만든 뒤 세션을 종료하기 전까지 언제든지 실행할 수 있습니다.  
  
```  
select SetCities_2_3 on 0 from [Store]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [세트 & #40; 명명 된 쿼리 범위를 만들기 Mdx& #41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md)  
  
  
