---
title: 새&#39;s (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5562b7424e4a104204becaed10378ffc999c4e98
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68891111"
---
# <a name="what39s-new-integration-services"></a>새&#39;s (Integration Services)
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 이전 릴리스에서 변경 되지 않았습니다.  
  
 다른 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 제품 및 기술에 대 한 자세한 내용은 [SQL Server 2014의 새로운 기능](../sql-server/what-s-new-in-sql-server-2016.md)을 참조 하세요.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 비즈니스 인텔리전스와 관련 된 변경 내용에 대 한 자세한 내용은 [Analysis Services 및 비즈니스 인텔리전스의 새로운 기능](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)을 참조 하세요.  
  
##  <a name="rich-xml-validation-output-in-the-xml-task"></a><a name="ValidateXML"></a> XML 태스크에서 풍부한 XML 유효성 검사 출력  
 XML 태스크의 `ValidationDetails` 속성을 사용하도록 설정하여 XML 문서의 유효성을 검사하고 풍부한 오류 출력을 가져올 수 있습니다. `ValidationDetails` 속성을 사용할 수 있게 되기 전에 먼저 XML 태스크에 의해 수행된 XML 유효성 검사가 오류 또는 해당 위치에 대한 정보 없이 true 또는 false 결과만 반환했습니다. 이제 `ValidationDetails`를 true로 설정할 경우 출력 파일에는 줄 번호 및 위치를 포함하여 모든 오류에 대한 자세한 정보가 포함됩니다. 이 정보를 사용하여 XML 문서의 오류를 이해하고, 찾고, 수정할 수 있습니다. 자세한 내용은 [Validate XML with the XML Task](control-flow/xml-task.md)를 참조하십시오.  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)][!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 서비스 팩 2에는 `ValidationDetails` 속성이 도입되었습니다. 이 새 속성은 당시에는 발표되거나 문서화되지 않았습니다. `ValidationDetails` 속성 또한 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 및 SQL Server 2016에서 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014 버전에서 지원하는 기능](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
