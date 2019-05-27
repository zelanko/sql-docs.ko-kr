---
title: 데이터 피드 (SharePoint 용 PowerPivot) 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 50140fdf-6fd1-41a1-9c14-8ecfb97ba2e1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6efccad47f0d6670c87aeb1e9cc9ef9ec654a138
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070911"
---
# <a name="use-data-feeds-powerpivot-for-sharepoint"></a>데이터 피드 사용(SharePoint용 PowerPivot)
  데이터 피드는 온라인 데이터 원본에서 생성되어 대상 문서 또는 애플리케이션으로 스트리밍되는 하나 이상의 데이터 스트림입니다. PowerPivot for Excel을 사용 중인 경우 데이터 피드를 통해 임의 데이터 원본의 기존 회사 또는 비즈니스 데이터를 Excel 2010 통합 문서의 PowerPivot 창으로 쉽게 가져올 수 있습니다. 통합 문서로 데이터 피드를 가져온 후 SharePoint 서버에서 예약한 데이터 새로 고침 작업에서 나중에 참조할 수 있습니다.  
  
 데이터 피드의 사용 방법은 Atom 데이터 피드를 지원하는 애플리케이션의 기본 내보내기 기능을 사용하는지 또는 사용자 지정 데이터 서비스를 만들어 사용하는지에 따라 달라집니다. Atom XML 데이터를 게시하고 읽을 수 있는 애플리케이션은 데이터 피드 및 데이터 서비스의 메커니즘을 사용자에게 숨기는 원활한 데이터 전송 기능을 제공합니다. 사용자는 단순히 한 애플리케이션에서 다른 애플리케이션으로 데이터를 이동하기만 하면 됩니다.  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 Microsoft SharePoint 2010은 PowerPivot 통합 문서에서 사용할 수 있는 피드 데이터를 제공 합니다. 이 항목의 정보를 사용하여 기존의 보고서 및 목록에서 데이터 피드에 액세스하는 방법을 배울 수 있습니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [필수 구성 요소](#prereq)  
  
 [SharePoint 목록에서 데이터 피드 만들기](#sharepointlist)  
  
 [Reporting Services 보고서에서 데이터 피드 만들기](#rsreport)  
  
 [데이터 서비스 문서에서 데이터 피드 만들기](#dsdoc)  
  
##  <a name="prereq"></a> 필수 구성 요소  
 데이터 피드를 Excel 2010으로 가져오려면 PowerPivot for Excel이 있어야 합니다.  
  
 Atom 1.0 형식으로 데이터를 제공하는 웹 서비스나 데이터 서비스가 필요합니다.  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 SharePoint 2010 모두 이러한 형식으로 데이터를 제공할 수 있습니다.  
  
 SharePoint 목록을 데이터 피드로 내보낼 수 있으려면 SharePoint 서버에 ADO.NET Data Services를 설치해야 합니다. 자세한 내용은 [ADO.NET Data Services를 설치하여 SharePoint 목록의 데이터 피드 내보내기 지원](../../sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)을 참조하세요.  
  
##  <a name="sharepointlist"></a> SharePoint 목록에서 데이터 피드 만들기  
 SharePoint 2010 팜에서 SharePoint 목록의 목록 리본에는 데이터 피드로 내보내기 단추가 있습니다. 이 단추를 클릭하여 목록을 피드로 내보낼 수 있습니다. 최상의 결과를 얻으려면 Excel 2010과 PowerPivot 클라이언트 응용 프로그램이 워크스테이션에 설치되어 있어야 합니다. 데이터 피드 내보내기에 응답하여 PowerPivot 클라이언트 응용 프로그램이 시작되고 목록을 포함하는 새 PowerPivot 테이블을 만듭니다.  
  
1.  SharePoint 사이트에서 목록을 엽니다.  
  
2.  목록 도구에서 **목록**을 클릭합니다.  
  
3.  연결 및 내보내기에서 **데이터 피드로 내보내기**를 클릭합니다.  
  
    > [!NOTE]  
    >  합니다 **데이터 피드로 내보내기** 단추는 PowerPivot 통해 SharePoint에 추가 됩니다. SharePoint용 PowerPivot이 설치되어 있지 않거나 PowerPivot 기능을 활성화하지 않은 경우에는 이 단추를 사용할 수 없습니다.  
  
4.  클릭 **엽니다** PowerPivot for Excel 로컬로 설치 하는 경우 하거나 클릭 **저장** 나중에 가져오기 작업을 위해 하드 드라이브에.atomsvc 문서를 저장 하 합니다.  
  
5.  **열기**를 선택한 경우 테이블 가져오기 마법사를 사용하여 데이터 피드를 워크시트로 가져옵니다. 데이터 피드가 PowerPivot 창에 새 테이블로 추가됩니다.  
  
 ADO.NET Data Services 3.5.1이 SharePoint 서버에 설치되어 있지 않으면 오류가 발생합니다. 오류 및 오류 해결 방법에 대한 자세한 내용은 [ADO.NET Data Services를 설치하여 SharePoint 목록의 데이터 피드 내보내기 지원](../../sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)을 참조하세요.  
  
##  <a name="rsreport"></a> Reporting Services 보고서에서 데이터 피드 만들기  
 SQL Server 2008 R2 Reporting Services가 배포되어 있는 경우 새로운 Atom 렌더링 확장을 사용하여 기존 보고서에서 데이터 피드를 생성할 수 있습니다. 최상의 결과를 얻으려면 Excel 2010과 PowerPivot for Excel이 워크스테이션에 설치되어 있어야 합니다. 데이터 피드 내보내기에 응답하여 PowerPivot 클라이언트 응용 프로그램이 시작되고 테이블과 열이 스트리밍될 때 자동으로 이를 추가하고 연결합니다.  
  
 보고서에서 데이터 피드를 내보내는 방법에 대한 자세한 내용은 [보고서 작성기 도움말 파일](https://go.microsoft.com/fwlink/?LinkId=154494)에서 [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  SharePoint 라이브러리에 게시되는 PowerPivot 통합 문서에 보고서 데이터를 다시 가져오는 데이터 새로 고침 되풀이 일정을 설정하려면 보고서 서버를 SharePoint 통합용으로 구성해야 합니다. PowerPivot for SharePoint 및 Reporting Services 함께 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [구성 및 보고서 서버 관리 &#40;Reporting Services SharePoint 모드&#41;](../../reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md)합니다.  
  
##  <a name="dsdoc"></a> 데이터 서비스 문서에서 데이터 피드 만들기  
 Atom 피드를 생성하는 사용자 지정 데이터 서비스가 있는 경우 사용자와 애플리케이션에서 데이터를 사용할 수 있게 하는 방법으로 데이터 서비스 문서를 설정할 수 있습니다. *데이터 서비스 문서* 파일(.atomsvc)에서는 Atom 연결 형식으로 데이터를 게시하는 온라인 원본에 대해 하나 이상의 연결을 지정합니다. 데이터 서비스 문서는 SharePoint 서버에 게시된 데이터 서비스 문서를 찾아보기 위한 공용 액세스 지점을 제공하는 특수한 용도의 라이브러리인 *데이터 피드 라이브러리*에서 만들 수 있습니다. 데이터 피드 라이브러리에 있는 데이터 서비스 문서에 액세스할 수 있는 정보 작업자는 문서의 SharePoint URL을 참조하여 데이터 피드를 해당 통합 문서 및 애플리케이션으로 가져올 수 있습니다.  
  
1.  사이트 관리자가 만든 데이터 피드 라이브러리를 엽니다. 자세한 내용은 [만들거나 데이터 피드 라이브러리를 사용자 지정 &#40;SharePoint 용 PowerPivot&#41;](create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md)합니다.  
  
2.  라이브러리 도구에서 **문서**를 클릭합니다.  
  
3.  **새 문서**를 클릭합니다.  
  
4.  파일 이름과 설명을 제공합니다.  
  
5.  피드를 제공하는 하나 이상의 URL을 지정합니다.  
  
    1.  **기준 URL** 은 선택 사항입니다. 데이터 서비스 문서에서 여러 피드를 제공하는 경우 기준 URL을 지정해야 합니다. 기준 URL에서는 모든 피드에 공통되는 URL 부분(예: 서버 이름 및 사이트)을 지정해야 합니다. Reporting Services 보고서에 대한 데이터 서비스 문서를 만들 경우 기준 URL은 보고서 서버 URL 및 보고서입니다.  
  
    2.  **웹 서비스 URL** 은 필수입니다. 기준 URL이 없을 경우 이 값은 http:// 또는 https://를 주소에 포함해야 합니다. 기준 URL을 지정한 경우 웹 서비스 URL은 기준 URL 다음에 오는 부분입니다. 예를 들어 전체 URL은 http://adventure-works/inventory/today.aspx, 기본 url http://adventure-works/inventory, 및 웹 서비스 URL은 /today.aspx입니다.  
  
         웹 서비스 URL은 데이터 하위 집합을 필터링하거나 선택하는 매개 변수를 포함할 수 있습니다. 피드를 제공하는 애플리케이션이나 서비스는 URL에 지정된 매개 변수를 지원해야 합니다.  
  
6.  피드와 테이블의 개수가 일대일이 되도록 **테이블 이름**을 입력합니다. 이 값은 필수 사항입니다. 테이블 이름은 데이터 피드를 사용하는 클라이언트 애플리케이션에서 사용됩니다. PowerPivot for Excel에서 테이블 이름은 PowerPivot 창에서 가져온 데이터를 포함하는 테이블을 지정하는 데 사용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [중앙 관리에서 사이트 모음에 대해 PowerPivot 기능 통합 활성화](activate-power-pivot-integration-for-site-collections-in-ca.md)   
 [데이터 피드 라이브러리를 사용 하 여 데이터 피드 공유 &#40;SharePoint 용 PowerPivot&#41;](share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint.md)  
  
  
