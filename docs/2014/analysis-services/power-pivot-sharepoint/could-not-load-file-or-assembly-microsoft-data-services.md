---
title: 파일 또는 어셈블리를 로드할 수 없습니다 &#39;Microsoft.AnalysisServices.SharePoint.Integration&#39; | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6e350b67-5e18-4b90-8fb7-a0109cbb27b7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 42c7b7e876f244831920be390d97c88412eed63f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071673"
---
# <a name="could-not-load-file-or-assembly-39microsoftanalysisservicessharepointintegration39"></a>파일 또는 어셈블리를 로드할 수 없습니다 &#39;Microsoft.AnalysisServices.SharePoint.Integration&#39;
  SharePoint용 PowerPivot이 설치된 SharePoint 2010 환경에서는 PowerPivot용 애플리케이션 수준 솔루션이 제대로 배포되지 않은 경우 이 오류가 발생합니다.  
  
## <a name="details"></a>설명  
  
|||  
|-|-|  
|적용 대상|SharePoint용 PowerPivot|  
|제품 버전|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|원인|Powerpivotwebapp 솔루션이 배포되지 않았거나 올바르게 배포되지 않았습니다.|  
|메시지 텍스트|'Microsoft.AnalysisServices.SharePoint.Integration' 파일 또는 어셈블리를 로드할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 SharePoint용 PowerPivot에서는 솔루션 패키지를 사용하여 SharePoint 서버에서 해당 기능을 배포하는데, 이러한 솔루션 중 하나가 올바르게 배포되지 않았습니다. 그 결과 SharePoint 사이트에서 PowerPivot에 갤러리 또는 기타 PowerPivot 애플리케이션 페이지를 열려고 할 때마다 이 오류가 나타납니다.  
  
## <a name="user-action"></a>사용자 동작  
 솔루션 패키지를 배포합니다.  
  
1.  중앙 관리의 시스템 설정에서 **팜 솔루션 관리**를 클릭합니다.  
  
2.  **Powerpivotwebapp**를 클릭합니다.  
  
3.  **솔루션 배포**를 클릭합니다.  
  
4.  이 오류가 발생하는 웹 애플리케이션을 선택합니다. 웹 애플리케이션이 여러 개인 경우에는 모든 웹 애플리케이션에 대해 솔루션을 다시 배포합니다.  
  
5.  **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SharePoint에 PowerPivot 솔루션 배포](deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
