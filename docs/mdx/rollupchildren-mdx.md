---
title: RollupChildren (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ROLLUPCHILDREN
dev_langs:
- kbMDX
helpviewer_keywords:
- RollupChildren function
ms.assetid: 6f092540-067d-443f-b631-8523836a0d86
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 7493a809e9856743422421d61e6f7d1bcdd99ea6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="rollupchildren-mdx"></a>RollupChildren(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  지정한 단항 연산자를 통해 지정한 멤버의 자식 항목 값을 롤업하여 생성된 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
RollupChildren(Member_Expression, Unary_Operator)   
```  
  
## <a name="arguments"></a>인수  
 *Member_Expression*  
 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Unary_Operator*  
 단항 연산자를 지정하는 유효한 문자열 식입니다.  
  
## <a name="remarks"></a>주의  
 **RollupChildren** 함수는 지정 된 단항 연산자를 사용 하 여 지정된 된 멤버의 자식 값을 롤업 합니다.  
  
 다음은 이 함수에 대해 유효한 단항 연산자입니다.  
  
|연산자|결과|  
|--------------|------------|  
|**+**|합계 = 합계 + 현재 자식 항목|  
|**-**|합계 = 합계 - 현재 자식 항목|  
|**\***|합계 = 합계 * 현재 자식 항목|  
|**/**|합계 = 합계 / 현재 자식 항목|  
|**%**|합계 = (합계 / 현재 자식 항목) * 100|  
|**~**|자식 항목을 롤업에 사용하지 않습니다. 해당 값이 무시됩니다.|  
  
 위 목록에 표시되지 않은 멤버 속성의 연산자를 사용하면 오류가 발생합니다. 계산 순서는 연산자의 선행 규칙이 아닌 형제 항목의 순서에 따라 결정됩니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 대체 방법으로 단항 연산자의 대체 값이 들어 있는 "Alternate Rollup Operator"라는 멤버 속성을 사용하여 Account 차원에 있는 Net Profit 계층의 자식을 롤업합니다. 이 멤버 속성은 Adventure Works 큐브에는 없지만 만들 수 있습니다. 이러한를 사용이 하 여 **RollupChildren** 가상 분석을 위한 예산 응용 프로그램에서 함수를 사용할 수 없습니다.  
  
```  
RollupChildren  
   ( [Account].[Net Profit]  
   , [Account].CurrentMember.Properties ('Alternate Rollup Operator') )  
```  
  
## <a name="see-also"></a>관련 항목:  
 [MDX 함수 참조 & #40; Mdx& #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
