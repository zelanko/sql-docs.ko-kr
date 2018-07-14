---
title: 보고서에 사용되는 식(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- expressions [Reporting Services], about expressions
ms.assetid: 76b9ed31-5aec-40fc-bb88-a1c1b0ab3fc3
caps.latest.revision: 57
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ecdadef4e49f3630c78fc33c1c6f490deda26b5f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37274749"
---
# <a name="expression-uses-in-reports-report-builder-and-ssrs"></a>보고서에 사용되는 식(보고서 작성기 및 SSRS)
  매개 변수, 쿼리, 필터, 보고서 항목 속성, 그룹 및 정렬 정의, 입력란 속성, 책갈피, 문서 구조, 동적 페이지 머리글 및 바닥글 내용, 이미지, 동적 데이터 원본 정의에 대한 값을 지정하거나 계산하기 위해 보고서 정의 전체에서 식이 사용됩니다. 이 항목에서는 식을 사용하여 보고서의 내용 또는 모양을 수정할 수 있는 많은 경우에 대한 예를 제공합니다. 이 목록에는 일부만 나와 있습니다. 식 단추(**fx**)를 표시하는 대화 상자 또는 **\<Expression...>** 을 표시하는 드롭다운 목록에서 속성 식을 설정할 수 있습니다.  
  
 식은 간단하거나 복잡할 수 있습니다. *단순 식* 에는 단일 데이터 집합 필드, 매개 변수 또는 기본 제공 필드에 대한 참조가 포함됩니다. 복잡한 식에는 여러 개의 기본 제공 참조, 연산자 및 함수 호출이 포함될 수 있습니다. 예를 들어 복잡한 식에는 Sales 필드에 적용되는 Sum 함수가 포함될 수 있습니다.  
  
 식은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]에서 작성됩니다. 식은 등호(=)로 시작하고 뒤에 데이터 집합 필드 및 매개 변수, 상수, 함수 및 연산자와 같은 기본 제공 컬렉션에 대한 참조의 조합이 표시됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Simple"></a> 단순 식 사용  
 단순 식은 대괄호로 묶여 디자인 화면 및 대화 상자에 나타납니다. 예를 들어 데이터 집합 필드가 `[ProductID]`로 나타납니다. 데이터 집합의 필드를 입력란으로 끌어 놓으면 단순 식이 자동으로 생성됩니다. 자리 표시자가 생성되고 식에서 기본 값을 정의합니다. 또한 디자인 화면 또는 대화 상자 모두에서 데이터 영역 셀 또는 입력란에 식을 직접 입력할 수 있습니다(예: `[ProductID]`).  
  
 다음 표에서는 단순 식을 사용하는 방법의 예가 나열됩니다. 표에서는 기능, 설정할 속성, 속성을 설정하는 데 일반적으로 사용하는 대화 상자, 속성 값에 대해 설명합니다. 모든 식과 마찬가지로 디자인 화면, 대화 상자 또는 속성 창에 단순 식을 직접 입력하거나 식 대화 상자에서 단순 식을 편집할 수 있습니다.  
  
