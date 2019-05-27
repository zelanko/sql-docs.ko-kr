---
title: 식 추가(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a60ee091-b4ed-41e1-9b6a-032c316cd03f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 54505266a77c8baee7f39633ebccd0a5ab5708a8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106736"
---
# <a name="add-an-expression-report-builder-and-ssrs"></a>식 추가(보고서 작성기 및 SSRS)
  식은 보고서 항목 속성, 필터, 그룹, 정렬 순서, 연결 문자열 및 매개 변수 값을 정의하기 위해 보고서 전체에서 사용됩니다. 식은 등호(=)로 시작하며 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]으로 작성됩니다. 이러한 식은 보고서 처리기에 의해 런타임에 평가됩니다. 보고서 처리기는 평가 결과를 보고서 레이아웃 요소와 결합합니다.  
  
 식은 간단하거나 복잡할 수 있습니다. 간단한 식은 기본 제공 컬렉션의 단일 항목을 참조합니다. 복잡한 식에는 상수, 연산자, 전역 컬렉션 항목 및 함수 호출이 포함될 수 있습니다. 자세한 내용은 [식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-expression-to-a-text-box"></a>입력란에 식을 추가하려면  
  
-   **디자인** 뷰에서 식을 추가할 디자인 화면의 입력란을 클릭합니다.  
  
    -   간단한 식의 경우 식에 대한 표시 텍스트를 입력란에 입력합니다. 예를 들어 데이터 세트 필드 Sales의 경우 `[Sales]`를 입력합니다.  
  
    -   복잡한 식의 경우 입력란을 마우스 오른쪽 단추로 클릭하고 **식**을 선택합니다. **식** 대화 상자가 열립니다. 식 창에서 '=' 뒤에 식을 입력하거나 대화형으로 만든 다음 확인을 클릭합니다.  
  
         식이 디자인 화면에 `<<Expr>>`로 나타납니다.  
  
## <a name="see-also"></a>관련 항목  
 [텍스트 및 자리 표시자 서식 지정&#40;보고서 작성기 및 SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [입력란&#40;보고서 작성기 및 SSRS&#41;](text-boxes-report-builder-and-ssrs.md)   
 [보고서에 사용되는 식&#40;보고서 작성기 및 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [필터 수식 예&#40;보고서 작성기 및 SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)   
 [그룹 식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [식 대화 상자&#40;보고서 작성기&#41;](../expression-dialog-box-report-builder.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [보고서에 코드 추가&#40;SSRS&#41;](add-code-to-a-report-ssrs.md)  
  
  
