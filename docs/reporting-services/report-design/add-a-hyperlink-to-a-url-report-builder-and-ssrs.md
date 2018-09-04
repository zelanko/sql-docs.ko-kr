---
title: URL에 하이퍼링크 추가(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 09/07/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 756cde54f9379ad5caabedfe9b0adcace65b1605
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43277473"
---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>URL에 하이퍼링크 추가(보고서 작성기 및 SSRS)
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]  의 페이지를 매긴 보고서에서 입력란, 이미지, 차트 및 계기에 하이퍼링크 동작을 추가하는 방법을 알아봅니다. 링크를 통해 다른 보고서, 보고서의 책갈피 또는 정적 또는 동적 URL로 이동할 수 있습니다. 

 입력란, 이미지 또는 차트의 계산된 계열과 같이 **동작** 속성이 있는 모든 항목에 하이퍼링크 작업을 추가할 수 있습니다. 정의한 동작은 사용자가 해당 보고서 항목을 클릭할 때 발생합니다.  
  
*   지정하는 **URL로 브라우저를 여는 하이퍼링크를 추가** 할 수 있습니다. 하이퍼링크는 정적 URL 및 URL을 반환하는 식이 될 수 있습니다. URL을 포함하는 데이터베이스에 필드가 있는 경우 식에 해당 필드가 포함될 수 있으므로 보고서에 하이퍼링크의 동적 목록이 생깁니다. 지정하는 URL에 보고서를 읽는 사람이 액세스할 수 있도록 합니다.  
   
*  보고서 서버에 대한 URL 요청을 사용하여 개발자와 사용자가 모두 볼 수 있는 보고서 서버의 보고서에 **드릴스루를 만들 URL을 지정** 할 수도 있습니다. 예를 들어 보고서를 지정한 다음 사용자가 처음으로 해당 보고서를 볼 때 문서 구조를 숨길 수 있습니다. 자세한 내용은 [URL 액세스 &#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md) 및 [외부 항목에 대한 경로 지정&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)를 참조하세요.
 
 *  동일한 보고서에서 **특정 위치에 책갈피를 추가** 할 수 있습니다. 
  
[자습서: 텍스트 서식 지정&#40;보고서 작성기&#41;](../../reporting-services/tutorial-format-text-report-builder.md)에서 샘플 데이터를 사용하여 하이퍼링크를 추가해 보세요.  
  
> [!NOTE]  
>  데이터 집합 필드에 바인딩된 링크는 악의적 의도를 가진 사용자가 임의로 변경할 수도 있습니다. 자세한 내용은 [보안 보고서 및 리소스](../../reporting-services/security/secure-reports-and-resources.md)를 참조하세요.  
  
## <a name="to-add-a-hyperlink-and"></a>하이퍼링크를 추가하려면...   
  
1.  보고서 디자인 뷰에서 링크를 추가하려는 입력란, 이미지 또는 차트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  속성 대화 상자에서 **동작** 탭을 클릭합니다. 옵션에 대한 내용을 확인하세요.  

## <a name="-add-drillthrough-to-another-report"></a>다른 보고서에 드릴스루를 추가하려면

1. **동작** 탭에서 **보고서로 이동**을 선택합니다. 

2. 사용할 대상 보고서 및 매개 변수를 지정합니다. 매개 변수 이름은 대상 보고서에 대해 정의된 매개 변수와 일치해야 합니다. 

3. **추가** 단추와 **삭제** 단추를 사용하여 매개 변수를 추가 및 제거하고 위쪽 화살표와 아래쪽 화살표를 사용하여 매개 변수 목록의 순서를 지정합니다.

4.  드릴스루 보고서의 명명된 매개 변수에 전달할 **값** 을 입력하거나 선택합니다. 식을 편집하려면 식(fx) 단추를 클릭합니다.

5. **생략** 을 선택하여 매개 변수가 실행되지 않도록 합니다. 기본적으로 이 확인란은 선택 취소하여 비활성화되어 있습니다. 확인란을 선택하려면 식(fx) 단추를 클릭하고 True를 입력하거나 식을 만듭니다. 식 대화 상자에서 **확인** 을 클릭하면 확인란이 선택됩니다.
  
   자세한 내용은 [보고서에 드릴스루 동작 추가](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md) 를 참조하세요. 
   
6. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
   
## <a name="-add-a-bookmark"></a>책갈피를 추가하려면

현재 보고서의 위치에 책갈피로 연결할 수 있습니다. 책갈피로 연결하려면 먼저 보고서 항목의 **책갈피** 속성을 설정해야 합니다. **책갈피** 속성을 설정하려면 보고서 항목을 선택하고 속성 창에서 SalesChart 또는 5TopSales와 같이 책갈피 ID에 대한 값이나 식을 입력합니다.

1. **동작** 탭에서 **책갈피로 이동**을 선택합니다. 

2. 이동할 보고서의 책갈피 ID를 입력하거나 선택합니다. 식을 변경하려면 식 단추(fx)를 클릭합니다. 

   책갈피 ID는 정적 ID이거나 책갈피 ID를 반환하는 식일 수 있습니다. 식은 책갈피 ID가 들어 있는 필드를 포함할 수 있습니다.
   
   자세한 내용은 [보고서에 책갈피 추가](../../reporting-services/report-design/add-a-bookmark-to-a-report-report-builder-and-ssrs.md) 를 참조하세요.
   
3. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="-add-a-hyperlink"></a>...하이퍼링크 추가 
  
1. **작업** 탭에서 **URL로 이동**을 선택합니다. 이 옵션에 대한 추가 섹션이 대화 상자에 나타납니다.  
  
4.  **URL 선택**에서 URL이나 URL로 계산되는 식을 입력 또는 선택하거나, 드롭다운 화살표를 클릭하고 URL이 들어 있는 필드 이름을 클릭합니다. 

    기본 모드로 구성된 보고서 서버에 게시된 항목의 경우 전체 경로나 상대 경로를 사용합니다. `http://<servername>/images/image1.jpg`)을 입력합니다. 
    
    SharePoint 통합 모드로 구성된 보고서 서버에 게시된 항목의 경우 정규화된 URL을 사용합니다. `http://<SharePointservername>/<site>/Documents/images/image1.jpg`)을 입력합니다.
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="after-you-add-a-hyperlink"></a>하이퍼링크를 추가한 후
  
1.  (선택 사항) 텍스트가 자동으로 링크로 서식이 지정되지는 않습니다. 텍스트의 경우 텍스트가 링크임을 나타내기 위해 텍스트 색과 효과를 변경하는 것이 좋습니다. 예를 들어 리본 메뉴의 홈 탭에 있는 **글꼴** 섹션에서 색을 파란색으로 변경하고 효과를 밑줄로 변경합니다.  
  
7.  링크를 테스트하려면 **실행** 을 클릭하여 보고서를 미리 본 다음, 이 링크를 설정한 보고서 항목을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [대화형 정렬, 문서 구조 및 링크&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [문서 구조 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/create-a-document-map-report-builder-and-ssrs.md)  
  
  
