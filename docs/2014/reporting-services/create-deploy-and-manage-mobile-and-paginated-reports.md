---
title: Reporting Services(SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services]
- SSRS
- reports [Reporting Services], about reports
- Reporting Services
- SQL Server Reporting Services
ms.assetid: b8d18d3d-9db0-43e7-8286-7b46cc3a37ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3e67d718c928785d85712eb5307130af22570c26
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78173912"
---
# <a name="reporting-services-ssrs"></a>Reporting Services(SSRS)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 는 조직의 보고서를 만들고 배포 하 고 관리 하는 데 도움이 되는 다양 한 바로 사용할 수 있는 도구 및 서비스를 제공 합니다. 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에는 보고 기능을 확장하고 사용자 지정할 수 있는 프로그래밍 기능이 있습니다.

 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]는 다양 한 데이터 원본에 대 한 포괄적인 보고 기능을 제공 하는 서버 기반 보고 플랫폼입니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에는 보고서를 만들고 관리 하 고 제공 하는 데 사용할 수 있는 전체 도구 집합 및 개발자가 사용자 지정 응용 프로그램에서 데이터와 보고서 처리를 통합 하거나 확장할 수 있도록 하는 Api가 포함 되어 있습니다. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]도구는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 환경에서 작동 하며 도구 및 구성 요소 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 와 완전히 통합 됩니다.

 
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]로 관계형, 다차원 또는 XML 기반 데이터 원본을 사용하여 대화형, 테이블 형식, 그래픽 또는 자유형 보고서를 만들 수 있습니다. 보고서는 차트, 지도, 스파크라인을 비롯한 풍부한 데이터 시각화를 포함할 수 있습니다. 보고서를 게시하고 보고서 처리를 예약하며 필요할 때 보고서에 액세스할 수 있습니다. 다양한 보기 형식 중에서 선택하며 보고서를 다른 애플리케이션(예: [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)])으로 내보내고 게시된 보고서를 구독할 수 있습니다. 사용자가 만드는 보고서는 웹 기반 연결을 통해 보거나 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 애플리케이션 또는 SharePoint 사이트의 일부로 볼 수 있습니다. 또한 SharePoint 사이트에 게시된 보고서에 대한 데이터 경고를 만들고 보고서 데이터가 변경되면 전자 메일 메시지를 수신할 수 있습니다.

 의 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]새로운 기능에 대 한 자세한 내용은 [새로운 기능 &#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md)를 참조 하세요.

 다른 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소, 도구 및 리소스에 대한 자세한 내용은 [SQL Server 온라인 설명서](../2014-toc/index.yml)를 참조하십시오.

 **영역 폴더로 콘텐츠 찾아보기** ![아이콘](media/hlp-16folder.gif "폴더 아이콘") [Reporting Services 보고서 서버](../../2014/reporting-services/reporting-services-report-server.md)

 ![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘") [REPORTING SERVICES 보고서 &#40;SSRS&#41;](reports/reporting-services-reports-ssrs.md)

 ![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘") [보고서 데이터 &#40;SSRS&#41;](report-data/report-data-ssrs.md)

 ![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘") [보고서 매개 변수 보고서 작성기 및 보고서 디자이너 &#40;&#41;](report-design/report-parameters-report-builder-and-report-designer.md)

 ![](media/hlp-16folder.gif "폴더 아이콘") [보고서 디자이너 &#40;SSRS&#41;폴더 아이콘 보고서 파트](report-design/report-parts-in-report-designer-ssrs.md)

 ![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘") [일정](subscriptions/schedules.md)

 ![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘") [구독 및 배달 &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)

 ![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘") [Reporting Services 데이터 경고](../ssms/agent/alerts.md)

 ![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘") [파워 뷰](https://office.microsoft.com/excel-help/power-view-explore-visualize-and-present-your-data-HA102835634.aspx)

 ![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘") [Reporting Services 보안 및 보호](security/reporting-services-security-and-protection.md)

 ![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘") [URL 액세스 &#40;SSRS&#41;](url-access-ssrs.md)

 [SSRS&#41;&#40;](extensions-ssrs.md) ![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘") 확장

 ![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘") [Reporting Services 도구](tools/reporting-services-tools.md)

 ![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘") [오류 및 이벤트 참조 Reporting Services &#40;&#41;](troubleshooting/errors-and-events-reference-reporting-services.md)

 ![폴더 아이콘](media/hlp-16folder.gif "폴더 아이콘") [기능 참조 &#40;Reporting Services&#41;](feature-reference-reporting-services.md)

## <a name="see-also"></a>참고 항목
 [리소스 센터 SQL Server](https://go.microsoft.com/fwlink/?linkID=219676)


