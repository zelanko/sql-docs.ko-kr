---
title: 페이지 헤더 및 바닥글(보고서 작성기 및 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10125"
- sql13.rtp.rptdesigner.pagefooter.border.f1
- "10121"
- "10120"
- "10122"
- sql13.rtp.rptdesigner.pageheader.general.f1
- "10123"
- sql13.rtp.rptdesigner.pageheader.fill.f1
- sql13.rtp.rptdesigner.pageheader.border.f1
- sql13.rtp.rptdesigner.pagefooter.fill.f1
- sql13.rtp.rptdesigner.pagefooter.general.f1
- "10124"
ms.assetid: 4fb9faac-511e-404a-b8d7-1f2e3cb47b11
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b03f701a40c97d5958e5e8b2146844f335d64724
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56298641"
---
# <a name="page-headers-and-footers-report-builder-and-ssrs"></a>페이지 머리글 및 바닥글(보고서 작성기 및 SSRS)
  보고서는 각 페이지의 위쪽과 아래쪽에서 각기 실행되는 머리글과 바닥글을 포함할 수 있습니다. 머리글과 바닥글에는 정적 텍스트, 이미지, 선, 사각형, 테두리, 배경색, 배경 이미지 및 식이 들어갈 수 있습니다. 식에는 단 하나의 데이터 세트와 데이터 세트를 범위로 포함하는 집계 함수 호출이 있는 보고서용 데이터 세트 필드 참조가 포함됩니다.  
  
> [!NOTE]  
>  각 렌더링 확장 프로그램에서는 페이지를 다르게 처리합니다. 보고서 페이지 매김 및 렌더링 확장 프로그램에 대한 자세한 내용은 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)를 참조하세요.  
  
 기본적으로 보고서에는 페이지 바닥글은 있지만 페이지 머리글은 없습니다. 헤더 및 바닥글을 추가하거나 제거하는 방법에 대한 자세한 내용은 [페이지 헤더 및 바닥글 추가 또는 제거&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)를 참조하세요.  
  
 머리글과 바닥글에는 일반적으로 페이지 번호, 보고서 제목 및 기타 보고서 속성이 포함됩니다. 이러한 항목을 보고서 헤더 또는 바닥글에 추가하는 방법에 대한 자세한 내용은 [페이지 번호 또는 기타 보고서 속성 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md)를 참조하세요.  
  
 페이지 머리글 또는 바닥글을 만들면 모든 보고서 페이지에 표시됩니다. 첫 번째와 마지막 페이지에서 페이지 헤더 및 바닥글을 표시하지 않는 방법에 대한 자세한 내용은 [첫 페이지 또는 마지막 페이지에서 페이지 헤더 또는 바닥글 숨기기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-headers-and-footers"></a>보고서 머리글 및 바닥글  
 페이지 머리글 및 바닥글은 보고서 머리글 및 바닥글과 다릅니다. 보고서에는 특별한 보고서 머리글 또는 보고서 바닥글 영역이 없습니다. 보고서 머리글은 보고서 디자인 화면에서 보고서 본문의 맨 위에 입력되는 보고서 항목으로 구성됩니다. 따라서 보고서의 첫 내용으로 한 번만 나타납니다. 보고서 바닥글은 보고서 본문의 맨 아래에 입력되는 보고서 항목으로 구성됩니다. 따라서 보고서의 마지막 내용으로 한 번만 나타납니다.  
  
## <a name="displaying-variable-data-in-a-page-header-or-footer"></a>페이지 머리글 또는 바닥글에 변수 데이터 표시  
 페이지 머리글 및 바닥글은 정적인 내용을 표시하는 데도 사용할 수 있지만 일반적으로 페이지 내용에 대한 정보 또는 페이지 번호 등의 변화하는 내용을 표시하는 데 사용합니다. 페이지마다 달라지는 변수 데이터를 표시하려면 식을 사용해야 합니다.  
  
 보고서에 한 데이터 세트만 정의되어 있는 경우에는 `[FieldName]` 같은 간단한 식을 페이지 머리글 또는 바닥글에 추가할 수 있습니다. 보고서 데이터 창 데이터 세트 필드 컬렉션 또는 기본 제공 필드 컬렉션에서 페이지 머리글이나 페이지 바닥글로 필드를 끄십시오. 적절한 식이 있는 입력란이 자동으로 추가됩니다.  
  
 페이지에 있는 값의 합계 또는 기타 집계를 계산하려면 ReportItems 또는 데이터 세트 이름을 지정하는 집계 식을 사용하면 됩니다. ReportItems 컬렉션은 보고서 렌더링이 발생한 후 각 페이지의 입력란 컬렉션입니다. 데이터 세트 이름은 보고서 정의에 있어야 합니다. 다음 표에서는 각 유형의 집계 식에서 지원되는 항목을 보여 줍니다.  
  
|식에서의 지원 여부|ReportItems 집계|데이터 세트 집계(범위는 데이터 세트의 이름이어야 함)|  
|-----------------------------|----------------------------|----------------------------------------------------------|  
|보고서 본문에 있는 입력란|예|아니오|  
|&PageNumber|예|아니오|  
|&TotalPages|예|아니오|  
|집계 함수|예 예:<br /><br /> `=First(ReportItems!TXT_LastName.Value)`|예 예:<br /><br /> `=Max(Quantity.Value,"DataSet1")`|  
|페이지에 있는 항목의 필드 컬렉션|간접적임. 예:<br /><br /> `=Sum(ReportItems!Textbox1.Value)`|예 예:<br /><br /> `=Sum(Fields!Quantity.Value,"DataSet1")`|  
|데이터 바인딩된 이미지|간접적임. 예: `=ReportItems!TXT_Photo.Value`|예 예:<br /><br /> `=First(Fields!Photo.Value,"DataSet1")`|  
  
 이 항목의 다음 섹션에서는 머리글 및 바닥글에 일반적으로 사용하는 변수 데이터를 가져오는 미리 만들어 놓은 식을 보여 줍니다. Excel 렌더링 확장 프로그램에서 머리글 및 바닥글을 처리하는 방법에 대한 섹션도 있습니다. 식에 대한 자세한 내용은 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
### <a name="adding-calculated-page-totals-to-a-header-or-footer"></a>머리글 또는 바닥글에 계산된 페이지 합계 추가  
 일부 보고서의 경우 각 보고서의 머리글 또는 바닥글에 계산된 값(예: 페이지에 숫자 값이 있는 경우 페이지당 총 합계)을 포함하면 유용합니다. 필드를 직접 참조할 수 없으므로 머리글 또는 바닥글에 삽입하는 식은 데이터 필드 대신 입력란과 같은 보고서 항목의 이름을 참조해야 합니다.  
  
 `=Sum(ReportItems!Textbox1.Value)`  
  
 반복되는 데이터 행을 포함하는 테이블 또는 목록에 입력란이 있는 경우 런타임에 머리글 또는 바닥글에 나타나는 값은 현재 페이지의 테이블 또는 목록에 있는 모든 `TextBox1` 인스턴스 데이터 값의 합계입니다.  
  
 페이지 합계를 계산할 때 다른 렌더링 확장 프로그램을 사용하여 보고서를 보면 합계가 서로 다를 수 있습니다. 각 렌더링 확장 프로그램마다 페이지가 매겨진 출력을 다르게 계산합니다. HTML로 본 페이지를 PDF로 보면 PDF 페이지의 데이터 양이 다른 경우 합계가 다를 수 있습니다. 자세한 내용은 [렌더링 동작&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)을 참조하세요.  
  
### <a name="for-reports-with-multiple-datasets"></a>데이터 세트가 여러 개인 보고서의 경우  
 데이터 세트가 여러 개인 보고서의 경우에는 머리글 또는 바닥글에 필드 또는 데이터 바인딩된 이미지를 직접 추가할 수 없습니다. 그러나 머리글 또는 바닥글에 사용할 데이터 바인딩된 필드나 이미지를 간접적으로 참조하는 식은 작성할 수 있습니다.  
  
 머리글 또는 바닥글에 변수 데이터를 삽입하려면  
  
-   머리글 또는 바닥글에 입력란을 추가합니다.  
  
-   입력란에 나타낼 변수 데이터를 생성하는 식을 작성합니다.  
  
-   식에 페이지의 보고서 항목에 대한 참조를 포함시킵니다. 예를 들어 특정 필드의 데이터를 포함하는 입력란을 참조할 수 있습니다. 데이터 세트의 필드에 대한 직접적인 참조는 포함시키지 않습니다. 예를 들어 `[LastName]`식은 사용할 수 없습니다. 다음 식을 사용하여 `TXT_LastName`이라는 입력란의 첫 번째 인스턴스 내용을 표시할 수 있습니다.  
  
     `=First(ReportItems!TXT_LastName.Value)`  
  
 페이지 머리글 또는 바닥글의 필드에는 집계 함수를 사용할 수 없습니다. 보고서 본문에 있는 보고서 항목에만 집계 함수를 사용할 수 있습니다. 페이지 헤더 및 바닥글에 일반적으로 사용하는 식에 대한 자세한 내용은 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)를 참조하세요.  
  