|기능|속성, 컨텍스트 및 대화 상자|속성 값|  
|-------------------|---------------------------------------|--------------------|  
|입력란에 표시할 데이터 집합 필드를 지정합니다.|입력란 내의 자리 표시자에 대한 Value 속성입니다. **자리 표시자 속성 대화 상자, 일반**을 사용합니다.|`[Sales]`|  
|그룹에 대한 값을 집계합니다.|테이블릭스 그룹과 연결된 행 내의 자리 표시자에 대한 Value 속성입니다. **입력란 속성 대화 상자**를 사용합니다.|`[Sum(Sales)]`|  
|페이지 번호를 포함합니다.|페이지 머리글에 위치한 입력란 내의 자리 표시자에 대한 Value 속성입니다. **입력란 속성 대화 상자, 일반**을 사용합니다.|`[&PageNumber]`|  
|선택한 매개 변수 값을 표시합니다.|디자인 화면의 입력란 내에 있는 자리 표시자에 대한 Value 속성입니다. **입력란 속성 대화 상자, 일반**을 사용합니다.|`[@SalesThreshold]`|  
|데이터 영역에 대한 그룹 정의를 지정합니다.|테이블릭스 그룹의 그룹 식입니다. **테이블릭스 그룹 속성 대화 상자, 일반**을 사용합니다.|`[Category]`|  
|테이블에서 특정 필드 값을 제외합니다.|테이블릭스의 필터 수식입니다. **테이블릭스 속성 대화 상자, 필터**를 사용합니다.|데이터 형식에 대해 **정수**를 선택합니다.<br /><br /> `[Quantity]`<br /><br /> `>`<br /><br /> `100`|  
|그룹 필터에 대한 특정 값만 포함합니다.|테이블릭스 그룹의 필터 수식입니다. **테이블릭스 그룹 속성 대화 상자, 필터**를 사용합니다.|`[Category]`<br /><br /> `=`<br /><br /> `Clothing`|  
|데이터 집합에서 두 개 이상의 필드에 대한 특정 값을 제외합니다.|테이블릭스의 그룹에 대한 필터 수식입니다. **테이블릭스 속성 대화 상자, 필터**를 사용합니다.|`=[Color]`<br /><br /> `<>`<br /><br /> `Red`<br /><br /> `=[Color]`<br /><br /> `<>`<br /><br /> `Blue`|  
|테이블의 기존 필드를 기반으로 정렬 순서를 지정합니다.|테이블릭스의 정렬 식입니다. **테이블릭스 속성 대화 상자, 정렬**을 사용합니다.|`[SizeSortOrder]`|  
|쿼리 매개 변수를 보고서 매개 변수에 연결합니다.|데이터 집합의 매개 변수 컬렉션입니다. **데이터 집합 속성 대화 상자, 매개 변수**를 사용합니다.|`[@Category]`<br /><br /> `[@Category]`|  
|주 보고서의 매개 변수를 하위 보고서로 전달합니다.|하위 보고서의 매개 변수 컬렉션입니다. **하위 보고서 속성 대화 상자, 매개 변수**를 사용합니다.|`[@Category]`<br /><br /> `[@Category]`|  
  
 
  
##  <a name="Complex"></a> 복잡한 식 사용  
 복잡한 식은 여러 개의 기본 제공 참조, 연산자 및 함수 호출을 포함하고 디자인 화면에 `<<Expr>>`로 나타날 수 있습니다. 식 텍스트를 보거나 변경하려면 **식** 대화 상자를 열거나 속성 창에 직접 입력해야 합니다. 다음 표에서는 복잡한 식을 사용하여 설정할 속성, 속성을 설정하는 데 일반적으로 사용하는 대화 상자, 속성 값을 비롯하여 데이터를 표시 또는 구성하거나 보고서 모양을 변경하는 일반적인 방법을 나열합니다. 식을 대화 상자, 디자인 화면 또는 속성 창에 직접 입력할 수 있습니다.  
  
