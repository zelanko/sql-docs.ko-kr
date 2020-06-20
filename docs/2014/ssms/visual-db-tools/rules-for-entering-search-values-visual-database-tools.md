---
title: 검색 값 입력 규칙(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- time [SQL Server], searches
- date searches
- dates [SQL Server], searches
- embedding apostrophes [SQL Server]
- logical value searches [SQL Server]
- case-sensitive search matches
- search criteria [SQL Server], rules
- text value searches [SQL Server]
- numeric value searches [SQL Server]
ms.assetid: 3c8134b7-83f4-41b4-99c8-e3949a685ff5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2263e2565137d50f318b8593e6ca9c16736c6cbe
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067133"
---
# <a name="rules-for-entering-search-values-visual-database-tools"></a>검색 값 입력 규칙(Visual Database Tools)
  이 항목에서는 다음과 같은 리터럴 형식 값을 검색 조건으로 입력할 때 적용되는 규칙을 설명합니다.  
  
-   텍스트 값  
  
-   숫자 값  
  
-   날짜  
  
-   논리 값  
  
> [!NOTE]  
>  이 항목의 정보는 표준 SQL-92 규칙에서 발췌한 것입니다. 그러나 데이터베이스마다 자체의 고유한 방식으로 SQL을 구현할 수 있으므로 여기에서 설명하는 지침이 모든 경우에 적용되는 것은 아닙니다. 특정 데이터베이스에 대하여 검색 값을 입력하는 방법에 대한 내용은 사용하고 있는 데이터베이스의 설명서를 참조하십시오.  
  
## <a name="searching-on-text-values"></a>텍스트 값 검색  
 다음 지침은 검색 조건에 텍스트 값을 입력할 때 적용됩니다.  
  
-   **인용 부호** 성에 대한 다음 예와 같이 텍스트 값을 작은따옴표로 묶습니다.  
  
    ```  
    'Smith'  
    ```  
  
     [조건 창](visual-database-tools.md)에 검색 조건을 입력할 때 텍스트 값을 입력하기만 하면 쿼리 및 뷰 디자이너가 자동으로 이 값을 작은따옴표로 묶습니다.  
  
    > [!NOTE]  
    >  일부 데이터베이스의 경우 작은따옴표 안의 용어는 리터럴 값으로 해석되지만 큰따옴표 안의 용어는 열 또는 테이블 참조 같은 데이터베이스 개체로 해석됩니다. 따라서 쿼리 및 뷰 디자이너에서 큰따옴표 안의 용어를 허용할 수 있다 하더라도 예상하는 것과 다르게 해석될 수 있습니다.  
  
-   **아포스트로피 포함** 검색하는 데이터에 작은따옴표(아포스트로피)가 포함되어 있으면 작은따옴표를 두 개 입력하여 작은따옴표가 구분 기호가 아니라 리터럴 값으로 해석되도록 나타낼 수 있습니다. 예를 들어, 다음 조건은 "Swann’s Way" 값을 검색합니다.  
  
    ```  
    ='Swann''s Way'  
    ```  
  
-   **길이 제한** 긴 문자열을 입력할 때 데이터베이스에 대한 SQL 문의 최대 길이를 초과하면 안 됩니다.  
  
-   **대/소문자 구분** 사용하고 있는 데이터베이스의 대/소문자 구분 규칙을 따릅니다. 사용하는 데이터베이스에 따라 텍스트를 검색할 때 대/소문자를 구분할 것인지 여부가 결정됩니다. 예를 들어 일부 데이터베이스는 "=" 연산자를 대/소문자가 정확하게 일치하는 항목으로 해석하지만 다른 데이터베이스는 대/소문자를 무시하고 일치하는 항목으로 해석합니다.  
  
     데이터베이스가 대/소문자를 구분하는 검색을 사용하는지 여부를 잘 모르겠는 경우에는 다음 예와 같이 검색 조건에 UPPER 함수 또는 LOWER 함수를 사용하여 검색 데이터의 대/소문자를 변환할 수 있습니다.  
  
    ```  
    WHERE UPPER(lname) = 'SMITH'  
    ```  
  
## <a name="searching-on-numeric-values"></a>숫자 값 검색  
 다음 지침은 검색 조건에 숫자 값을 입력할 때 적용됩니다.  
  
-   **인용 부호** 숫자는 인용 부호로 묶지 않습니다.  
  
-   **숫자가 아닌 문자** Windows 제어판의 **국가별 설정** 대화 상자에 정의된 소수 구분 기호와 음수 기호(-) 외에는 숫자가 아닌 문자를 포함할 수 없습니다. 자릿수 구분 기호(예: 천 단위 구분 쉼표) 또는 통화 기호를 넣지 마십시오.  
  
-   **소수점** 정수를 입력하는 경우 검색할 숫자의 입력 값이 정수 또는 실수인지에 따라 소수점을 사용할 수 있습니다.  
  
-   **지수 표기법** 매우 큰 수 또는 매우 작은 수를 다음 예에서와 같이 지수 표기법으로 입력할 수 있습니다.  
  
    ```  
    > 1.23456e-9  
    ```  
  
## <a name="searching-on-dates"></a>날짜 검색  
 날짜를 입력하는 형식은 사용하는 데이터베이스와 쿼리 및 뷰 디자이너에서 날짜가 입력되는 대상 창에 따라 다릅니다.  
  
> [!NOTE]  
>  데이터 원본에 사용되는 형식을 알지 못하는 경우에는 일반적으로 사용하는 임의의 형식으로 날짜를 조건 창의 필터 열에 입력합니다. 이렇게 입력한 항목은 대부분 적절한 형식으로 디자이너에서 자동 변환됩니다.  
  
 다음과 같은 날짜 형식을 쿼리 및 뷰 디자이너에서 사용할 수 있습니다.  
  
-   **로캘 관련** **Windows 국가별 설정 속성** 대화 상자에 지정된 날짜 형식  
  
-   **데이터베이스 관련** 해당 데이터베이스에서 인식하는 모든 형식  
  
-   **ANSI 표준 날짜** 다음 예와 같이 중괄호, 날짜를 나타내는 'd' 및 날짜 문자열을 사용하는 형식  
  
    ```  
    { d '1990-12-31' }  
    ```  
  
-   **ANSI 표준 datetime** ANSI 표준 날짜와 비슷하지만 1990년 12월 31일에 대한 다음 예와 같이 'd' 대신 'ts'를 사용하고 24시간제를 사용하여 시, 분, 초를 날짜에 추가합니다.  
  
    ```  
    { ts '1990-12-31 00:00:00' }  
    ```  
  
     일반적으로 ANSI 표준 날짜 형식은 실제 날짜 데이터 형식을 사용하여 날짜를 나타내는 데이터베이스에 사용됩니다. 이와 달리 datetime 형식은 datetime 데이터 형식을 지원하는 데이터베이스에 사용됩니다.  
  
 다음 표에는 쿼리 및 뷰 디자이너의 각 창에서 사용할 수 있는 날짜 형식이 요약되어 있습니다.  
  
|**창**|**날짜 형식**|  
|--------------|---------------------|  
|조건|로캘 관련 데이터베이스 관련 ANSI 표준<br /><br /> [조건 창](visual-database-tools.md) 에 입력한 날짜는 SQL 창에서 데이터베이스 호환 형식으로 변환됩니다.|  
|SQL|데이터베이스 관련 ANSI 표준|  
|결과|로캘 관련|  
  
## <a name="searching-on-logical-values"></a>논리 값 검색  
 논리 데이터의 형식은 데이터베이스마다 다릅니다. 대부분의 경우 False 값은 0으로 저장됩니다. True 값은 대개 1로 저장되지만 -1이 되는 경우도 있습니다. 다음 지침은 검색 조건에 논리 값을 입력할 때 적용됩니다.  
  
-   False 값을 검색하려면 다음 예와 같이 0을 사용하십시오.  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 0  
    ```  
  
-   True 값을 검색할 때 사용할 형식을 모르면 다음 예에서와 같이 1을 사용하여 시도해 보십시오.  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 1  
    ```  
  
-   또는 다음과 같이 0이 아닌 값을 검색하여 검색 범위를 넓힐 수 있습니다.  
  
    ```  
    SELECT * FROM authors  
    WHERE contract <> 0  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [검색 조건 지정&#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)  
  
  
