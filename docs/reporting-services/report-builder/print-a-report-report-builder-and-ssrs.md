---
title: 보고서 인쇄(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: b96936c9-c387-41a9-8c19-6eb325769ffd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b1d0877c14b3ce34c69e667c074fd0c95dcb250d
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50031402"
---
# <a name="print-a-report-report-builder-and-ssrs"></a>보고서 인쇄(보고서 작성기 및 SSRS)
  보고서 서버에 보고서를 저장한 후에는 브라우저, Reporting Services 웹 포털 또는 내보낸 보고서를 보는 데 사용되는 애플리케이션에서 보고서를 보고 인쇄할 수 있습니다. 보고서를 저장하기 전 미리 볼 때 해당 보고서를 인쇄할 수 있습니다.  
  
 보고서를 인쇄할 때 사용할 용지 크기를 지정할 수 있습니다. 용지 크기에 따라 보고서의 페이지 수와 각 페이지에 맞는 보고서 데이터가 결정됩니다. 용지 크기는 PDF, 이미지 및 인쇄 하드 페이지 나누기 렌더러로 렌더링되는 보고서에만 적용됩니다. 용지 크기 설정 작업은 다른 렌더러에 영향을 주지 않습니다. 자세한 내용은 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)을 참조하세요.  
  
 Reporting Services 웹 포털의 보고서 뷰어 도구 모음 또는 보고서 작성기의 미리 보기에서 보고서를 하드 페이지 나누기 렌더러로 내보내거나 인쇄 단추를 클릭하여 보고서의 복사본을 인쇄할 수 있습니다. 용지 크기 또는 다른 페이지 설정 속성을 지정해야 할 수 있습니다. 용지 크기를 비롯한 페이지 설정 속성을 변경하려면 **보고서 속성** 대화 상자를 사용합니다.  
  
 인쇄 페이지 여백은 디자인 모드와 실행 모드에서 지정할 수 있습니다.  
  
-   **디자인 모드.** 디자인 모드에서 페이지 여백을 설정하면 보고서를 저장할 때 해당 설정이 보고서 정의에 저장됩니다.  
  
-   **실행 모드.** 실행 모드에서 페이지 여백을 설정하면 해당 정보가 보고서 정의에 저장되지 않습니다. 다음에 보고서를 인쇄할 때는 인쇄 여백을 다시 지정하지 않는 한 보고서 정의에서 설정을 가져옵니다.  
  
    > [!NOTE]  
    >  인쇄 여백은 디자인 모드나 실행 모드에서 표시되지 않습니다. 보고서의 디자인 화면 영역과 인쇄 영역 간에는 어떠한 관계도 없습니다. 실행 모드에서 인쇄 여백을 확인하려면 리본 메뉴의 **실행** 탭에서 인쇄 레이아웃을 클릭합니다.  
  
 보고서 페이지 매김에 대한 자세한 내용은 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-print-a-report-in-report-builder"></a>보고서 작성기에서 보고서를 인쇄하려면  
  
1.  보고서를 엽니다.  
  
2.  홈 탭에서 **실행**을 클릭합니다.  
  
3.  (옵션) **인쇄 레이아웃** 을 클릭하여 보고서가 인쇄되었을 때의 모양을 확인합니다.  
  
4.  (옵션) **페이지 설정** 을 클릭하여 용지, 방향 및 여백을 설정합니다.  
  
    > [!NOTE]  
    >  이러한 값은 디자인 뷰에서 설정한 보고서 속성의 값을 기본값으로 사용합니다. **페이지 설정** 대화 상자의 이 부분에서 설정하는 값은 이 세션에만 적용됩니다. 이 보고서를 닫은 후 다시 열면 기본값으로 다시 설정됩니다.  
  
5.  **인쇄**를 클릭합니다.  
  
6.  **인쇄** 대화 상자에서 프린터를 선택하고 다른 인쇄 옵션을 지정합니다.  
  
### <a name="to-print-a-report-from-a-web-browser-application"></a>웹 브라우저 애플리케이션에서 보고서를 인쇄하려면  
  
1.  Reporting Services 웹 포털에서 인쇄하려는 보고서로 이동합니다. 보고서를 엽니다.  
  
3.  보고서 맨 위의 도구 모음에서 **인쇄**를 클릭합니다.  
  
    > [!NOTE]  
    >  HTML 보고서를 처음 인쇄하는 경우에는 보고서 서버에서 인쇄에 사용할 ActiveX 컨트롤을 설치하라는 메시지를 표시합니다. 인쇄하려면 컨트롤을 설치하고 구성해야 합니다.  
  
4.  **인쇄** 대화 상자에서 프린터를 선택한 후 **인쇄**를 클릭합니다.  
  
### <a name="to-print-a-report-from-other-applications"></a>다른 애플리케이션에서 보고서를 인쇄하려면  
  
1.  Reporting Services 웹 포털에서 인쇄하려는 보고서로 이동합니다. 보고서를 엽니다.  
  
2.  보고서 맨 위의 도구 모음에서 렌더링 형식을 선택하고 **내보내기**를 클릭합니다. 렌더링 형식에 맞는 뷰어 애플리케이션에서 보고서가 열립니다.  
  
     예를 들어 PDF를 선택한 경우 Adobe Acrobat Reader에서 보고서가 열립니다.  
  
3.  해당 프로그램의 **파일** 메뉴에서 **인쇄**를 클릭합니다.  
  
### <a name="to-change-paper-size"></a>용지 크기를 변경하려면  
  
1.  보고서 본문 바깥쪽을 마우스 오른쪽 단추로 클릭하고 **보고서 속성**을 클릭합니다.  
  
2.  **페이지 설정**의 **용지 크기** 목록에서 값을 선택합니다. 각 옵션은 **너비** 및 **높이** 속성을 채웁니다. **너비** 및 **높이** 상자에 숫자 값을 입력하여 사용자 지정 크기를 지정할 수도 있습니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  크기 값에는 사용자의 로캘 설정을 기반으로 하는 기본 단위가 포함됩니다. 다른 단위를 지정하려면 숫자 값 뒤에 cm, mm, pt 또는 pc 등의 물리적 단위 지정자를 입력합니다.  
  
### <a name="to-set-page-margins-in-design-mode"></a>디자인 모드에서 페이지 여백을 설정하려면  
  
-   디자인 화면 주변의 파란색 영역을 마우스 오른쪽 단추로 클릭하고 **보고서 속성**을 클릭한 다음 **페이지 설정** 페이지를 클릭합니다.  
  
### <a name="to-set-page-margins-in-run-mode"></a>실행 모드에서 페이지 여백을 설정하려면  
  
-   **실행** 탭에서 **페이지 설정** 을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 인쇄&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [보고서 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [보고서 속성 대화 상자, 페이지 설정&#40;보고서 작성기&#41;](https://msdn.microsoft.com/library/eb3b5d01-7b82-4808-a58b-9e096742f8c6)   
 [보고서 디자인 뷰&#40;보고서 작성기&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)  
  
  
