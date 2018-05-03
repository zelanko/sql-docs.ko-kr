---
title: 데이터 피드 (SharePoint 용 파워 피벗) 사용 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8f0b6c60d3f68d7a643264d3e850b7ce6cd56c22
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="use-data-feeds-power-pivot-for-sharepoint"></a>데이터 피드 사용(SharePoint용 PowerPivot)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  데이터 피드는 온라인 데이터 원본에서 생성되어 대상 문서 또는 응용 프로그램으로 스트리밍되는 하나 이상의 데이터 스트림입니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel을 사용 중인 경우 데이터 피드를 통해 임의 데이터 원본의 기존 회사 또는 비즈니스 데이터를 Excel 2010 통합 문서의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 창으로 쉽게 가져올 수 있습니다. 통합 문서로 데이터 피드를 가져온 후 SharePoint 서버에서 예약한 데이터 새로 고침 작업에서 나중에 참조할 수 있습니다.  
  
 데이터 피드의 사용 방법은 Atom 데이터 피드를 지원하는 응용 프로그램의 기본 내보내기 기능을 사용하는지 또는 사용자 지정 데이터 서비스를 만들어 사용하는지에 따라 달라집니다. Atom XML 데이터를 게시하고 읽을 수 있는 응용 프로그램은 데이터 피드 및 데이터 서비스의 메커니즘을 사용자에게 숨기는 원활한 데이터 전송 기능을 제공합니다. 사용자는 단순히 한 응용 프로그램에서 다른 응용 프로그램으로 데이터를 이동하기만 하면 됩니다.  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 Microsoft SharePoint 2010은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에서 사용할 수 있는 데이터 피드를 제공합니다. 이 항목의 정보를 사용하여 기존의 보고서 및 목록에서 데이터 피드에 액세스하는 방법을 배울 수 있습니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [필수 구성 요소](#prereq)  
  
 [SharePoint 목록에서 데이터 피드 만들기](#sharepointlist)  
  
 [Reporting Services 보고서에서 데이터 피드 만들기](#rsreport)  
  
 [데이터 서비스 문서에서 데이터 피드 만들기](#dsdoc)  
  
##  <a name="prereq"></a> 필수 구성 요소  
 데이터 피드를 Excel 2010으로 가져오려면 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel이 있어야 합니다.  
  
 Atom 1.0 형식으로 데이터를 제공하는 웹 서비스나 데이터 서비스가 필요합니다. [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 SharePoint 2010 모두 이러한 형식으로 데이터를 제공할 수 있습니다.  
  
 SharePoint 목록을 데이터 피드로 내보낼 수 있으려면 SharePoint 서버에 ADO.NET Data Services를 설치해야 합니다. 자세한 내용은 [ADO.NET Data Services를 설치하여 SharePoint 목록의 데이터 피드 내보내기 지원](http://msdn.microsoft.com/en-us/f32527ae-f623-4e08-adfb-6d3262f5c2ac)을 참조하세요.  
  
##  <a name="sharepointlist"></a> SharePoint 목록에서 데이터 피드 만들기  
 SharePoint 2010 팜에서 SharePoint 목록의 목록 리본에는 데이터 피드로 내보내기 단추가 있습니다. 이 단추를 클릭하여 목록을 피드로 내보낼 수 있습니다. 최상의 결과를 얻으려면 Excel 2010과 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 클라이언트 응용 프로그램이 워크스테이션에 설치되어 있어야 합니다. 데이터 피드 내보내기에 응답하여 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 클라이언트 응용 프로그램이 시작되어 목록을 포함하는 새 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 테이블을 만듭니다.  
  
1.  SharePoint 사이트에서 목록을 엽니다.  
  
2.  목록 도구에서 **목록**을 클릭합니다.  
  
3.  연결 및 내보내기에서 **데이터 피드로 내보내기**를 클릭합니다.  
  
    > [!NOTE]  
    >  **데이터 피드로 내보내기** 단추는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]을 통해 SharePoint에 추가됩니다. SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이 설치되어 있지 않거나 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 기능을 활성화하지 않은 경우에는 이 단추를 사용할 수 없습니다.  
  
4.  **for Excel이 로컬에 설치되어 있는 경우** 열기 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 를 클릭하고, 나중에 가져오기 작업을 수행할 수 있도록 .atomsvc 문서를 하드 드라이브에 저장하려면 **저장** 을 클릭합니다.  
  
5.  **열기**를 선택한 경우 테이블 가져오기 마법사를 사용하여 데이터 피드를 워크시트로 가져옵니다. 데이터 피드가 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 창에 새 테이블로 추가됩니다.  
  
 ADO.NET Data Services 3.5.1이 SharePoint 서버에 설치되어 있지 않으면 오류가 발생합니다. 오류 및 오류 해결 방법에 대한 자세한 내용은 [ADO.NET Data Services를 설치하여 SharePoint 목록의 데이터 피드 내보내기 지원](http://msdn.microsoft.com/en-us/f32527ae-f623-4e08-adfb-6d3262f5c2ac)을 참조하세요.  
  
##  <a name="rsreport"></a> Reporting Services 보고서에서 데이터 피드 만들기  
 SQL Server 2008 R2 Reporting Services가 배포되어 있는 경우 새로운 Atom 렌더링 확장을 사용하여 기존 보고서에서 데이터 피드를 생성할 수 있습니다. 최상의 결과를 얻으려면 Excel 2010과 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel이 워크스테이션에 설치되어 있어야 합니다. 데이터 피드 내보내기에 응답하여 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 클라이언트 응용 프로그램이 시작되어 스트리밍되는 테이블과 열을 자동으로 이를 추가해 관계를 만듭니다.  
  
 보고서에서 데이터 피드를 내보내는 방법에 대한 자세한 내용은 [보고서 작성기 도움말 파일](http://go.microsoft.com/fwlink/?LinkId=154494)에서 [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  SharePoint 라이브러리에 게시되는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서로 보고서 데이터를 다시 가져오는 데이터 새로 고침 되풀이 일정을 설정하려면 보고서 서버를 SharePoint 통합용으로 구성해야 합니다. SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]Reporting Services를 함께 사용하는 방법에 대한 자세한 내용은 [보고서 서버의 구성 및 관리&#40;Reporting Services SharePoint 모드&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md)를 참조하세요.  
  
##  <a name="dsdoc"></a> 데이터 서비스 문서에서 데이터 피드 만들기  
 Atom 피드를 생성하는 사용자 지정 데이터 서비스가 있는 경우 사용자와 응용 프로그램에서 데이터를 사용할 수 있게 하는 방법으로 데이터 서비스 문서를 설정할 수 있습니다. *데이터 서비스 문서* 파일(.atomsvc)에서는 Atom 연결 형식으로 데이터를 게시하는 온라인 원본에 대해 하나 이상의 연결을 지정합니다. 데이터 서비스 문서는 SharePoint 서버에 게시된 데이터 서비스 문서를 찾아보기 위한 공용 액세스 지점을 제공하는 특수한 용도의 라이브러리인 *데이터 피드 라이브러리*에서 만들 수 있습니다. 데이터 피드 라이브러리에 있는 데이터 서비스 문서에 액세스할 수 있는 정보 작업자는 문서의 SharePoint URL을 참조하여 데이터 피드를 해당 통합 문서 및 응용 프로그램으로 가져올 수 있습니다.  
  
1.  사이트 관리자가 만든 데이터 피드 라이브러리를 엽니다. 자세한 내용은 [데이터 피드 라이브러리 만들기 또는 사용자 지정&#40;SharePoint용 파워 피벗&#41;](../../analysis-services/power-pivot-sharepoint/create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md)을 참조하세요.  
  
2.  라이브러리 도구에서 **문서**를 클릭합니다.  
  
3.  **새 문서**를 클릭합니다.  
  
4.  파일 이름과 설명을 제공합니다.  
  
5.  피드를 제공하는 하나 이상의 URL을 지정합니다.  
  
    1.  **기준 URL** 은 선택 사항입니다. 데이터 서비스 문서에서 여러 피드를 제공하는 경우 기준 URL을 지정해야 합니다. 기준 URL에서는 모든 피드에 공통되는 URL 부분(예: 서버 이름 및 사이트)을 지정해야 합니다. Reporting Services 보고서에 대한 데이터 서비스 문서를 만들 경우 기준 URL은 보고서 서버 URL 및 보고서입니다.  
  
    2.  **웹 서비스 URL** 은 필수입니다. 이 값은 기준 URL 없이 포함 해야 `http://` 또는 `https://` 주소에서입니다. 기준 URL을 지정한 경우 웹 서비스 URL은 기준 URL 다음에 오는 부분입니다. 예를 들어 전체 URL이 `http://adventure-works/inventory/today.aspx`, 기본 url `http://adventure-works/inventory`, 및 웹 서비스 URL은 /today.aspx입니다.  
  
         웹 서비스 URL은 데이터 하위 집합을 필터링하거나 선택하는 매개 변수를 포함할 수 있습니다. 피드를 제공하는 응용 프로그램이나 서비스는 URL에 지정된 매개 변수를 지원해야 합니다.  
  
6.  피드와 테이블의 개수가 일대일이 되도록 **테이블 이름**을 입력합니다. 이 값은 필수 사항입니다. 테이블 이름은 데이터 피드를 사용하는 클라이언트 응용 프로그램에서 사용됩니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel에서 테이블 이름은 가져온 데이터를 포함하는 테이블 이름을 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 창에서 지정하는 데 사용됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [중앙 관리에서 사이트 모음에 대해 파워 피벗 기능 통합 활성화](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)   
 [데이터 피드 라이브러리를 사용하여 데이터 피드 공유&#40;SharePoint용 파워 피벗&#41;](../../analysis-services/power-pivot-sharepoint/share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint.md)  
  
  
