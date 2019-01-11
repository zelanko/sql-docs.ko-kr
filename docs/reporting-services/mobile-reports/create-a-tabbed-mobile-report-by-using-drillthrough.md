---
title: 드릴스루를 사용하여 탭 모바일 보고서 만들기 | Reporting Services 모바일 보고서 | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d01f9f1bef4d13cbce3f3e736cbef2f838c680ef
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2018
ms.locfileid: "48906179"
---
# <a name="create-a-tabbed-mobile-report-by-using-drillthrough"></a>드릴스루를 사용하여 탭 모바일 보고서 만들기
드릴스루 보고서 및 매개 변수를 사용하여 탭으로 구성된 보고서 모양으로 작업되는 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 모바일 보고서를 만드는 방법에 대해 알아봅니다.

예를 들어 이 보고서의 위쪽에는 탭 역할을 하는 계기가 있습니다. 운송 계기를 클릭하면 차트의 나머지 부분에서 데이터가 운송 데이터로 필터링됩니다.

![06-모바일-보고서-웹-뷰어-운송](../../reporting-services/mobile-reports/media/tabbed-mobile-report-web-viewer-transportation-complete.png)

백그라운드에서 이는 실제로 별개의 보고서 5개로 구성된 집합이며 각 보고서는 보고서 맨 위에서 선택한 계기와 일치하도록 보고서를 필터링하는 서로 다른 매개 변수를 포함합니다. 먼저 5개의 보고서를 만든 다음 5개 보고서 각각에 대해 다른 4개 계기가 다른 4개 보고서로 드릴스루되도록 만듭니다.

다음에 이 예제를 위한 단계가 나와 있습니다.

## <a name="create-the-basic-report"></a>기본 보고서 만들기

1. 다음 5개의 계기가 포함된 판매라는 보고서를 만듭니다.

    * Sales
    * 운송
    * 연료
    * 스토리지
    * 기타 비용

   ![01-판매-모바일-보고서-게시자](../../reporting-services/mobile-reports/media/01-sales-mobile-report-publisher.png)
    
2. 판매 계기에 대해 **강조**를 **켜기**로 설정하여 보고서의 나머지 부분과 대조되도록 합니다. 이 경우 검정 바탕에 흰색입니다.

    ![01a-판매-강조-모바일-보고서-게시자](../../reporting-services/mobile-reports/media/01a-sales-accent-mobile-report-publisher.png)
    
3. [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서 서버에 저장합니다.

## <a name="make-copies-of-the-report"></a>보고서의 복사본 만들기

1. 판매 보고서의 복사본을 4개 만들고 다음과 같이 이름을 지정합니다. 

    * 운송
    * 연료
    * 스토리지
    * 기타 비용

3. [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서 서버에 저장합니다.

## <a name="set-the-gauge-as-a-drillthrough"></a>계기를 드릴스루로 설정

이 섹션에서는 각 계기(판매 계기 이외)를 각각의 해당 보고서에 대한 드릴스루로 설정합니다.

1. 판매 보고서에서 운송 계기를 선택합니다.

    ![02-판매-만들기-드릴스루-모바일-보고서-게시자](../../reporting-services/mobile-reports/media/02-sales-create-drillthrough-mobile-report-publisher.png)

2. **레이아웃** 탭을 선택한 상태에서 **Visual 속성** 창에서 **드릴스루 대상**을 선택합니다.

3. **모바일 보고서**를 선택합니다.

4. 드릴스루 대상이 될 보고서를 탐색하고 선택합니다. 이 경우 “금융 - 운송”입니다.

    ![03-판매-선택-대시보드-모바일-보고서-게시자](../../reporting-services/mobile-reports/media/03-sales-select-dashboard-mobile-report-publisher.png)

5. **대상 보고서 구성**에서 매개 변수를 선택하여 보고서를 필터링하고, **적용**을 선택합니다.

   ![04-판매-적용-매개 변수-모바일-보고서-게시자](../../reporting-services/mobile-reports/media/04-sales-apply-parameters-mobile-report-publisher.png)
   
6. 판매 보고서의 각기 다른 계기에 대해 이러한 단계를 반복합니다. 

## <a name="set-the-gauges-for-the-other-reports"></a>다른 보고서의 계기 설정

1.  운송 보고서를 열고, 판매 계기를 판매 보고서에 대한 드릴스루로 설정하고, 다른 3개 계기를 각각의 보고서에 대한 드릴스루로 설정합니다.

2. 계속 운송 보고서에서 운송 계기의 **강조**를 보고서의 나머지 부분과 대비되도록 **켜기**로 설정합니다.

3. 연료, 스토리지 및 기타 비용 보고서에 대해 이러한 단계를 반복합니다. 

## <a name="view-the-report-in-the-web-portal"></a>웹 포털에서 보고서 보기

1. [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서 서버로 이동하여 보고서 중 하나를 엽니다. 

2. 각 계기마다 오른쪽 위 모서리에 드릴스루 아이콘이 있습니다.

    ![웹-뷰어-드릴스루-아이콘-모바일-보고서-게시자](../../reporting-services/mobile-reports/media/web-viewer-drillthrough-icon-mobile-report-builder.png)

3. 계기 중 하나를 선택하여 해당 계기의 데이터를 필터링하는 보고서로 이동합니다.

   ![06-모바일-보고서-웹-뷰어-운송](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

### <a name="see-also"></a>관련 항목:
    
* [모바일 보고서에 매개 변수 추가](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [모바일 보고서에서 다른 모바일 보고서나 URL로 드릴스루 추가](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)




  