#### <a name="adding-a-data-bound-image-to-a-header-or-footer"></a>머리글 또는 바닥글에 데이터 바인딩된 이미지 추가  
 데이터베이스에 저장된 이미지 데이터를 머리글 또는 바닥글에 사용할 수 있습니다. 그러나 이미지 보고서 항목에서 직접 데이터베이스 필드를 참조할 수는 없습니다. 대신 보고서 본문에 입력란을 추가한 다음 해당 입력란을 이미지를 포함하는 데이터 필드로 설정해야 합니다. 이때 값은 base64로 인코딩되어야 합니다. 보고서 본문에서 입력란을 숨겨 base64로 인코딩된 이미지를 표시하지 않을 수 있습니다. 그런 다음 페이지 머리글 또는 바닥글의 이미지 보고서 항목에서 숨겨진 입력란의 값을 참조할 수 있습니다.  
  
 예를 들어 제품 정보 페이지로 구성된 보고서의 각 페이지에 있는 머리글에 제품의 사진을 표시하려는 경우를 가정합니다. 보고서 머리글에 저장된 이미지를 인쇄하려면 보고서 본문에 데이터베이스에서 이미지를 검색하는 `TXT_Photo` 라는 숨겨진 입력란을 정의하고 식을 사용하여 이 입력란에 값을 제공합니다.  
  
 `=Convert.ToBase64String(Fields!Photo.Value)`  
  
 이미지를 표시하도록 디코딩된 `TXT_Photo` 입력란을 사용하는 Image 보고서 항목을 머리글에 추가합니다.  
  
 `=Convert.FromBase64String(ReportItems!TXT_Photo.Value)`  
  
