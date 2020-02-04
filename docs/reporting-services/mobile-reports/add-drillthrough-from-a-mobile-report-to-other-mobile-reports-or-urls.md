---
title: 모바일 보고서에서 다른 모바일 보고서나 URL로 드릴스루 추가 | Microsoft Docs
ms.date: 09/20/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 30d0a3fd-5588-417e-b25d-cc5b7624cdb1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4b702c79ad5c80254595ef5c4ff440919a8482e1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63280714"
---
# <a name="add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls"></a>모바일 보고서에서 다른 모바일 보고서나 URL로 드릴스루 추가
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 모바일 보고서의 계기, 차트 또는 데이터 표에서 다른 모바일 보고서 또는 사용자 지정 URL로의 드릴스루를 추가할 수 있습니다. 

*드릴스루*  는 다른 대상 보고서나 URL을 여는 원본 보고서의 링크입니다. 대체로 대상 드릴스루 보고서에는 요약 보고서의 일부 항목에 대한 세부 정보가 포함되어 있습니다. 원본 모바일 보고서에 따라 하나 이상의 매개 변수를 대상 모바일 보고서에 전달하거나 사용자 지정 URL에 통합할 수 있습니다.  
  
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 웹 포털에서 원본 모바일 보고서를 보고 드릴스루 대상이 있는 요소를 선택하면 다른 모바일 보고서나 URL인 해당 대상으로 이동합니다.  

URL이나 다른 모바일 보고서에 드릴스루 기능이 있는 보고서 항목은 드릴스루 아이콘 ![모바일 보고서 드릴스루 아이콘](../../reporting-services/mobile-reports/media/mobile-report-drill-through-icon.png) 이 오른쪽 위에 있습니다.

![모바일 보고서 계기 드릴스루](../../reporting-services/mobile-reports/media/mobile-report-gauge-drill-through.png) 

>**팁**: 먼저 대상 보고서를 만들고 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 웹 포털에 저장합니다. 원본 보고서에서 매개 변수를 전달하려는 경우 대상 보고서에도 매개 변수를 추가합니다. 그런 다음 원본 보고서에서 대상 보고서로의 드릴스루를 설정할 수 있습니다. [모바일 보고서에 매개 변수를 추가](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)합니다.
 
## <a name="set-up-drillthrough-to-a-mobile-report"></a>모바일 보고서에 드릴스루 설정  

1. [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]의 레이아웃 뷰에서 드릴스루를 지원하는 시각화를 선택합니다.   

   대부분의 차트 및 간단한 데이터 표와 마찬가지로 지도와 계기도 드릴스루를 지원합니다.
   
2. **Visual 속성** 창에서 **드릴스루 대상** > **모바일 보고서**를 선택합니다.  
3. 서버와 대상 모바일 보고서를 선택합니다.  

   >참고: 대상 모바일 보고서가 원본 모바일 보고서와 다른 서버에 있을 경우 다음 섹션에 설명된 대로 사용자 지정 URL을 사용하여 연결합니다.  
 
4. 대상 모바일 보고서를 선택하면 탐색기 컨트롤에 바인딩될 수 있는 속성과 대상 모바일 보고서의 데이터 세트에 구성된 매개 변수를 포함하여 사용 가능한 입력 매개 변수가 표시됩니다.  

   ![mobile-report-drillthrough-target](../../reporting-services/mobile-reports/media/mobile-report-drillthrough-target.PNG)
   
   *대상 모바일 보고서의 드릴스루 속성*  
  
5. 일치하는 데이터 형식의 속성을 원본 모바일 보고서의 사용 가능한 출력 속성에 연결하려면 각 속성의 오른쪽에 있는 화살표를 선택합니다. 보고서 사용자가 대상 모바일 보고서로 드릴스루하기 전에 원본 모바일 보고서를 조작하지 않은 경우 여기서 각 출력에 대한 기본값을 설정할 수도 있습니다.  
  
## <a name="set-up-a-drillthrough-to-a-custom-url"></a>사용자 지정 URL에 대한 드릴스루 설정  
  
1. [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]의 레이아웃 뷰에서 드릴스루 대상을 지원하는 시각화를 선택합니다.    
2. **Visual 속성** 창에서 **드릴스루 대상** > **사용자 지정 URL**을 선택합니다.  드릴스루 구성 대화 상자가 열립니다.  
  
3. **드릴스루 URL 설정**에서 시각화를 클릭할 때 이동할 대상 URL을 입력하고 오른쪽에 나열된 **사용 가능한 매개 변수** 중에서 선택합니다. 확인된 샘플 매개 변수(포함된 경우)와 함께 사용자 지정 URL의 미리 보기가 아래 패널에 표시됩니다.  
  
   ![mobile-report-drillthrough-url](../../reporting-services/mobile-reports/media/mobile-report-drillthrough-url.PNG)
  
   *사용자 지정 URL에 대한 드릴스루 속성*  
  
4. **적용**을 클릭합니다.  

  
[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]에서 모바일 보고서를 미리 볼 때 드릴스루가 있는 시각화를 클릭하면 드릴스루를 사용할 수 없다는 메시지가 표시됩니다. [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 레이아웃 또는 미리 보기 모드 내에서가 아니라 모바일 보고서를 저장하거나 게시한 다음 본 후에만 실제로 대상에 드릴스루할 수 있습니다.  

## <a name="hide-a-target-mobile-report-on-the-web-portal"></a>웹 포털에서 대상 모바일 보고서 숨기기
대상 보고서에 대한 기본값을 설정하지 않으려는 경우 웹 포털에서 숨기는 것이 좋습니다. 숨기지 않으면 사용자가 원본 보고서를 통해 이동하지 않고 웹 포털에서 직접 보려고 할 경우 대상 보고서가 비어 있습니다.

1. 웹 포털에서 숨기려는 대상 보고서의 줄임표(...)를 선택한 다음 관리를 선택합니다.

2. **속성**에서 **바둑판식 뷰에서 숨기기**를 선택합니다.

웹 포털에서 숨겨진 항목을 표시하도록 선택할 수 있습니다. 

* 웹 포털의 오른쪽 위에서 **보기** > **숨김 표시**를 선택합니다. 

숨겨진 항목은 더 밝은 색으로 표시됩니다.
    
### <a name="see-also"></a>참고 항목  
 
* [Reporting Services 모바일 보고서에 매개 변수 추가](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [SQL Server 모바일 보고서 게시자를 사용하여 모바일 보고서 만들기](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 
* [웹 포털(SSRS 기본 모드)](../../reporting-services/web-portal-ssrs-native-mode.md)

