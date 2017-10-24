---
title: "오류 처리 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bbd604d132fa204da606b44d72551f198661c81a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="error-handling-mdx"></a>오류 처리(MDX)
  MDX 스크립트의 오류가 처리되는 방법을 각 큐브에서 제어할 수 있습니다. 오류 처리는 **ScriptErrorHandlingMode** 열거자를 통해 수행됩니다. 이 열거자에 사용할 수 있는 값은 다음과 같습니다.  
  
 **IgnoreNone**  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 가 MDX 스크립트에서 오류를 발견하면 서버가 오류를 발생시킵니다.  
  
 **IgnoreAll**  
 구문 오류, 이름 확인 오류 등을 포함하는 MDX 스크립트 내의 모든 명령을 서버가 무시하도록 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  