## <a name="using-headers-and-footers-to-position-text"></a>머리글 및 바닥글을 사용하여 텍스트 배치  
 머리글 및 바닥글을 사용하여 페이지에 텍스트를 배치할 수 있습니다. 예를 들어 고객에게 우편으로 전송할 보고서를 만드는 경우 머리글 또는 바닥글을 사용하여 봉투를 접었을 때 고객 주소가 봉투 창의 주소 부분에 나타나도록 배치할 수 있습니다.  
  
 머리글 또는 바닥글을 입력란으로만 채우는 경우 보고서 본문에서 입력란을 숨길 수 있습니다. 보고서 본문에 입력란을 배치하면 값이 보고서 첫 페이지의 머리글 또는 바닥글에 나타나는지, 아니면 마지막 페이지의 머리글 또는 바닥글에 나타나는지에 영향을 줄 수 있습니다. 예를 들어 보고서가 여러 페이지로 확장되도록 하는 테이블, 행렬 또는 목록이 있는 경우 숨겨진 입력란 값은 마지막 페이지에 나타납니다. 첫 페이지에 나타나도록 하려면 숨겨진 입력란을 보고서 본문의 위쪽에 배치합니다.  
  
## <a name="designing-reports-with-page-headers-and-footers-for-specific-renderers"></a>특정 렌더러에 대해 페이지 머리글 및 바닥글로 보고서 디자인  
 보고서가 처리될 때 데이터와 레이아웃 정보가 결합됩니다. 보고서를 볼 때는 결합된 정보가 각 보고서 페이지에 어느 정도의 보고서 데이터가 맞는지를 결정하는 렌더러에 전달됩니다.  
  
 브라우저를 사용하여 보고서 서버에서 보고서를 보는 경우 표시되는 보고서 페이지의 콘텐츠를 HTML 렌더러가 제어합니다. 현재 보고 있는 형식과 다른 형식으로 보고서를 제공할 계획이거나 특정 형식으로 보고서를 인쇄할 계획이면 최종 보고서 형식에 사용할 렌더러에 맞게 보고서 레이아웃을 최적화할 수 있습니다. 보고서 페이지 매김에 대한 자세한 내용은 [Reporting Services의 페이지 매김&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)를 참조하세요.  
  
