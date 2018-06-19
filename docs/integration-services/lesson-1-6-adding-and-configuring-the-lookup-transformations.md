---
title: '6단계: 조회 변환 추가 및 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
ms.assetid: 5c59f723-9707-4407-80ae-f05f483cf65f
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6735e372f7c1a4b49cdf57e73ee5cd82b2930bba
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35332737"
---
# <a name="lesson-1-6---adding-and-configuring-the-lookup-transformations"></a>1-6단원: 조회 변환 추가 및 구성
원본 파일에서 데이터를 추출하도록 플랫 파일 원본을 구성한 후에 다음 태스크에서는 **CurrencyKey** 및 **DateKey**값을 얻는 데 필요한 조회 변환을 정의합니다. 조회 변환에서는 지정한 입력 열의 데이터를 참조 데이터 집합의 열로 조인하여 조회를 수행합니다. 참조 데이터 집합은 기존 테이블, 기존 뷰, 새 테이블 또는 SQL 문의 결과일 수 있습니다. 이 자습서에서 조회 변환은 OLE DB 연결 관리자를 사용하여 참조 데이터 집합의 원본인 데이터가 포함된 데이터베이스에 연결합니다.  
  
> [!NOTE]  
> 또한 참조 데이터 집합이 포함된 캐시에 연결되도록 조회 변환을 구성할 수도 있습니다. 자세한 내용은 [Lookup Transformation](../integration-services/data-flow/transformations/lookup-transformation.md)을(를) 참조하세요.  
  
이 자습서에서는 다음과 같은 두 가지 조회 변환 구성 요소를 패키지에 추가하고 구성하는 과정을 다룹니다.  
  
-   플랫 파일의 일치하는 **CurrencyID** 열 값에 따라 **DimCurrency** 차원 테이블의 **CurrencyKey** 열에서 값을 조회하는 하나의 변환  
  
-   플랫 파일의 일치하는 **CurrencyDate** 열 값에 따라 **DimDate** 차원 테이블의 **DateKey** 열에서 값을 조회하는 하나의 변환  
  
두 경우 모두 조회 변환에는 이전에 작성한 OLE DB 연결 관리자를 사용합니다.  
  
### <a name="to-add-and-configure-the-lookup-currency-key-transformation"></a>Lookup Currency Key 변환을 추가하고 구성하려면  
  
1.  **SSIS 도구 상자**에서 **일반**을 확장한 다음 **조회** 를 **데이터 흐름** 탭의 디자인 화면으로 끌어다 놓습니다. 조회를 **Extract Sample Currency Data** 원본 바로 아래에 배치합니다.  
  
2.  **Extract Sample Currency Data** 플랫 파일 원본을 클릭하고 녹색 화살표를 새로 추가한 **조회** 변환으로 끌어다 놓아서 두 구성 요소를 연결합니다.  
  
3.  **데이터 흐름** 디자인 화면에서 **조회** 변환의 **조회** 를 클릭하고 이름을 **Lookup Currency Key**로 바꿉니다.  
  
4.  **Lookup CurrencyKey** 변환을 두 번 클릭하여 조회 변환 편집기를 표시합니다.  
  
5.  **일반** 페이지에서 다음을 선택합니다.  
  
    1.  **전체 캐시**를 선택합니다.  
  
    2.  **연결 유형** 영역에서 **OLE DB 연결 관리자**를 선택합니다.  
  
6.  **연결** 페이지에서 다음을 선택합니다.  
  
    1.  **OLE DB 연결 관리자** 상자에 **localhost.AdventureWorksDW2012** 가 표시되어 있는지 확인합니다.  
  
    2.  **SQL 쿼리 결과 사용**을 선택하고 다음 SQL 문을 입력하거나 복사합니다.  
  
        ```sql
        SELECT * FROM [dbo].[DimCurrency]
        WHERE [CurrencyAlternateKey]
        IN ('ARS', 'AUD', 'BRL', 'CAD', 'CNY',
            'DEM', 'EUR', 'FRF', 'GBP', 'JPY',
            'MXN', 'SAR', 'USD', 'VEB')
        ```  
  
7.  **열** 페이지에서 다음을 선택합니다.  
  
    1.  **사용 가능한 입력 열** 패널에서 **CurrencyID** 를 **사용 가능한 조회 열** 패널로 끌어다 **CurrencyAlternateKey**에 놓습니다.  
  
    2.  **사용 가능한 조회 열** 목록에서 **CurrencyKey**왼쪽에 있는 확인란을 선택합니다.  
  
8.  **확인** 을 클릭하여 **데이터 흐름** 디자인 화면으로 돌아갑니다.  
  
9. Lookup Currency Key 변환을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
10. 속성 창에서 **LocaleID** 속성이 **영어(미국)** 로 설정되어 있고 **DefaultCodePage** 속성이 **1252**로 설정되어 있는지 확인합니다.  
  
### <a name="to-add-and-configure-the--lookup-datekey-transformation"></a>Lookup DateKey 변환을 추가하고 구성하려면  
  
1.  **SSIS 도구 상자**에서 **조회** 를 **데이터 흐름** 디자인 화면으로 끌어다 놓습니다. 조회를 **Lookup Currency Key** 변환 바로 아래에 배치합니다.  
  
2.  **Lookup Currency Key** 변환을 클릭하고 녹색 화살표를 새로 추가한 **조회** 변환으로 끌어다 놓아서 두 구성 요소를 연결합니다.  
  
3.  **입/출력 선택** 대화 상자에서 **출력** 목록 상자의 **조회 일치 항목 출력** 을 클릭한 다음 **확인**을 클릭합니다.  
  
4.  **데이터 흐름** 디자인 화면에서 새로 추가한 **Lookup** 변환의 **조회** 를 클릭하고 이름을 **Lookup Date Key**로 바꿉니다.  
  
5.  **Lookup Date Key** 변환을 두 번 클릭합니다.  
  
6.  **일반** 페이지에서 **부분 캐시**를 선택합니다.  
  
7.  **연결** 페이지에서 다음을 선택합니다.  
  
    1.  **OLEDB 연결 관리자** 대화 상자에서 **localhost.AdventureWorksDW2012** 가 표시되어 있는지 확인합니다.  
  
    2.  **테이블 또는 뷰 사용** 상자에서 **[dbo].[DimDate]** 를 입력하거나 선택합니다.  
  
8.  **열** 페이지에서 다음을 선택합니다.  
  
    1.  **사용 가능한 입력 열** 패널에서 **CurrencyDate** 를 **사용 가능한 조회 열** 패널로 끌어다 **FullDateAlternateKey**에 놓습니다.  
  
    2.  **사용 가능한 조회 열** 목록에서 **DateKey**왼쪽에 있는 확인란을 선택합니다.  
  
9. **고급** 페이지에서 캐싱 옵션을 검토합니다.  
  
10. **확인** 을 클릭하여 **데이터 흐름** 디자인 화면으로 돌아갑니다.  
  
11. Lookup Date Key 변환을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
12. 속성 창에서 **LocaleID** 속성이 **영어(미국)** 로 설정되어 있고 **DefaultCodePage** 속성이 **1252**로 설정되어 있는지 확인합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[7단계: OLE DB 대상 추가 및 구성](../integration-services/lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
## <a name="see-also"></a>참고 항목  
[Lookup Transformation](../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
  
