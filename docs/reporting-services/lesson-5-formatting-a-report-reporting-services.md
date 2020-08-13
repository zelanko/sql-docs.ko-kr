---
title: '5단원: 보고서 서식 지정(Reporting Services) | Microsoft Docs'
description: Sales Orders 보고서에 데이터 영역과 일부 필드를 추가한 후 날짜 및 통화 필드와 열 머리글의 서식을 지정하는 방법을 알아봅니다.
ms.date: 04/29/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ae46efa9-6e04-48ec-afb4-5a2314dcb05a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ef2d3fd220aef7a593a2244cf2d7509c5264fcca
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245112"
---
# <a name="lesson-5-formatting-a-report-reporting-services"></a>5단원: 보고서 서식 지정(Reporting Services)

이제 Sales Orders 보고서에 데이터 영역과 일부 필드를 추가했으므로 날짜 및 통화 필드와 열 머리글의 서식을 지정할 수 있습니다.

## <a name="format-the-date"></a><a name="bkmk_format_date"></a>날짜 서식 지정

Date 필드 식은 기본적으로 날짜 및 시간 정보를 표시합니다. 날짜만 표시되도록 서식을 지정할 수 있습니다.

1. **디자인** 탭을 선택합니다.
2. `[Date]` 필드 식이 포함된 셀을 마우스 오른쪽 단추로 클릭하고 **텍스트 상자 속성**을 선택합니다.
3. **숫자**를 클릭한 다음, **범주** 필드에서 **날짜**를 선택합니다.
4. **형식** 상자에서 **January 31, 2000**을 선택합니다.
5. **확인**을 선택하여 서식을 적용합니다.
6. 보고서를 미리 보기하여 `[Date]` 필드의 서식 변경 내용을 확인하고 디자인 뷰로 돌아갑니다.

## <a name="format-the-currency"></a><a name="bkmk_format_currency"></a>통화 서식 지정

LineTotal 필드 식은 일반 숫자를 표시합니다. 숫자에 서식을 지정하여 통화로 표시할 수 있습니다.

1. `[LineTotal]` 식이 포함된 셀을 마우스 오른쪽 단추로 클릭하고 **텍스트 상자 속성**을 선택합니다.
2. 맨 왼쪽 열 목록 상자에서 **숫자**를 선택하고 **범주** 목록 상자에서 **통화**를 선택합니다.
3. 국가별 설정이 영어(미국)인 경우 **형식** 목록 상자의 기본값은 다음과 같아야 합니다.
    - **소수 자릿수: 2**
    - **음수: ($12345.00)**
    - **기호: $ 영어(미국)**
4. **천 단위 구분 기호(,) 사용**을 선택합니다. 샘플 텍스트가 **$12,345.00**으로 표시되면 설정이 올바른 것입니다.
5. **확인**을 선택하여 서식을 적용합니다.
6. 보고서를 미리 보기하여 `[LineTotal]` 식 열의 변경 내용을 확인하고 디자인 뷰로 돌아갑니다.  

## <a name="change-text-style-and-column-widths"></a><a name="bkmk_change_textstyle"></a>텍스트 스타일 및 열 너비 변경

머리글 행을 강조 표시하고 데이터 열의 너비를 조정하여 보고서에 다른 서식 지정을 추가할 수 있습니다.

### <a name="to-format-header-rows-and-table-columns"></a>머리글 행 및 테이블 너비의 서식을 지정하려면

1. 테이블을 선택하여 열 핸들과 행 핸들이 테이블 위와 옆에 표시되도록 합니다. 테이블 위쪽 및 옆쪽을 따라 표시되는 회색 막대는 행 및 열 핸들입니다.

2. 열 핸들 사이의 선에 커서를 두면 커서가 양방향 화살표로 바뀝니다. 이 상태에서 열을 끌어 크기를 원하는 대로 조정합니다.
    ![rs_BasicTableDetailsDesign](media/rs-basictabledetailsdesign.png)

3. 열 머리글 레이블이 있는 행을 선택하고 **서식** 메뉴에서 **글꼴** > **굵게**를 선택합니다.

4. 보고서를 미리 봅니다. 아래와 같이 표시됩니다.

    ![열 머리글이 굵게 설정된 테이블의 미리 보기](media/rs-basictabledetailsformattedpreview.png "열 머리글이 굵게 설정된 테이블의 미리 보기")  

5. **파일** 메뉴에서 **모두 저장**을 선택하여 보고서를 저장합니다.

## <a name="next-steps"></a>다음 단계

이 단원에서는 열 머리글과 필드 식에 성공적으로 서식을 지정했습니다. 다음으로, 보고서에 그룹화 및 합계를 추가해 보겠습니다. 다음으로 [6단원: 그룹화 및 합계 추가&#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

[숫자 및 날짜 서식 지정 &#40;보고서 작성기 및 SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)
[렌더링 동작 &#40;보고서 작성기 및 SSRS&#41;](report-design/rendering-behaviors-report-builder-and-ssrs.md)