### <a name="working-with-page-headers-and-footers-in-excel"></a>Excel에서의 페이지 머리글 및 바닥글 작업  
 Excel 렌더링 확장 프로그램을 대상으로 하는 보고서에 대해 페이지 머리글 및 바닥글을 정의하는 경우 다음 지침을 따르면 가장 좋은 결과를 얻을 수 있습니다.  
  
-   페이지 바닥글을 사용하여 페이지 번호를 표시합니다.  
  
-   페이지 머리글을 사용하여 이미지, 제목 또는 기타 텍스트를 표시합니다. 머리글에는 페이지 번호를 삽입하지 마십시오.  
  
 Excel에서 페이지 바닥글은 레이아웃이 제한되어 있습니다. 페이지 바닥글에 복잡한 보고서 항목을 포함하는 보고서를 정의하면 Excel에서 해당 보고서를 볼 때 페이지 바닥글이 예상과 다르게 처리될 수 있습니다.  
  
 Excel 렌더링 확장 프로그램에서는 페이지 머리글에 이미지 및 단순 또는 복잡한 보고서 항목의 절대 위치를 수용할 수 있습니다. 페이지 머리글 레이아웃이 보다 다양하게 지원되지만 이로 인해 머리글에서의 페이지 번호 계산 기능이 제한을 받게 됩니다. Excel 렌더링 확장 프로그램에서는 기본적으로 워크시트 수를 기반으로 페이지 번호를 계산하며 보고서 정의 방법에 따라 잘못된 페이지 번호가 생성될 수 있습니다. 예를 들어 4장의 페이지로 인쇄되며 하나의 큰 워크시트로 렌더링되는 보고서가 있는 경우 머리글에 페이지 번호 정보를 포함하면 인쇄되는 각 페이지의 머리글에 "1페이지 중 1페이지"가 표시됩니다.  
  
 보다 정확한 페이지 수는 인쇄된 페이지의 차원과 상호 관련된 논리 페이지를 기반으로 합니다. Excel에서는 페이지 바닥글에 자동으로 논리 페이지 번호가 사용됩니다. 페이지 머리글에 논리 페이지 수를 삽입하려면 간단한 머리글을 사용하도록 디바이스 정보 설정을 구성해야 합니다. 간단한 머리글을 사용하면 머리글 영역에서 복잡한 보고서 레이아웃을 처리하는 기능이 제거됩니다.  
  
 자세한 내용은 [Microsoft Excel로 내보내기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)에서 이 데이터로 작업할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서에 이미지 포함&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [사각형 및 선&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)  
  
  
