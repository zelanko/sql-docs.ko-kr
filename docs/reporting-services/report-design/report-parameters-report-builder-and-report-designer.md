---
title: 보고서 매개 변수(보고서 작성기 및 보고서 디자이너) | Microsoft Docs
description: 이 항목에서는 Reporting Services 보고서 매개 변수의 일반적인 용도와 설정할 수 있는 속성 등에 대해 설명합니다.
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.custom: seodec18
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.date: 12/06/2018
ms.openlocfilehash: abbda73ac3aeda94ee8752dbbe638d93bc3d5573
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97425131"
---
# <a name="report-parameters-report-builder-and-report-designer"></a>보고서 매개 변수(보고서 작성기 및 보고서 디자이너)

::: moniker range="=sql-server-2016"

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

::: moniker-end

::: moniker range=">=sql-server-2017"

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)]

::: moniker-end

이 항목에서는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 매개 변수의 일반적인 용도와 설정할 수 있는 속성 등에 대해 설명합니다. 보고서 매개 변수를 사용하면 보고서 데이터를 제어하고, 관련된 보고서를 서로 연결하고, 다양하게 보고서를 표현할 수 있습니다. [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] 및 보고서 디자이너에서 생성한 페이지를 매긴 보고서와 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]에서 생성한 모바일 보고서에서도 보고서 매개 변수를 사용할 수 있습니다. 자세한 내용은 [보고서 매개 변수 개념](../../reporting-services/report-design/report-parameters-concepts-report-builder-and-ssrs.md)을 참조하세요.  

