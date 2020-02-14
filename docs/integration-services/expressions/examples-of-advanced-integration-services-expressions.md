---
title: 고급 Integration Services 식의 예 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- functions [Integration Services]
- operators [Integration Services]
- expressions [Integration Services], examples
- examples [Integration Services]
ms.assetid: c7794ba3-0de5-466b-ae8a-9ddd27360049
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f5643e4e1d900b0c4152a422927a29302f40f952
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297625"
---
# <a name="examples-of-advanced-integration-services-expressions"></a>고급 Integration Services 식의 예

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  이 섹션에서는 여러 개의 연산자와 함수가 결합된 고급 식의 예를 제공합니다. 선행 제약 조건이나 조건부 분할 변환에 사용된 식은 부울로 계산되어야 합니다. 그러나 속성 식, 변수, 파생 열 변환 또는 For 루프 컨테이너에 사용된 식에는 이 제한이 적용되지 않습니다.  
  
 다음 예에서는 **AdventureWorks** 및 [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 사용합니다. 각 예에서 사용되는 테이블이 식별됩니다.  
  
## <a name="boolean-expressions"></a>부울 식  
  
-   이 예에서는 **Product** 테이블을 사용합니다. 이 식은 **SellStartDate** 열의 월 부분을 계산하고 월이 6월 이후이면 TRUE를 반환합니다.  
  
    ```  
    DATEPART("mm",SellStartDate) > 6  
    ```  
  
-   이 예에서는 **Product** 테이블을 사용합니다. 이 식은 **ListPrice** 열을 **StandardCost** 열로 나눈 값을 반올림한 결과를 계산하고 결과가 1.5보다 크면 TRUE를 반환합니다.  
  
    ```  
    ROUND(ListPrice / StandardCost,2) > 1.50  
    ```  
  
-   이 예에서는 **Product** 테이블을 사용합니다. 이 식은 3개 연산이 모두 TRUE이면 TRUE를 반환합니다. **Size** 열과 **BikeSize** 변수의 데이터 형식이 호환되지 않으면 두 번째 예에 표시된 것처럼 식에 명시적 캐스트가 필요합니다. DT_WSTR로의 캐스트는 문자열 길이를 포함합니다.  
  
    ```  
    MakeFlag ==  TRUE && FinishedGoodsFlag == TRUE && Size != @BikeSize  
    MakeFlag ==  TRUE && FinishedGoodsFlag == TRUE  && Size != (DT_WSTR,10)@BikeSize  
    ```  
  
-   이 예에서는 **CurrencyRate** 테이블을 사용합니다. 이 식은 테이블과 변수의 값을 비교합니다. **FromCurrencyCode** 또는 **ToCurrencyCode** 열의 항목이 변수 값과 같고 **AverageRate** 값이 **EndOfDayRate**값보다 크면 TRUE가 반환됩니다.  
  
    ```  
    (FromCurrencyCode == @FromCur || ToCurrencyCode == @ToCur) && AverageRate > EndOfDayRate  
    ```  
  
-   이 예에서는 **Currency** 테이블을 사용합니다. 이 식은 **Name** 열이 a 또는 A가 아니면 TRUE를 반환합니다.  
  
    ```  
    SUBSTRING(UPPER(Name),1,1) != "A"  
    ```  
  
     다음 식은 동일한 결과를 제공하지만 한 문자만 대문자로 변환되기 때문에 훨씬 효율적입니다.  
  
    ```  
    UPPER(SUBSTRING(Name,1,1)) != "A"  
    ```  
  
## <a name="non-boolean-expressions"></a>부울이 아닌 식  
 부울이 아닌 식은 파생 열 변환, 속성 식 및 For 루프 컨테이너에 사용됩니다.  
  
-   이 예에서는 **Contact** 테이블을 사용합니다. 이 식은 **FirstName**, **MiddleName**및 **LastName** 열에서 선행 및 후행 공백을 제거합니다. **MiddleName** 열이 Null이 아니면 첫 문자를 추출하여 중간 이니셜과 **FirstName** 및 **LastName**열의 값을 연결하고 값 사이에 공백을 삽입합니다.  
  
    ```  
    TRIM(FirstName) + " " + (!ISNULL(MiddleName) ? SUBSTRING(MiddleName,1,1) + " " : "") + TRIM(LastName)  
    ```  
  
-   이 예에서는 **Contact** 테이블을 사용합니다. 이 식은 **Salutation** 열의 항목 유효성을 검사하고 **Salutation** 항목이나 빈 문자열을 반환합니다.  
  
    ```  
    (Salutation == "Sr." || Salutation == "Ms." || Salutation == "Sra." || Salutation == "Mr.") ? Salutation : ""  
    ```  
  
-   이 예에서는 **Product** 테이블을 사용합니다. 이 식은 **Color** 열의 첫 문자를 대문자로 변환하고 나머지 문자를 소문자로 변환합니다.  
  
    ```  
    UPPER(SUBSTRING(Color,1,1)) + LOWER(SUBSTRING(Color,2,15))  
    ```  
  
-   이 예에서는 **Product** 테이블을 사용합니다. 이 식은 제품이 판매된 월 수를 계산하며 **SellStartDate** 또는 **SellEndDate** 열에 NULL이 포함된 경우 "알 수 없음" 문자열을 반환합니다.  
  
    ```  
    !(ISNULL(SellStartDate)) && !(ISNULL(SellEndDate)) ? (DT_WSTR,2)DATEDIFF("mm",SellStartDate,SellEndDate) : "Unknown"  
    ```  
  
-   이 예에서는 **Product** 테이블을 사용합니다. 이 식은 **StandardCost** 열의 표시를 계산하고 결과를 전체 두 자릿수로 반올림합니다. 결과는 백분율로 표시됩니다.  
  
    ```  
    ROUND(ListPrice / StandardCost,2) * 100  
    ```  
  
## <a name="related-tasks"></a>관련 작업  
 [데이터 흐름 구성 요소에서 식 사용](https://msdn.microsoft.com/library/9181b998-d24a-41fb-bb3c-14eee34f910d)  
  
## <a name="related-content"></a>관련 내용  
 pragmaticworks.com의 기술 문서 - [SSIS 식 치트 시트](https://go.microsoft.com/fwlink/?LinkId=746575)  
  
  
