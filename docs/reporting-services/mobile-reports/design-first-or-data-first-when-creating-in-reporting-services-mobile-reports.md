---
title: "Reporting Services 모바일 보고서에서 만들 때 디자인 먼저 진행 또는 데이터 먼저 입력 | Microsoft Docs"
ms.custom: 
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7b355fa-312b-4074-bc9b-776269d4fb51
caps.latest.revision: "17"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5eb348ea84163770d112667b071f7538061a1360
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="design-first-or-data-first-when-creating-in-reporting-services-mobile-reports"></a>Design first or data first when creating in Reporting Services mobile reports
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)]를 사용하면 조정 가능한 표 행/열이 표시된 디자인 화면에서 유동적인 모바일 보고서 요소를 사용하여 어떤 화면 크기에나 적합하도록 효율적으로 확장되는 모바일 보고서를 빠르게 만들 수 있습니다.   
  
모바일 보고서를 만들 때는 데이터를 먼저 입력하거나 디자인을 먼저 진행하는 두 가지 기본 방식 중에서 선택할 수 있습니다. [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] 에서는 두 가지 방식을 모두 지원합니다.   
  
## <a name="design-first"></a>디자인 먼저 진행  
  
다음 다이어그램에는 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] 레이아웃 보기의 구성 요소가 나와 있습니다.   
  
![SS_MRP_LayoutTab](../../reporting-services/mobile-reports/media/ss-mrp-layouttab.png)  
  
디자인을 먼저 진행하는 방식에서는 데이터를 가져오지 않고 모바일 보고서 레이아웃을 먼저 만듭니다. 데이터 서식을 올바르게 지정했는지 모를 때 이 방식을 사용하면 모바일 보고서를 효율적으로 만들 수 있습니다. 실제 데이터가 없으므로 갤러리 요소는 생성된 시뮬레이션 데이터에 자동 바인딩됩니다. 이러한 데이터를 내보낸 다음 템플릿으로 사용해 필요한 데이터를 설명할 수 있습니다.  
  
## <a name="data-first"></a>데이터 먼저 입력  
데이터를 먼저 입력하는 방식에서는 필요한 모든 데이터를 먼저 가져온 다음 모바일 보고서를 디자인하고 모바일 보고서 요소에 대해 데이터 속성을 설정합니다. 이 경우 각 요소를 레이아웃에 추가할 때 실제 데이터에 연결할 수 있다는 이점이 있습니다. 데이터를 먼저 입력하는 방식을 사용할 때는 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)]에서 사용할 수 있도록 실제 데이터의 서식을 올바르게 지정했는지 확인하세요.   
  
 다음 다이어그램에는 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] 데이터 보기의 모든 구성 요소가 나와 있습니다.  
  
![SS_MRP_DataTab](../../reporting-services/mobile-reports/media/ss-mrp-datatab.png)  
  
### <a name="see-also"></a>관련 항목:  
- [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기 및 게시](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [iPad 앱에서 SQL Server 모바일 보고서 및 KPI](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  보기(iOS용 Power BI)  
-  [iPhone 앱에서 SQL Server 모바일 보고서 및 KPI](https://pbiwebprod-docs.azurewebsites.net/en-us/documentation/powerbi-mobile-iphone-kpis-mobile-reports) 보기(iOS용 Power BI)  
  
  
  
  

