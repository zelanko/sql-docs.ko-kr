---
title: "로드할 수 없습니다. 'Microsoft.AnalysisServices.SharePoint.Integration' | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 6e350b67-5e18-4b90-8fb7-a0109cbb27b7
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a69a219376c2a67b003eaa6769843dc23791d829
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="could-not-load-microsoftanalysisservicessharepointintegration"></a>Microsoft.AnalysisServices.SharePoint.Integration를 로드할 수 없습니다.
  SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이 설치된 SharePoint 2010 환경에서는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 용 응용 프로그램 수준 솔루션이 제대로 배포되지 않은 경우 이 오류가 발생합니다.  
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|적용 대상|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|제품 버전|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|원인|Powerpivotwebapp 솔루션이 배포되지 않았거나 올바르게 배포되지 않았습니다.|  
|메시지 텍스트|'Microsoft.AnalysisServices.SharePoint.Integration' 파일 또는 어셈블리를 로드할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 에서는 솔루션 패키지를 사용하여 SharePoint 서버에서 해당 기능을 배포하는데, 이러한 솔루션 중 하나가 올바르게 배포되지 않았습니다. 그 결과 SharePoint 사이트에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 갤러리 또는 기타 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 응용 프로그램 페이지를 열려고 할 때마다 이 오류가 나타납니다.  
  
## <a name="user-action"></a>사용자 동작  
 솔루션 패키지를 배포합니다.  
  
1.  중앙 관리의 시스템 설정에서 **팜 솔루션 관리**를 클릭합니다.  
  
2.  **Powerpivotwebapp**를 클릭합니다.  
  
3.  **솔루션 배포**를 클릭합니다.  
  
4.  이 오류가 발생하는 웹 응용 프로그램을 선택합니다. 웹 응용 프로그램이 여러 개인 경우에는 모든 웹 응용 프로그램에 대해 솔루션을 다시 배포합니다.  
  
5.  **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SharePoint에 PowerPivot 솔루션 배포](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  

