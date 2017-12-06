---
title: "Reporting Services 모바일 보고서의 지도 | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 50658295-a71c-441e-8eba-e1ef066629c0
caps.latest.revision: "10"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: dd0c562ba03e3a5b5d92530a40ad58b89e75756c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="maps-in-reporting-services-mobile-reports"></a>Maps in Reporting Services mobile reports
지도는 지리 데이터를 시각화하는 유용한 방법입니다. [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] 은(는) 다양한 유형의 지도 시각화를 제공하며, 대륙 및 많은 국가의 지도를 기본으로 제공합니다. [사용자 지정 지도를 업로드하여 사용](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)할 수도 있습니다.   
  
## <a name="types-of-maps"></a>지도 유형  
  
SQL Server 모바일 보고서는 다양한 상황에 유용한 세 가지 다른 유형의 지도를 제공합니다.  
  
![SSMRP_MapsGallery](../../reporting-services/mobile-reports/media/ssmrp-mapsgallery.png)  
  
**Gradient Heat Maps** (그라데이션 열 지도) Values(값) 속성의 필드가 지도의 각 영역을 채우는 한 가지 색상의 음영으로 표시됩니다. **Value Direction** (값 방향) 상자에서 높은 값이나 낮은 값 중 어떤 값을 더 어두운 색으로 나타낼지 설정할 수 있습니다.  
  
**Bubble Map** (거품형 지도) Values(값) 속성은 연결된 영역에 표시되는 거품형 시각화의 반지름을 결정한다. 모든 거품에 같은 색을 쓸지 아니면 모두 다른 색을 쓸지를 설정할 수 있습니다.   
  
**Range Stop Heat Maps** (범위 중지 열 지도)는 대상과 관련된 값을 보여줍니다. **Targets** (대상) 속성은 비교 필드와 값 필드 간의 델타를 결정합니다. 결과로 발생되는 델타는 지도의 연결된 영역을 채우는 색을 빨간색, 노란색, 녹색 중에서 결정합니다. **Value Direction** (값 방향) 상자에서 높은 값이나 낮은 값 중에서 어떤 값을 녹색으로 나타낼지 설정할 수 있습니다.  
  
## <a name="select-the-map-type-and-region"></a>지도 유형 및 영역 선택  
  
1. **레이아웃** 탭에서 지도 유형을 선택하고 디자인 화면으로 끌어서 원하는 크기로 만듭니다.  
  
2. **레이아웃** 뷰 > **Visual Properties**(시각 속성) 패널 > **지도**에서 원하는 지도 영역을 선택합니다.  
  
   ![SSMRP_SelectMap](../../reporting-services/mobile-reports/media/ssmrp-selectmaps.png)  
  
3. 그라데이션 및 범위 중지 열 지도에 대해 높은 값과 낮은 값 중 **Visual Properties** (시각 속성)의 **Value Direction**(값 방향) 상자에 적합한 값을 설정합니다.  
  
7. 거품형 지도의 경우 **Visual Properties** (시각 속성)에서 **Use Different Colors** (다른 색 사용)을 **On** (설정) 또는 **Off** (해제)으로 설정하여 거품을 모두 같은 색이나 다른 색으로 만듭니다.  
  
## <a name="select-the-map-data"></a>지도 데이터 선택  
보고서에 지도를 처음 추가할 때, [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 은(는) 시뮬레이션된 지리 데이터로 지도를 채웁니다.  
  
![SSMRP_MapsData](../../reporting-services/mobile-reports/media/ssmrp-mapsdata.png)  
  
지도에 실제 데이터를 표시하려면, 지도의 데이터 속성 값을 2가지 이상 설정해야 합니다.   
* **Keys** (키) 속성은 데이터를 특정 지도 영역(예: 미국의 주 또는 아프리카의 국가)에 연결합니다.  
* **Values** (값) 속성은 선택된 키 필드와 같은 테이블에 있는 숫자 필드입니다. 이 값은 지도마다 다르게 표현됩니다. **gradient map** (그라데이션 지도)는 이 값을 사용하여 값 영역에 기반하여 가지각색의 음영으로 영역의 색을 채웁니다. **bubble map** (거품형 지도)에서 각 영역의 거품 시각화 크기는 값 속성을 기반으로 합니다.   
* 범위 중지 열 지도의 경우 **Targets** (대상) 속성도 설정해야 합니다.  
  
### <a name="set-map-data-properties"></a>지도 데이터 속성 설정  
  
1. 왼쪽 위 모서리에서 **Data** (데이터) 탭을 선택합니다.  
  
2. **데이터 추가**를 선택한 후 **로컬 Excel** 또는 **SSRS 서버**중 하나를 선택합니다.  
  
   > **팁**: 데이터는 [모바일 보고서에 적합한 형식](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)이어야 합니다.  
  
3. 원하는 워크시트를 선택하고 **가져오기**를 선택합니다.  
   [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]에 데이터가 표시됩니다.  
  
4. **데이터** 뷰 > **데이터 속성** 패널 > **Keys**(키)의 왼쪽 상자에서 지도 데이터를 포함하는 테이블을 선택하고 오른쪽 상자에서 지도의 영역과 일치하는 키 필드를 선택합니다.  
  
5. **값** 아래 왼쪽 상자에 동일한 테이블이 있습니다. 지도에 값을 표시할 숫자 필드를 선택합니다.   
  
6. 범위 중지 열 지도의 경우 **Targets** (대상) 상자의 왼쪽 상자에 같은 테이블이 있습니다. 오른쪽 상자에서 대상으로 사용할 값의 숫자 필드를 선택합니다.   
  
   ![SSMRP_MapRangeHeatData](../../reporting-services/mobile-reports/media/ssmrp-maprangeheatdata.png)  
  
7. 왼쪽 위 모서리에서 **미리 보기** 를 선택합니다.  
  
   ![SSMRP_MapRangeHeatPreview](../../reporting-services/mobile-reports/media/ssmrp-maprangeheatpreview.png)  
     
8. 왼쪽 위 모서리에서 **저장** 아이콘을 선택하고 사용자의 컴퓨터 **Save Locally** (로컬에 저장)하거나 **Save to Server**(서버에 저장)합니다.  
  
### <a name="see-also"></a>참고 항목  
-  [Reporting Services 모바일 보고서의 사용자 지정 맵](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)  
- [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기 및 게시](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
  
  
