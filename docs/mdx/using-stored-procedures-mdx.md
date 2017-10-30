---
title: "저장된 프로시저 (MDX)를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- user-defined functions [MDX]
- stored procedures [MDX]
ms.assetid: 818fb2ad-f88b-4d0c-9f70-f378aed42e8e
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2c24641d2be7e4e2130d21881b94a9bcd1698fd7
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="using-stored-procedures-mdx"></a>저장 프로시저 사용(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  .NET 저장 프로시저 또는 사용자 정의 함수를 작성하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 및 MDX(Multidimensional Expressions)의 기능을 확장할 수 있습니다. 자세한 내용은 참조 [ADOMD.NET 서버 프로그래밍](../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
 저장 프로시저를 참조하거나 호출할 때는 함수 이름 뒤에 괄호를 지정합니다. 괄호 안에는 매개 변수로 전달할 데이터를 제공하는 식(인수)을 지정할 수 있습니다. 함수를 호출할 때는 모든 괄호에 대해 인수 값을 제공해야 하며 사용자 정의 함수에서 매개 변수가 정의된 순서와 같은 순서로 인수 값을 지정해야 합니다.  
  
 다음 예제 쿼리에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버에 SampleAssembly라는 어셈블리가 등록되어 있다고 가정합니다.  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
> [!NOTE]  
>  *저장 프로시저* 에 사용 되는 용어는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 이런이 유형의 함수에 대 한 합니다. 이전 버전의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 이러한 유형의 함수를 호출 *사용자 정의 함수*합니다.  
  
## <a name="types-of-stored-procedures"></a>저장 프로시저 유형  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]는 COM 및 CLR 어셈블리를 모두 지원합니다. CLR 어셈블리에 적용되는 향상된 보안 기능 때문에 CLR 어셈블리를 권장합니다. 서버에 Microsoft Office Excel이 설치되어 있으면 Excel 기능도 사용할 수 있습니다.  
  
> [!NOTE]  
>  Microsoft VBA(Visual Basic for Applications) COM 어셈블리는 자동으로 등록됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [함수 &#40; MDX 구문 &#41;](../mdx/functions-mdx-syntax.md)  
  
  

