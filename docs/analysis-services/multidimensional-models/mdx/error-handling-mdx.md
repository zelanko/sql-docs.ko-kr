---
title: 오류 처리 (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e7575a598342dfabd66bc15a8f67b3b8ca70f690
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
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
  
  