|기능|속성, 컨텍스트 및 대화 상자|속성 값|  
|-------------------|---------------------------------------|--------------------|  
|데이터 집합의 집계 값을 계산합니다.|입력란 내의 자리 표시자에 대한 Value 속성입니다. **자리 표시자 속성 대화 상자, 일반**을 사용합니다.|`=First(Fields!Sales.Value,"DataSet1")`|  
|동일한 입력란에서 텍스트와 식을 연결합니다.|페이지 머리글 또는 페이지 바닥글에 위치한 입력란 내의 자리 표시자에 대한 Value입니다. **자리 표시자 속성 대화 상자, 일반**을 사용합니다.|`="This report began processing at " & Globals!ExecutionTime`|  
|다른 범위의 데이터 집합에 대한 집계 값을 계산합니다.|테이블릭스 그룹에 위치한 입력란 내의 자리 표시자에 대한 Value입니다. **자리 표시자 속성 대화 상자, 일반**을 사용합니다.|`=Max(Fields!Total.Value,"DataSet2)`|  
|값에 따라 입력란에 있는 데이터의 서식을 지정합니다.|테이블릭스의 정보 행에서 입력란 내에 있는 자리 표시자에 대한 Color입니다. **입력란 속성 대화 상자, 글꼴**을 사용합니다.|`=IIF(Fields!TotalDue.Value < 10000,"Red","Black")`|  
|보고서 전체에서 참조할 값을 한 번 계산합니다.|보고서 변수에 대한 Value입니다. **보고서 속성 대화 상자, 변수**를 사용합니다.|`=Variables!MyCalculation.Value`|  
|데이터 집합에서 두 개 이상의 필드에 대한 특정 값을 포함합니다.|테이블릭스의 그룹에 대한 필터 수식입니다. **테이블릭스 속성 대화 상자, 필터**를 사용합니다.|데이터 형식에 대해 **부울**을 선택합니다.<br /><br /> `=IIF(InStr(Fields!Subcat.Value,"Shorts")=0 AND (Fields!Size.Value="M" OR Fields!Size.Value="S"),TRUE, FALSE)`<br /><br /> `=`<br /><br /> `TRUE`|  
|*Show*라는 부울 매개 변수를 사용하여 사용자가 전환할 수 있는 디자인 화면의 입력란을 숨깁니다.|입력란의 Hidden 속성입니다. **입력란 속성 대화 상자, 표시 유형**을 사용합니다.|`=Not Parameters!` *Show\<부울 매개 변수>* `.Value`|  
|동적 페이지 머리글 또는 바닥글 내용을 지정합니다.|페이지 머리글 또는 페이지 바닥글에 위치한 입력란 내의 자리 표시자에 대한 Value입니다.|`="Page " & Globals!PageNumber & " of "  & Globals!TotalPages`|  
|매개 변수를 사용하여 동적으로 데이터 원본을 지정합니다.|데이터 원본에 대한 연결 문자열입니다. **데이터 원본 속성 대화 상자, 일반**을 사용합니다.|`="Data Source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks2012"`|  
|사용자가 선택한 다중값 매개 변수의 모든 값을 식별합니다.|입력란 내의 자리 표시자에 대한 Value입니다. **테이블릭스 속성 대화 상자, 필터**를 사용합니다.|`=Join(Parameters!MyMultivalueParameter.Value,", ")`|  
|다른 그룹 없이 테이블릭스의 각 20개의 행에 대한 페이지 나누기를 지정합니다.|테이블릭스의 그룹에 대한 그룹 식입니다. **그룹 속성 대화 상자, 페이지 나누기**를 사용합니다. **각 그룹 인스턴스 사이**옵션을 선택합니다.|`=Ceiling(RowNumber(Nothing)/20)`|  
|매개 변수를 기반으로 조건부 표시 유형을 지정합니다.|테이블릭스에 대한 Hidden 속성입니다. **테이블릭스 속성 대화 상자, 표시 유형**을 사용합니다.|`=Not Parameters!<` *부울 매개 변수* `>.Value`|  
|특정 culture에 대해 서식이 지정된 날짜를 지정합니다.|데이터 영역의 입력란 내에 있는 자리 표시자에 대한 Value입니다. **입력란 속성 대화 상자, 일반**을 사용합니다.|`=Fields!OrderDate.Value.ToString(System.Globalization.CultureInfo.CreateSpecificCulture("de-DE"))`|  
|문자열과 두 소수 자릿수의 백분율로 서식이 지정된 숫자를 연결합니다.|데이터 영역의 입력란 내에 있는 자리 표시자에 대한 Value입니다. **입력란 속성 대화 상자, 일반**을 사용합니다.|`="Growth Percent: " & Format(Fields!Growth.Value,"p2")`|  
  
 
  
## <a name="see-also"></a>관련 항목  
 [식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](report-parameters-report-builder-and-report-designer.md)   
 [필터 수식 예 &#40;보고서 작성기 및 SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [페이지 머리글 및 바닥글 &#40;보고서 작성기 및 SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)   
 [텍스트 및 자리 표시자 서식 지정 &#40;보고서 작성기 및 SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [항목 숨기기&#40;보고서 작성기 및 SSRS&#41;](../report-builder/hide-an-item-report-builder-and-ssrs.md)  
  
  
