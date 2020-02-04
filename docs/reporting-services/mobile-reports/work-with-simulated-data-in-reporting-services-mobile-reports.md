---
title: Reporting Services 모바일 보고서의 시뮬레이션 데이터 사용 | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 6baabc36-58fb-4a98-bb9c-c42bafb16d0f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 15c2ebe8c7084e10e4b7ff1ad556ed465d91c799
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "62474872"
---
# <a name="work-with-simulated-data-in-reporting-services-mobile-reports"></a>Work with simulated data in Reporting Services mobile reports
디자인 화면에 갤러리 요소를 추가하면 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 에서 해당 요소에 대해 시뮬레이션 데이터를 즉시 생성합니다. 이 데이터는 모바일 보고서를 만들 때 다양하고 유용한 목적으로 활용할 수 있습니다.   
  
![SS_MRP_SimDataTreeMapProps](../../reporting-services/mobile-reports/media/ss-mrp-simdatatreemapprops.png)  
  
시뮬레이션 데이터는 디자인 기반 방식으로 모바일 보고서를 만들 때 유용합니다. 처음에 요소를 시뮬레이션 데이터로 채우면 특정 데이터 요구 사항을 충족하지 않고도 모바일 보고서 프로토타입을 만들 수 있습니다. 그런 다음 이러한 모바일 보고서의 전반적 미관과 효과를 평가할 수 있습니다.  
  
## <a name="create-an-excel-file-with-simulated-data-as-a-template"></a>시뮬레이션 데이터가 포함된 Excel 파일을 템플릿으로 만들기  
  
시뮬레이션 데이터는 특정 모바일 보고서 디자인의 데이터 요구 사항을 정확히 나타내는 템플릿을 제공합니다.   
  
-  데이터 뷰의 오른쪽 상단에 있는 **모든 데이터 내보내기** 를 클릭합니다.   
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 는 시뮬레이션 데이터가 포함된 Excel 문서를 생성하여 실제 데이터로 빠르게 대체하고 즉시 내보낼 수 있습니다.   
  
## <a name="how-simulated-data-behaves"></a>시뮬레이션 데이터의 작동 방식  
  
생성된 시뮬레이션 데이터는 만들고 있는 모바일 보고서에 맞게 생성된 것입니다. 디자인 화면에 요소를 추가하면 연관된 시뮬레이션 데이터가 늘어나고 변경되면서 실제 데이터가 없는 상황에서 최선의 환경을 제공합니다. 따라서 차트 시각화에 시리즈를 추가하거나 하나 이상의 모바일 보고서 요소로 구성된 범위를 다른 방식으로 확장할 경우 추가 필드와 필터를 사용할 수 있습니다.  
  
앞에서 설명한 바와 같이 시뮬레이션 데이터를 Excel 파일로 내보내 관련 모바일 보고서에 완벽한 데이터 템플릿을 만들 수 있습니다. Excel 파일에서 실제 데이터로 교체하고 다시 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]로 가져올 수 있습니다.   
  
모든 컨트롤이 실제 데이터에 연결되면 더 이상 사용하지 않는 시뮬레이션 테이블은 모바일 보고서에서 자동으로 제거됩니다. 디자인 화면에서 요소가 참조하고 있는 시뮬레이션 테이블은 제거할 수 없습니다.  
  
>**참고**: 시뮬레이션 데이터는 모바일 보고서와 함께 serialize되지 않고 런타임에 즉시 생성되므로 전체 모바일 보고서의 크기에 추가되지 않습니다.  
  
### <a name="see-also"></a>참고 항목  
- [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기 및 게시](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  [iPad 앱에서 SQL Server 모바일 보고서 및 KPI](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  보기(iOS용 Power BI)  
-  [iPhone 앱에서 SQL Server 모바일 보고서 및 KPI](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports) 보기(iOS용 Power BI)  
  
  
  
  
  

