---
title: "드릴스루를 사용 하 여 탭된 모바일 보고서 만들기 | Reporting Services 모바일 보고서 | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6554f808c19540d2a3b7cbe3fdf4e86c5fe7a357
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="create-a-tabbed-mobile-report-by-using-drillthrough"></a>드릴스루를 사용 하 여 탭된 모바일 보고서 만들기
드릴스루 보고서 및 매개 변수를 사용하여 탭으로 구성된 보고서 모양으로 작업되는 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 모바일 보고서를 만드는 방법에 대해 알아봅니다.

예를 들어 이 보고서의 위쪽에는 탭 역할을 하는 계기가 있습니다. 운송 계기를 클릭하면 차트의 나머지 부분에서 데이터가 운송 데이터로 필터링됩니다.

![06-모바일-보고서-웹-뷰어-운송](../../reporting-services/mobile-reports/media/tabbed-mobile-report-web-viewer-transportation-complete.png)

백그라운드에서 이는 실제로 별개의 보고서 5개로 구성된 집합이며 각 보고서는 보고서 맨 위에서 선택한 계기와 일치하도록 보고서를 필터링하는 서로 다른 매개 변수를 포함합니다. 다섯 개의 보고서를 먼저 만든 각 다섯 개 보고서에 대해 수행 합니다 다른 4 개의 계기 drillthroughs에 다른 4 개 보고서를 합니다.

이 예제에 대 한 단계는 다음과 같습니다.

## <a name="create-the-basic-report"></a>기본 보고서 만들기

1. 다음 5개의 계기가 포함된 판매라는 보고서를 만듭니다.

    * Sales
    * 운송
    * 연료
    * 저장소
    * 기타 비용

   ![01-sales-모바일-보고서-게시자](../../reporting-services/mobile-reports/media/01-sales-mobile-report-publisher.png)
    
2. 설정 **악센트** 를 **에** Sales 계기에 대 한 하므로 것은와 대비는 나머지 보고서-이 경우의 검정 바탕에 흰색입니다.

    ![01a-Sales-Accent-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/01a-sales-accent-mobile-report-publisher.png)
    
3. 저장 하는 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서 서버.

## <a name="make-copies-of-the-report"></a>보고서의 복사본을 확인 하십시오.

1. 판매 보고서의 4 개 복사본을 만들고 이름을 지정 하 여: 

    * 운송
    * 연료
    * 저장소
    * 기타 비용

3. 에 저장 된 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서 서버.

## <a name="set-the-gauge-as-a-drillthrough"></a>계기를 드릴스루로 설정

이 섹션에서는 각각의 해당 보고서를 드릴스루로 (Sales 위계) 외에 각 계기를 설정 합니다.

1. 판매 보고서에서 운송 계기를 선택 합니다.

    ![02-Sales-Create-DrillThrough-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/02-sales-create-drillthrough-mobile-report-publisher.png)

2. 와 **레이아웃** 탭이 선택에 **시각적 속성** 창 선택 **드릴스루 대상**합니다.

3. 선택 **모바일 보고서**합니다.

4. 탐색 하 고이 경우-드릴스루에 대 한 대상 될 보고서를 선택 합니다. "재무-운송."

    ![03-Sales-Select-Dashboard-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/03-sales-select-dashboard-mobile-report-publisher.png)

5. **대상 보고서 구성**, 보고서를 필터링 하 여 선택 매개 변수를 선택 **적용**합니다.

   ![04-Sales-Apply-Parameters-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/04-sales-apply-parameters-mobile-report-publisher.png)
   
6. 각 판매 보고서에 있는 다른 계기에 대해 이러한 단계를 반복 합니다. 

## <a name="set-the-gauges-for-the-other-reports"></a>다른 보고서에 계기를 설정 합니다.

1.  열기 운송 보고서 설정 Sales 계기 판매 보고서를 드릴스루 하 고 해당 보고서에 drillthroughs로 세 개의 다른 계기를 합니다.

2. 운송 보고서에서 여전히 설정 **악센트** 운송 계기를 **에**와 대비는 보고서의 나머지입니다.

3. 연료, 저장소 및 기타 경비 보고서에 대 한 이러한 단계를 반복 합니다. 

## <a name="view-the-report-in-the-web-portal"></a>웹 포털에서 보고서 보기

1. 이동 하 여 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서 서버 및 보고서 중 하나를 엽니다. 

2. 오른쪽 위 모서리에 있는 드릴스루 아이콘 각 하면 계기에 표시 합니다.

    ![Web-Viewer-drillthrough-icon-mobile-report-builder](../../reporting-services/mobile-reports/media/web-viewer-drillthrough-icon-mobile-report-builder.png)

3. 계기는 계기의 데이터를 필터링 하는 보고서로 이동 하려면 중 하나를 선택 합니다.

   ![06-모바일-보고서-웹-뷰어-운송](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

### <a name="see-also"></a>참고 항목
    
* [모바일 보고서에 매개 변수 추가](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [모바일 보고서에서 다른 모바일 보고서나 URL로 드릴스루 추가](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)




  


