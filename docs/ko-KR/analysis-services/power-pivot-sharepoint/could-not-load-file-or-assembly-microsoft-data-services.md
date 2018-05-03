---
title: 파일 또는 Microsoft 데이터 액세스 서비스 어셈블리를 로드할 수 없습니다 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1de8cd48bcce0b2c66a555358fc7c73182999f0f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="could-not-load-file-or-assembly-microsoft-data-services"></a>파일 또는 Microsoft 데이터 액세스 서비스 어셈블리를 로드할 수 없습니다.
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이 설치된 SharePoint 2010 환경에서는 데이터 피드 내보내기를 시도할 때 시스템에 필요한 Microsoft ADO.NET Data Services 버전이 없으면 이 오류가 발생합니다.  
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|적용 대상|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|제품 버전|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|원인|ADO.NET Data Services 3.5 SP1이 없습니다.|  
|메시지 텍스트|파일이나 어셈블리 'Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' 또는 여기에 종속되어 있는 파일이나 어셈블리 중 하나를 로드할 수 없습니다. 시스템에서 지정한 파일을 찾을 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 SharePoint 2010에는 SharePoint 목록을 XML 데이터 피드로 내보내는 데 사용할 수 있는 데이터 피드로 내보내기 단추가 포함되어 있습니다. 또한 SharePoint 모드의 Reporting Services와 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 은 모두 ADO.NET Data Services가 필요한 데이터 피드 기능을 지원합니다.  
  
 ADO.NET Data Services가 설치되어 있지 않으면 데이터 피드를 요청할 때 이 오류가 발생합니다.  
  
## <a name="user-action"></a>사용자 동작  
  
1.  SharePoint 2010에 대 한 하드웨어 및 소프트웨어 요구 사항 설명서로 이동 [결정 하드웨어 및 소프트웨어 요구 사항 (SharePoint 2010)](http://go.microsoft.com/fwlink/?LinkId=169734) (http://go.microsoft.com/fwlink/?LinkId=169734)합니다.  
  
2.  **소프트웨어 필수 구성 요소 설치**에서 현재 사용 중인 운영 체제(Windows Server 2008 SP2 또는 Windows Server 2008 R2)에 맞는 ADO.NET Data Services 3.5의 링크를 찾습니다.  
  
3.  링크를 클릭하여 서비스를 설치하는 설치 프로그램을 실행합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SharePoint에 Power Pivot 솔루션 배포](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
