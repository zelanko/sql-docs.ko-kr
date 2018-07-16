---
title: 오류 처리 (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
caps.latest.revision: 26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bbbe021cbb65803f79a4aa0a92791441e22e9cb6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37332683"
---
# <a name="error-handling-mdx"></a>오류 처리(MDX)
  MDX 스크립트의 오류가 처리되는 방법을 각 큐브에서 제어할 수 있습니다. 오류 처리를 통해 수행 됩니다는 `ScriptErrorHandlingMode` 열거자입니다. 이 열거자에 사용할 수 있는 값은 다음과 같습니다.  
  
 `IgnoreNone`  
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 가 MDX 스크립트에서 오류를 발견하면 서버가 오류를 발생시킵니다.  
  
 `IgnoreAll`  
 구문 오류, 이름 확인 오류 등을 포함하는 MDX 스크립트 내의 모든 명령을 서버가 무시하도록 합니다.  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
