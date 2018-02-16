---
title: "오류 처리 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f612a88976890a95b8fbd3d28826685d0e4ef414
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="error-handling-mdx"></a>오류 처리(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
MDX 스크립트의 오류가 처리되는 방법을 각 큐브에서 제어할 수 있습니다. 오류 처리는 **ScriptErrorHandlingMode** 열거자를 통해 수행됩니다. 이 열거자에 사용할 수 있는 값은 다음과 같습니다.  
  
 **IgnoreNone**  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 가 MDX 스크립트에서 오류를 발견하면 서버가 오류를 발생시킵니다.  
  
 **IgnoreAll**  
 구문 오류, 이름 확인 오류 등을 포함하는 MDX 스크립트 내의 모든 명령을 서버가 무시하도록 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