직접 보고서에 매개 변수를 추가하려면 [자습서: 보고서에 매개 변수 추가&#40;보고서 작성기&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)에서 만드는 모바일 보고서에서 보고서 매개 변수를 사용할 수 있습니다.  

## <a name="common-uses-for-parameters"></a><a name="bkmk_Common_Uses_for_Parameters"></a> 매개 변수의 일반적인 용도

 다음은 매개 변수를 사용하는 가장 일반적인 몇 가지 방법입니다.  
  
**페이지를 매긴 보고서 및 모바일 보고서 데이터 제어**
  
- 변수를 포함하는 데이터 세트 쿼리를 작성하여 데이터 원본에서 페이지를 매긴 보고서 데이터를 필터링합니다.  
  
- 공유 데이터 세트에서 데이터를 필터링합니다. 페이지를 매긴 보고서에 공유 데이터 세트를 추가하면 쿼리를 변경할 수 없습니다. 만들어진 보고서 매개 변수에 대한 참조가 포함되어 있는 데이터 세트 필터를 보고서에 추가할 수 있습니다.  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모바일 보고서의 공유 데이터 세트에서 데이터를 필터링합니다. 자세한 내용은 [Create mobile reports with SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) 을 참조하세요.  
  
- 사용자가 값을 지정하여 페이지를 매긴 보고서의 데이터를 사용자 지정할 수 있도록 합니다. 예를 들어 매출 데이터의 시작 날짜와 종료 날짜에 대한 두 개의 매개 변수를 제공합니다.  
  
**관련된 보고서 연결**
  
- 매개 변수를 사용하여 주 보고서를 드릴스루 보고서, 하위 보고서 및 링크된 보고서에 연결합니다. 일련의 보고서를 디자인할 때 특정 질문에 응답하도록 각 보고서를 디자인할 수 있습니다. 각 보고서는 관련된 세부 정보를 다른 뷰 또는 다른 수준으로 표시할 수 있습니다. 서로 관련된 일련의 보고서를 제공하려면 대상 보고서의 관련 데이터에 대한 매개 변수를 만듭니다.  
  
    자세한 내용은 [드릴스루 보고서&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/drillthrough-reports-report-builder-and-ssrs.md), [하위 보고서&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md) 및 [연결된 보고서 만들기](../../reporting-services/reports/create-a-linked-report.md)를 참조하세요.  

- 여러 사용자에 대한 매개 변수 집합을 사용자 지정합니다. 보고서 서버에서 판매 보고서를 기반으로 하는 링크된 보고서 두 개를 만듭니다. 한 링크된 보고서에서는 영업 사원에 대해 미리 정의된 매개 변수 값을 사용하고 링크된 나머지 보고서에서는 영업 관리자에 대해 미리 정의된 매개 변수 값을 사용합니다. 두 보고서 모두 동일한 보고서 정의를 사용합니다.  
  
**다양한 보고서 표현**
  
- URL 요청을 통해 보고서 서버에 보고서의 렌더링을 사용자 지정하는 명령을 보냅니다. 자세한 내용은 [URL 액세스&#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md) 및 [URL에 보고서 매개 변수 전달](../../reporting-services/pass-a-report-parameter-within-a-url.md)을 참조하세요.  
  
- 사용자가 값을 지정하여 보고서 모양을 사용자 지정할 수 있도록 합니다. 예를 들어 테이블에서 중첩된 모든 행 그룹을 확장하거나 축소할 것인지 여부를 나타내는 부울 매개 변수를 제공합니다.  
  
- 사용자는 식에 매개 변수를 포함하여 보고서 데이터 및 모양을 사용자 지정할 수 있습니다.  
  
    자세한 내용은 [매개 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)를 참조하세요.  
  
## <a name="viewing-a-report-with-parameters"></a><a name="UserInterface"></a> 매개 변수가 있는 보고서 보기

매개 변수가 있는 보고서를 보는 경우 보고서 뷰어 도구 모음에 각 매개 변수가 표시되므로 대화형으로 값을 지정할 수 있습니다. 다음 그림에서는 @ReportMonth, @ReportYear, @EmployeeID, @ShowAll, @ExpandTableRows, @CategoryQuota 및 @SalesDate 매개 변수를 포함하는 매개 변수 영역을 보여줍니다.  

![매개 변수가 있는 보고서 보기](../../reporting-services/report-design/media/ssrb-rptparamviewrpt.png "매개 변수가 있는 보고서 보기")  
  
1. **매개 변수 창** 보고서 뷰어 도구 모음에 프롬프트와 각 매개 변수에 대한 기본값이 표시됩니다. 매개 변수 창에서 매개 변수 레이아웃을 사용자 지정할 수 있습니다. 자세한 내용은 [보고서에서 매개 변수 창 사용자 지정&#40;보고서 작성기&#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)에서 만드는 모바일 보고서에서 보고서 매개 변수를 사용할 수 있습니다.  
  
2. **\@SalesDate 매개 변수**@SalesDate 매개 변수는 **DateTime** 데이터 형식입니다. 날짜 선택 프롬프트가 입력란 옆에 표시됩니다. 이 날짜를 수정하려면 입력란에 새 날짜를 입력하거나 달력 컨트롤을 사용합니다.  
  
3. **\@ShowAll 매개 변수**@ShowAll 매개 변수는 **Boolean** 데이터 형식입니다. 라디오 단추를 사용하여 **True** 또는 **False** 를 지정합니다.  
  
4. **매개 변수 영역 핸들 표시 또는 숨기기** 보고서 뷰어 도구 모음에서 이 화살표를 클릭하여 매개 변수 창을 표시하거나 숨깁니다.  
  
5. **\@CategoryQuota 매개 변수**@CategoryQuota 매개 변수는 **Float** 데이터 형식이므로 숫자 값을 사용합니다.  @CategoryQuota은 다중 값 허용하도록 설정됩니다.  
  
6. **보고서 보기**  매개 변수 값을 입력한 후 **보고서 보기** 를 클릭하여 보고서를 실행합니다. 모든 매개 변수에 기본값이 있는 경우 보고서를 처음으로 볼 때 보고서가 자동으로 실행됩니다.  
  
## <a name="creating-parameters"></a><a name="bkmk_Create_Parameters"></a> 매개 변수 만들기

몇 가지 다른 방법으로 보고서 매개 변수를 만들 수 있습니다.
  
> [!NOTE]
>  일부 데이터 원본은 매개 변수를 지원하지 않습니다.
  
**매개 변수가 있는 저장 프로시저 또는 데이터 세트 쿼리**
  
 변수를 포함하는 데이터 세트 쿼리 또는 입력 매개 변수를 포함하는 데이터 세트 저장 프로시저를 추가합니다. 각 변수 또는 입력 매개 변수에 대해 데이터 세트 매개 변수가 생성되며 각 데이터 세트 매개 변수에 대해 보고서 매개 변수가 생성됩니다.  
  
 ![보고서 작성기 매개 변수 데이터 세트 속성](../../reporting-services/report-design/media/ssrb-paramdatasetprops.png "보고서 작성기 매개 변수 데이터 세트 속성")  
  
 보고서 작성기의 이 이미지는 다음을 보여 줍니다.  
  
1.  보고서 데이터 창의 보고서 매개 변수  
  
2.  매개 변수가 있는 데이터 세트.  
  
3.  매개 변수 창  
  
4.  데이터 세트 속성 대화 상자에 나열된 매개 변수.  
  
 데이터 세트는 포함하거나 공유할 수 있습니다. 보고서에 공유 데이터 세트를 추가하면 내부로 표시된 데이터 세트 매개 변수를 보고서에서 재정의할 수 없습니다. 내부로 표시되지 않은 데이터 세트 매개 변수를 재정의할 수 있습니다.  
  
 자세한 내용은 이 항목의 [데이터 세트 쿼리](#bkmk_Dataset_Parameters)를 참조하세요.  
  
**수동으로 매개 변수 만들기**
  
보고서 데이터 창에서 매개 변수를 수동으로 만듭니다. 사용자가 보고서 내용이나 모양을 사용자 지정하기 쉽게 대화형으로 값을 입력할 수 있도록 보고서 매개 변수를 구성할 수 있습니다. 사용자가 미리 구성된 값을 변경하지 못하도록 보고서 매개 변수를 구성할 수도 있습니다.  
  
> [!NOTE]  
>  매개 변수는 서버에서 독립적으로 관리되므로 새 매개 변수 설정을 가진 주 보고서를 다시 게시하더라도 보고서의 기존 매개 변수 설정을 덮어쓰지 않습니다.  
  
 **매개 변수가 있는 보고서 파트**
  
 매개 변수에 대한 참조를 포함하거나 변수가 포함된 공유 데이터 세트를 참조하는 보고서 파트를 추가합니다.  
  
 보고서 파트는 보고서 서버에 저장되며 다른 사용자가 자신의 보고서에 사용할 수 있습니다. 매개 변수인 보고서 파트는 보고서 서버에서 관리할 수 없습니다. 보고서 파트 갤러리에서 매개 변수를 검색하여 추가한 후에 보고서에서 구성할 수 있습니다. 자세한 내용은 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)를 참조하세요.  
  
> [!NOTE]  
>  매개 변수는 매개 변수가 포함된 종속 데이터 세트가 있는 데이터 영역에 대해 개별 보고서 파트로 게시할 수 있습니다. 매개 변수는 보고서 파트로 나열되지만 보고서에 보고서 파트 매개 변수를 직접 추가할 수 없습니다. 대신 보고서 파트를 추가하면 보고서 파트에 의해 포함되었거나 참조되는 데이터 세트 쿼리에서 필요한 보고서 매개 변수가 자동으로 생성됩니다. 보고서 파트에 대한 자세한 내용은 [보고서 파트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md) 및 [보고서 디자이너의 보고서 파트&#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)를 참조하세요.  
  
### <a name="parameter-values"></a>매개 변수 값

 다음은 보고서에서 매개 변수 값을 선택할 수 있는 옵션입니다.  
  
- 드롭다운 목록에서 단일 매개 변수 값을 선택합니다.  
  
- 드롭다운 목록에서 여러 매개 변수 값을 선택합니다.  
  
- 드롭다운 목록에서 단일 매개 변수의 값을 선택합니다. 이 선택에 따라 드롭다운 목록에서 다른 매개 변수에 사용할 수 있는 값이 결정됩니다. 이들은 연계 매개 변수입니다. 연계 매개 변수를 사용하면 수천 개 값의 매개 변수 값을 관리 가능한 수치로 연속적으로 필터링할 수 있습니다.  
  
     자세한 내용은 [보고서에 연계 매개 변수 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)에서 만드는 모바일 보고서에서 보고서 매개 변수를 사용할 수 있습니다.  
  
- 매개 변수의 기본값이 생성되었으므로 먼저 매개 변수 값을 선택하지 않고 보고서를 실행합니다.  
  
## <a name="report-parameter-properties"></a><a name="bkmk_Report_Parameters"></a> 보고서 매개 변수 속성

 보고서 속성 대화 상자를 사용하여 보고서 매개 변수 속성을 변경할 수 있습니다. 다음 표에는 각 매개 변수에 대해 설정할 수 있는 속성이 요약되어 있습니다.  
  
|속성|Description|  
|--------------|-----------------|  
|속성|매개 변수의 대/소문자를 구분하는 이름을 입력합니다. 이 이름은 문자로 시작해야 하고 문자, 숫자 및 밑줄(_)을 포함할 수 있습니다. 이름에 공백은 포함할 수 없습니다. 자동으로 생성된 매개 변수의 경우 이름이 데이터 세트 쿼리의 매개 변수와 일치합니다. 기본적으로 수동으로 만든 매개 변수는 ReportParameter1과 유사합니다.|  
|prompt|보고서 뷰어 도구 모음에서 매개 변수 옆에 표시되는 텍스트입니다.|  
|데이터 형식|보고서 매개 변수는 다음 데이터 형식 중 하나여야 합니다.<br /><br /> **Boolean**. 사용자가 라디오 단추에서 True 또는 False를 선택합니다.<br /><br /> **DateTime**. 사용자가 달력 컨트롤에서 날짜를 선택합니다.<br /><br /> **Integer**. 사용자가 입력란에 값을 입력합니다.<br /><br /> **Float**. 사용자가 입력란에 값을 입력합니다.<br /><br /> **Text**. 사용자가 입력란에 값을 입력합니다.<br /><br /> 매개 변수에 대해 사용할 수 있는 값이 정의된 경우 사용자는 데이터 형식이 **DateTime** 인 경우에도 드롭다운 목록에서 값을 선택합니다.<br /><br /> 보고서 데이터 형식에 대한 자세한 내용은 [RDL Data Types](../../reporting-services/reports/report-definition-language-ssrs.md#bkmk_RDL_Data_Types)을 참조하세요.|  
|빈 값 허용|매개 변수 값에 빈 문자열이나 공백을 허용하려면 이 옵션을 선택합니다.<br /><br /> 매개 변수에 대한 유효한 값을 지정할 경우 공백 값을 유효한 값 중 하나로 허용하려면 지정한 값 중 하나로 공백 값을 포함시켜야 합니다. 이 옵션을 선택해도 사용 가능한 값에 공백이 자동으로 포함되지는 않습니다.|  
|Null 값 허용|매개 변수 값이 Null이 될 수 있도록 허용하려면 이 옵션을 선택합니다.<br /><br /> 매개 변수에 대한 유효한 값을 지정할 경우 null을 유효한 값 중 하나로 허용하려면 지정한 값 중 하나로 null을 포함시켜야 합니다. 이 옵션을 선택해도 사용 가능한 값에 null이 자동으로 포함되지는 않습니다.|  
|다중 값 허용|사용자가 선택할 수 있는 드롭다운 목록을 만드는 데 사용 가능한 값을 제공합니다. 이렇게 하면 데이터 세트 쿼리에서 유효한 값만 제출되도록 할 수 있습니다.<br /><br /> 매개 변수의 값이 드롭다운 목록에 표시되는 다중 값이 될 수 있도록 허용하려면 이 옵션을 선택합니다. Null 값은 허용되지 않습니다. 이 옵션을 선택하면 매개 변수 드롭다운 목록의 사용 가능한 값 목록에 확인란이 추가되고 목록의 맨 위에 **모두 선택** 에 대한 확인란이 포함됩니다. 사용자는 원하는 값을 선택할 수 있습니다.<br /><br /> 값을 제공하는 데이터가 빠르게 변동될 경우 사용자에게 표시되는 목록이 최신 상태가 아닐 수도 있습니다.|  
|Visible|보고서를 실행할 때 보고서 위쪽에 보고서 매개 변수를 표시하려면 이 옵션을 선택합니다. 이 옵션을 설정하면 사용자가 런타임에 매개 변수 값을 선택할 수 있습니다.|  
|숨김|게시된 보고서에서 보고서 매개 변수를 숨기려면 이 옵션을 선택합니다. 보고서 매개 변수 값은 여전히 보고서 URL, 구독 정의 또는 보고서 서버에 설정할 수 있습니다.|  
|내부|보고서 매개 변수를 숨기려면 이 옵션을 선택합니다. 게시된 보고서에서 보고서 매개 변수는 보고서 정의에서만 볼 수 있습니다.|  
|사용 가능한 값|매개 변수에 대해 사용 가능한 값을 지정한 경우에는 유효한 값이 항상 드롭다운 목록으로 표시됩니다. 예를 들어 **DateTime** 매개 변수에 사용할 수 있는 값을 제공하면 날짜에 대한 드롭다운 목록이 달력 컨트롤 대신 매개 변수 창에 표시됩니다.<br /><br /> 값 목록이 보고서와 하위 보고서 간에 일관되도록 하려면 데이터 원본과 연관된 데이터 세트의 모든 쿼리에 단일 트랜잭션을 사용하도록 데이터 원본에서 옵션을 설정할 수 있습니다.<br /><br /> **보안 정보** **텍스트** 데이터 형식의 매개 변수가 포함된 보고서에서는 유효한 값 목록이라고도 하는 사용 가능한 값 목록을 사용해야 하며 보고서를 실행하는 모든 사용자가 보고서의 데이터를 보는 데 필요한 권한만 갖도록 해야 합니다. 자세한 내용은 [보안&#40;보고서 작성기&#41;](../../reporting-services/report-builder/security-report-builder.md)에서 만드는 모바일 보고서에서 보고서 매개 변수를 사용할 수 있습니다.|  
|기본값|쿼리 또는 정적 목록에서 기본값을 설정합니다.<br /><br /> 매개 변수마다 기본값이 있을 경우에는 보고서를 처음으로 볼 때 보고서가 자동으로 실행됩니다.|  
|고급|이 매개 변수가 보고서의 데이터에 직접 또는 간접으로 영향을 주는지를 나타내는 값인 보고서 정의 특성 **UsedInQuery** 를 설정합니다.<br /><br /> **새로 고칠 시기 자동으로 결정**<br /> 보고서 프로세서가 이 값에 대한 설정을 결정하도록 하려면 이 옵션을 선택합니다. 보고서 프로세서가 이 매개 변수에 대한 직접 또는 간접 참조가 있는 데이터 세트 쿼리를 검색하거나 보고서에 하위 보고서가 있으면 **True** 입니다.<br /><br /> **항상 새로 고침**<br /> 보고서 매개 변수가 데이터 세트 쿼리 또는 매개 변수 식에 직접 또는 간접으로 사용되는 경우 이 옵션을 선택합니다. 이 옵션은 **UsedInQuery** 를 True로 설정합니다.<br /><br /> **새로 고침 안 함**<br /> 보고서 매개 변수가 데이터 세트 쿼리 또는 매개 변수 식에 직접 또는 간접으로 사용되지 않는 경우 이 옵션을 선택합니다. 이 옵션은 **UsedInQuery** 를 False로 설정합니다.<br /><br /> **주의** **새로 고침 안 함** 은 주의해서 사용하세요. 보고서 서버에서 **UsedInQuery** 는 보고서 데이터와 렌더링된 보고서의 캐시 옵션 및 스냅샷 보고서의 매개 변수 옵션을 제어하는 데 사용됩니다. **새로 고침 안 함** 을 잘못 설정하면 잘못된 보고서 데이터 또는 보고서가 캐시되거나 스냅샷 보고서에 일치하지 않는 데이터가 포함될 수 있습니다. 자세한 내용은 [RDL(Report Definition Language)&#40;SSRS&#41;](../../reporting-services/reports/report-definition-language-ssrs.md)을 참조하세요.|  
  
##  <a name="dataset-query"></a><a name="bkmk_Dataset_Parameters"></a> 데이터 세트 쿼리  
 데이터 세트 쿼리에서 데이터를 필터링하려면 결과 집합에서 포함하거나 제외할 값을 지정하여 검색된 데이터를 제한하는 제한 절을 포함합니다.  
  
 데이터 원본에 쿼리 디자이너를 사용하여 매개 변수가 있는 쿼리를 작성할 수 있습니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리의 경우 서로 다른 데이터 원본이 매개 변수에 대한 서로 다른 구문을 지원합니다. 위치 또는 이름으로 쿼리에서 식별되는 매개 변수의 범위를 지원합니다. 자세한 내용은 [보고서 데이터 세트&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)에서 특정 외부 데이터 원본 형식에 대한 항목을 참조하세요. 관계형 쿼리 디자이너에서 매개 변수가 있는 쿼리를 만들려면 필터에 대해 매개 변수 옵션을 선택해야 합니다. 자세한 내용은 [관계형 쿼리 디자이너 사용자 인터페이스&#40;보고서 작성기&#41;](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md)를 참조하세요.  
  
-   Microsoft SQL Server Analysis Services, SAP NetWeaver BI 또는 Hyperion Essbase처럼 다차원 데이터 원본을 기반으로 하는 쿼리에서는 쿼리 디자이너에서 지정한 필터를 기반으로 하는 매개 변수를 만들 것인지 여부를 지정할 수 있습니다. 자세한 내용은 [쿼리 디자인 도구&#40;SSRS&#41;](../report-data/query-design-tools-ssrs.md)에서 데이터 확장 프로그램에 해당하는 쿼리 디자이너 항목을 참조하세요.  
  
##  <a name="parameter-management-for-a-published-report"></a><a name="bkmk_Manage_Parameters"></a> 게시된 보고서에 대한 매개 변수 관리  
 보고서를 디자인할 때는 보고서 매개 변수가 보고서 정의에 저장되고, 보고서를 게시할 때는 보고서 매개 변수가 보고서 정의와 별개로 저장되고 관리됩니다.  
  
 게시된 보고서의 경우 다음을 사용할 수 있습니다.  
  
-   **보고서 매개 변수 속성.** 보고서 정의로부터 독립적으로 보고서 서버에서 보고서 매개 변수 값을 직접 변경합니다.  
  
-   **캐시된 보고서.** 보고서에 대한 캐시 계획을 만들려면 각 매개 변수에 기본값이 있어야 합니다. 자세한 내용은 [보고서 캐시&#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)버전에서 캐시를 미리 로드할 수 있는 유일한 방법이었습니다.  
  
-   **캐시된 공유 데이터 세트.** 공유 데이터 세트에 대한 캐시 계획을 만들려면 각 매개 변수에 기본값이 있어야 합니다. 자세한 내용은 [보고서 캐시&#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)버전에서 캐시를 미리 로드할 수 있는 유일한 방법이었습니다.  
  
-   **링크된 보고서.** 다양한 대상에 대한 데이터를 필터링하기 위해 미리 설정된 매개 변수 값을 사용하여 링크된 보고서를 만들 수 있습니다. 자세한 내용은 [연결된 보고서 만들기](../../reporting-services/reports/create-a-linked-report.md)를 참조하세요.  
  
-   **보고서 구독.** 구독을 통해 데이터를 필터링하고 보고서를 전달하는 매개 변수 값을 지정할 수 있습니다. 자세한 내용은 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)을 참조하세요.  
  
-   **URL 액세스.** 보고서 URL에 매개 변수 값을 지정할 수 있습니다. URL 액세스를 사용하여 보고서를 실행하고 매개 변수 값을 지정할 수도 있습니다. 자세한 내용은 [URL 액세스&#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md)를 참조하세요.  
  
 게시된 보고서에 대한 매개 변수 속성은 보고서 정의를 다시 게시할 경우 유지됩니다. 보고서 정의가 동일한 보고서로 다시 게시되고 매개 변수 이름 및 데이터 형식이 그대로 유지되면 속성 설정도 그대로 유지됩니다. 보고서 정의에서 매개 변수를 추가 또는 삭제하거나 데이터 형식 또는 기존 매개 변수의 이름을 변경할 경우 게시된 보고서의 매개 변수 속성을 변경해야 할 수 있습니다.  
  
 매개 변수를 수정할 수 없는 경우도 있습니다. 보고서 매개 변수가 데이터 세트 쿼리에서 기본값을 가져오는 경우 이 값을 게시된 보고서에 맞게 수정하거나 보고서 서버에서 수정할 수 없습니다. 런타임 시 사용되는 값은 쿼리를 실행할 때 결정되거나 식 기반 매개 변수의 경우 식을 계산할 때 결정됩니다.  
  
 보고서 실행 옵션이 매개 변수 처리 방법에 영향을 줄 수 있습니다. 스냅샷으로 실행되는 보고서는 쿼리에 매개 변수의 기본값이 포함되지 않는 한 쿼리에서 파생된 매개 변수를 사용할 수 없습니다.  
  
##  <a name="parameters-for-a-subscription"></a><a name="bkmk_Parameters_Subscription"></a> 구독 매개 변수  
 요청 시 또는 스냅샷에 대한 구독을 정의하고 구독을 처리하는 중에 사용할 매개 변수 값을 지정할 수 있습니다.  
  
-   **요청 시 실행 보고서.**  요청 시 실행 보고서의 경우 보고서에 대해 나열된 각 매개 변수의 게시된 값과는 다른 매개 변수 값을 지정할 수 있습니다. 예를 들어 *Time Period* 매개 변수를 사용하여 현재 날짜, 주 또는 월에 해당하는 고객 서비스 요청을 반환하는 서비스 호출 보고서가 있다고 가정합니다. 보고서의 기본 매개 변수 값이 **today** 로 설정된 경우 구독에서는 다른 매개 변수 값(예: **week** 또는 **month**)을 사용하여 주 또는 월을 나타내는 숫자가 포함된 보고서를 생성할 수 있습니다.  
  
-   **스냅샷.**  스냅샷의 경우 구독에서는 스냅샷에 대해 정의된 매개 변수 값을 사용해야 합니다. 스냅샷에 대해 정의된 매개 변수를 구독에서 재정의할 수 없습니다. 예를 들어 보고서 스냅샷으로 실행되는 서부 지역 판매 보고서를 구독하고 스냅샷에서 지역 매개 변수 값으로 **Western** 을 지정한다고 가정합니다. 이 보고서에 대한 구독을 만들 경우 구독의 매개 변수 값으로 **Western** 을 사용해야 합니다. 매개 변수 무시를 시각적으로 나타내기 위해 구독 페이지의 매개 변수 필드는 읽기 전용 필드로 설정됩니다.  
  
     보고서 실행 옵션이 매개 변수 처리 방법에 영향을 줄 수 있습니다. 보고서 스냅샷으로 실행되는 매개 변수가 있는 보고서는 보고서 스냅샷에 대해 정의된 매개 변수 값을 사용합니다. 매개 변수 값은 보고서의 매개 변수 속성 페이지에 정의됩니다. 스냅샷으로 실행되는 보고서는 쿼리에 매개 변수의 기본값이 포함되지 않는 한 쿼리에서 파생된 매개 변수를 사용할 수 없습니다.  
  
     구독을 정의한 후 보고서 스냅샷의 매개 변수 값을 변경하면 보고서 서버에서 구독이 비활성화됩니다. 구독을 비활성화하면 보고서가 수정된 것으로 표시됩니다. 구독을 활성화하려면 구독을 열어서 저장합니다.  
  
> [!NOTE]  
>  데이터 기반 구독은 구독자 데이터 원본에서 가져오는 매개 변수 값을 사용할 수 있습니다. 자세한 내용은 [구독자 데이터에 외부 데이터 원본 사용&#40;데이터 기반 구독&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)을 참조하세요.  
  
 자세한 내용은 [구독 및 배달&#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)을 참조하세요.  
  
##  <a name="parameters-and-securing-data"></a><a name="bkmk_Parameters_Security"></a> 매개 변수 및 데이터 보안  
 자격 증명이나 중요한 정보가 포함된 매개 변수가 있는 보고서를 배포할 때는 주의해야 합니다. 사용자가 보고서 매개 변수를 다른 값으로 쉽게 바꿀 수 있으므로 원치 않는 정보가 공개될 수 있기 때문입니다.  
  
 직원 또는 개인 데이터에 대해 매개 변수를 사용하는 대신 안전하게 사용자 컬렉션의 **UserID** 필드가 포함된 식을 기반으로 데이터를 선택할 수 있습니다. 사용자 컬렉션은 보고서를 실행하는 사용자의 ID를 가져온 다음 이 ID를 사용하여 사용자별 데이터를 검색하는 방법을 제공합니다.  
  
> [!IMPORTANT]  
>  **String** 형식의 매개 변수가 포함된 보고서에서는 유효한 값 목록이라고도 하는 사용 가능한 값 목록을 사용해야 하며 보고서를 실행하는 모든 사용자가 보고서의 데이터를 보는 데 필요한 권한만 갖도록 해야 합니다. **String** 유형의 매개 변수를 정의할 경우 모든 값을 사용할 수 있는 입력란이 사용자에게 제공됩니다. 사용 가능한 값 목록은 입력할 수 있는 값을 제한합니다. 보고서 매개 변수가 데이터 세트 매개 변수에 연결되어 있고 사용 가능한 값 목록을 사용하지 않는 경우에는 보고서 사용자가 입력란에 SQL 구문을 입력할 수 있으므로 보고서와 서버가 SQL 인젝션 공격을 받을 가능성이 있습니다. 사용자에게 새 SQL 문 실행을 위한 충분한 권한이 있으면 서버에 원하지 않은 결과가 발생할 수 있습니다.  
>   
>  보고서 매개 변수가 데이터 세트 매개 변수에 연결되어 있지 않고 매개 변수 값이 보고서에 포함된 경우에는 보고서 사용자가 식 구문 또는 URL을 매개 변수 값에 입력하고 보고서를 Excel 또는 HTML로 렌더링할 수 있습니다. 이후 다른 사용자가 보고서를 보면서 렌더링된 매개 변수 내용을 클릭할 경우 악의적인 스크립트나 링크가 실수로 실행될 수 있습니다.  
>   
>  악의적인 스크립트를 실수로 실행하는 위험을 줄이기 위해 신뢰할 수 있는 원본의 렌더링된 보고서만 여세요. 보고서를 안전하게 보호하는 방법에 대한 자세한 내용은 [보고서 및 리소스 보안](../../reporting-services/security/secure-reports-and-resources.md)을 참조하세요.  

##  <a name="related-sections"></a><a name="bkmk_Related_Topics"></a> 관련 단원  

 [자습서: 보고서에 매개 변수 추가&#40;보고서 작성기&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)  
  
[보고서 매개 변수 개념](../../reporting-services/report-design/report-parameters-concepts-report-builder-and-ssrs.md)  
  
 [보고서 예제(보고서 작성기 및 SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  
  
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)  
  
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
 [보안&#40;보고서 작성기&#41;](../../reporting-services/report-builder/security-report-builder.md)  
  
 [대화형 정렬, 문서 구조 및 링크&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)  
  
 [드릴스루, 드릴다운, 하위 보고서 및 중첩 데이터 영역&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)  
  
  
