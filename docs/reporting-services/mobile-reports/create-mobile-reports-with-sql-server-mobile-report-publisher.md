---
title: SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기 | Microsoft Docs
description: 다양한 데이터 시각화와 함께 온-프레미스 데이터에 연결된 모바일 디바이스용 Reporting Services 모바일 보고서에 대해 알아봅니다.
ms.date: 12/06/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: a5a8dbf6-4c3a-435d-8188-d6656c32f229
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 51708fc41bb154fcf67ac3a21bd6680c69e2f2c2
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53213062"
---
# <a name="create-mobile-reports-with-sql-server-mobile-report-publisher"></a>SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기
다양한 데이터 시각화와 함께 모바일 디바이스용으로 최적화되고 온-프레미스 데이터에 연결된 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 모바일 보고서에 대해 알아봅니다. 

>[!NOTE]
>  대시보드 및 KPI와 같은 Datazen Server 콘텐츠를 SQL Server [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 서버로 마이그레이션해야 하나요? [SQL Server Migration Assistant for Datazen](https://www.microsoft.com/download/details.aspx?id=53128)(Datazen용 SQL Server Migration Assistant)을 사용해 보세요. 
 
![SS_MRP_LayoutTabSm](../../reporting-services/media/ss-mrp-layouttabsm.png)  

[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)]를 사용하면 모바일 디바이스 및 다양한 폼 팩터용으로 최적화된 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 모바일 보고서를 신속하게 만들 수 있습니다. 모바일 보고서는 시간, 범주 및 비교 차트부터 트리맵 및 사용자 지정 맵까지의 다양한 시각화 기능을 사용합니다. 

* 온-프레미스 SQL Server 및 Analysis Services 데이터를 포함하여 다양한 데이터 원본에 모바일 보고서를 연결합니다. 
* 조정 가능한 표 행/열이 표시된 디자인 화면에서 유동적인 모바일 보고서 요소를 사용하여 어떤 화면 크기에나 적합하도록 효율적으로 확장되는 모바일 보고서를 만듭니다. 
* 그런 다음 Reporting Service 서버에 이러한 모바일 보고서를 저장하고, 브라우저 또는 iPad, iPhone, Android 휴대폰 및 태블릿 및 Windows 10 디바이스의 Power BI 모바일 앱에서 이를 보고 조작합니다.
  
## <a name="create-includessrsnoversionmdincludesssrsnoversion-mdmd--mobile-reports"></a>[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]  모바일 보고서 만들기  
  
다음 문서는 시작하는 데 도움이 됩니다.
-  [SQL Server 모바일 보고서 게시자](https://go.microsoft.com/fwlink/?LinkID=733527)다운로드  
-  [Reporting Services 모바일 보고서 만들기](../../reporting-services/mobile-reports/create-a-reporting-services-mobile-report.md)  
-  [전체 연습: SQL Server Reporting Services에서 모바일 보고서 및 KPI 만들기](https://christopherfinlan.com/2015/12/21/how-to-create-mobile-reports-and-kpis-in-sql-server-reporting-services-2016-an-end-to-end-walkthrough/)(Christopher Finlan의 블로그)  
- [디자인 먼저 진행 또는 데이터 먼저 입력](../../reporting-services/mobile-reports/design-first-or-data-first-when-creating-in-reporting-services-mobile-reports.md): 먼저 시뮬레이션된 데이터로 보고서를 디자인할지 또는 사용자 고유의 데이터로 시작할지 결정합니다.  
- [Reporting Services 모바일 보고서에 대한 데이터](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md): 공유 데이터 세트의 데이터를 사용하거나 모바일 보고서에서 사용할 Excel 통합 문서에서 데이터를 준비합니다.
- [Reporting Services의 모바일 보고서 및 KPI에서 데이터 새로 고침이 작동하는 방식](https://christopherfinlan.com/2016/02/10/so-refreshinghow-data-refresh-works-with-mobile-reports-and-kpis-in-reporting-services/)(Christopher Finlan의 블로그): 공유 데이터 세트의 캐싱에 대해 읽어봄으로써 설정 데이터를 새로 고침 빈도를 제어하고 보고서 성능을 향상시킬 수 있습니다.
- [모바일 보고서의 시각화](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
- [모바일 보고서의 계기](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
- [모바일 보고서의 맵](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
- 회사의 색 및 로고로[웹 포털 및 모바일 보고서 브랜딩](../../reporting-services/branding-the-web-portal.md) 
  
## <a name="ssrs-mobile-reports-in-the-power-bi-mobile-apps"></a>Power BI 모바일 앱의 SSRS 모바일 보고서

-  [iOS 및Android용 Power BI 모바일 앱에서 Reporting Services 모바일 보고서 및 KPI](https://powerbi.microsoft.com/documentation/powerbi-mobile-iphone-kpis-mobile-reports) 보기
-  Windows 10 디바이스용 Power BI 앱에서 [Reporting Services 보고서 및 KPI](https://powerbi.microsoft.com/documentation/powerbi-mobile-win10-kpis-mobile-reports/) 보기   

## <a name="see-also"></a>참고 항목  
  
-   [공유 데이터 원본 만들기, 수정 및 삭제(SSRS)](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)  
-   [공유 데이터 세트 관리](../../reporting-services/report-data/manage-shared-datasets.md)  
-  [Reporting Services에서 KPI 사용](../../reporting-services/working-with-kpis-in-reporting-services.md)  
- [Power BI 모바일 액세스가 가능하도록 보고서 서버 설정](../../reporting-services/report-server/enable-a-report-server-for-power-bi-mobile-access.md)  

  
  

