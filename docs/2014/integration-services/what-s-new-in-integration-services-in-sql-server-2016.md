---
title: 어떤&#39;s 새 (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
caps.latest.revision: 112
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c7d37fb3c1d2cd1dcafecc012fbe83e1864e50ed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080218"
---
# <a name="what39s-new-integration-services"></a>어떤&#39;s 새 (Integration Services)
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]는 이전 릴리스에서 변경되지 않았습니다.  
  
 다른 작업에 대 한 내용은 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 제품 및 기술에 참조 [SQL Server 2014의 새로운](../sql-server/what-s-new-in-sql-server-2016.md)합니다.  
  
 관련 된 변경 내용에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence 참조 [What's New in Analysis Services 및 Business Intelligence](../analysis-services/what-s-new-in-analysis-services.md)합니다.  
  
##  <a name="ValidateXML"></a> XML 태스크에서 풍부한 XML 유효성 검사 출력  
 XML 문서의 유효성을 검사 하 고 사용 하 여 풍부한 오류 출력을 가져올는 `ValidationDetails` XML 태스크의 속성입니다. 전에 `ValidationDetails` 속성을 사용할 수 있는 XML 유효성 검사 XML 태스크에 의해 true 또는 false 결과만 오류 또는 해당 위치에 대 한 정보 없이 반환 합니다. 설정할 때 이제 `ValidationDetails` true 이면 출력 파일 줄 번호 및 위치를 포함 하 여 모든 오류에 대 한 자세한 정보를 포함 합니다. 이 정보를 사용하여 XML 문서의 오류를 이해하고, 찾고, 수정할 수 있습니다. 자세한 내용은 [Validate XML with the XML Task](control-flow/xml-task.md)를 참조하십시오.  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 도입 된 `ValidationDetails` 속성 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 서비스 팩 2입니다. 이 새 속성은 당시에는 발표되거나 문서화되지 않았습니다. `ValidationDetails` 속성 에서도 제공 됩니다. [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 및 SQL Server 2016에서 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 2014 버전에서 지원하는 기능](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  