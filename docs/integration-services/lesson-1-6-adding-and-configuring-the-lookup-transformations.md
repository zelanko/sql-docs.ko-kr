---
title: '6단계: 조회 변환 추가 및 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 03/19/2019
ms.prod: sql
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5c59f723-9707-4407-80ae-f05f483cf65f
author: chugugrace
ms.author: chugu
ms.reviewer: ''
ms.openlocfilehash: ac10ace82a38110d2038f95c3514aa8271d5b88c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71283742"
---
# <a name="lesson-1-6-add-and-configure-the-lookup-transformations"></a>1-6단원: 조회 변환 추가 및 구성

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



원본 파일에서 데이터를 추출하도록 플랫 파일 원본을 구성한 후에는 **CurrencyKey** 및 **DateKey**에 대한 값을 얻는 데 필요한 조회 변환을 정의합니다. 조회 변환에서는 지정한 입력 열의 데이터를 참조 데이터 세트의 열로 조인하여 조회를 수행합니다. 참조 데이터 세트는 기존 테이블, 기존 뷰, 새 테이블 또는 SQL 문의 결과일 수 있습니다. 이 자습서에서 조회 변환은 OLE DB 연결 관리자를 사용하여 참조 데이터 세트의 원본 데이터가 포함된 데이터베이스에 연결합니다.  
  
> [!NOTE]  
> 또한 참조 데이터 세트가 포함된 캐시에 연결되도록 조회 변환을 구성할 수도 있습니다. 자세한 내용은 [조회 변환](../integration-services/data-flow/transformations/lookup-transformation.md)을 참조하세요.  
  
이 태스크에서는 다음과 같은 두 가지 조회 변환 구성 요소를 패키지에 추가하고 구성합니다.  
  
-   플랫 파일의 일치하는 **CurrencyID** 열 값에 따라 **DimCurrency** 차원 테이블의 **CurrencyKey** 열에서 값 조회를 수행하는 하나의 변환입니다.  
  
-   플랫 파일의 일치하는 **CurrencyDate** 열 값에 따라 **DimDate** 차원 테이블의 **DateKey** 열에서 값 조회를 수행하는 하나의 변환입니다.  
  
두 경우 모두 조회 변환에는 이전에 작성한 OLE DB 연결 관리자를 사용합니다.  
  
## <a name="add-and-configure-the-lookup-currency-key-transformation"></a>Lookup Currency Key 변환 추가 및 구성  
  
1.  **SSIS 도구 상자**에서 **일반**을 확장한 다음 **조회** 를 **데이터 흐름** 탭의 디자인 화면으로 끌어다 놓습니다. **조회**를 **Extract Sample Currency Data** 원본 바로 아래에 배치합니다.  
  
2.  **Extract Sample Currency Data** 플랫 파일 원본을 선택하고 파란색 화살표를 새로 추가한 **조회** 변환으로 끌어다 놓아서 두 구성 요소를 연결합니다.  
  
3.  **데이터 흐름** 디자인 화면에서 **조회** 변환의 **조회** 를 선택하고 이름을 **Lookup Currency Key**로 바꿉니다.  
  
4.  **Lookup Currency Key** 변환을 두 번 클릭하여 **조회 변환 편집기**를 표시합니다.  
  
5.  **일반** 페이지에서 다음을 선택합니다.  
  
    1.  **전체 캐시**를 선택합니다.  
  
    2.  **연결 형식** 영역에서 **OLE DB 연결 관리자**를 선택합니다.  
  
6.  **연결** 페이지에서 다음을 선택합니다.  
  
    1.  **OLE DB 연결 관리자** 상자에 **localhost.AdventureWorksDW2012** 가 표시되어 있는지 확인합니다.  
  
    2.  **SQL 쿼리 결과 사용**을 선택한 후, 다음 SQL 문을 입력하거나 붙여넣습니다.  
  
        ```sql
        SELECT * FROM [dbo].[DimCurrency]
        WHERE [CurrencyAlternateKey]
        IN ('ARS', 'AUD', 'BRL', 'CAD', 'CNY',
            'DEM', 'EUR', 'FRF', 'GBP', 'JPY',
            'MXN', 'SAR', 'USD', 'VEB')
        ```  
    3.  **미리 보기**를 선택하여 쿼리 결과를 확인합니다.
  
7.  **열** 페이지에서 다음을 선택합니다.  
  
    1.  **사용 가능한 입력 열** 패널에서 **CurrencyID** 를 **사용 가능한 조회 열** 패널로 끌어다 **CurrencyAlternateKey**에 놓습니다.  
  
    2.  **사용 가능한 조회 열** 목록에서 **CurrencyKey**왼쪽에 있는 확인란을 선택합니다.  
  
8.  **확인**을 선택하여 **데이터 흐름** 디자인 화면으로 돌아갑니다.  
  
9. Lookup Currency Key 변환을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
10. **속성** 창에서 **LocaleID** 속성이 **영어(미국)** 이고 **DefaultCodePage** 속성이 **1252**인지 확인합니다.  
  
## <a name="add-and-configure-the-lookup-date-key-transformation"></a>Lookup Date Key 변환 추가 및 구성  
  
1.  **SSIS 도구 상자**에서 **조회** 를 **데이터 흐름** 디자인 화면으로 끌어다 놓습니다. 이 **조회**를 **Lookup Currency Key** 변환 바로 아래에 배치합니다.  
  
2.  **Lookup Currency Key** 변환을 선택하고 파란색 화살표를 새 **조회** 변환으로 끌어다 놓아서 두 구성 요소를 연결합니다.  
  
3.  **입/출력 선택** 대화 상자에서 **출력** 목록 상자의 **조회 일치 항목 출력**을 선택한 다음, **확인**을 선택합니다.  
  
4.  **데이터 흐름** 디자인 화면에서 새로 추가한 **Lookup** 변환의 **조회**를 선택하고 해당 이름을 **Lookup Date Key**로 바꿉니다.  
  
5.  **Lookup Date Key** 변환을 두 번 클릭합니다.  
  
6.  **일반** 페이지에서 **부분 캐시**를 선택합니다.  
  
7.  **연결** 페이지에서 다음을 선택합니다.  
  
    1.  **OLEDB 연결 관리자** 대화 상자에서 **localhost.AdventureWorksDW2012**가 표시되어 있는지 확인합니다.  
  
    2.  **테이블 또는 뷰 사용** 상자에서 **[dbo].[DimDate]** 를 입력하거나 선택합니다.  
  
8.  **열** 페이지에서 다음을 선택합니다.  
  
    1.  **사용 가능한 입력 열** 패널에서 **CurrencyDate** 를 **사용 가능한 조회 열** 패널로 끌어다 **FullDateAlternateKey**에 놓습니다.  데이터 형식 불일치를 나타내는 메시지가 표시되는 경우 CurrencyDate의 데이터 형식을 [DT_DBDATE]로 변경합니다.
  
    2.  **사용 가능한 조회 열** 목록에서 **DateKey**왼쪽에 있는 확인란을 선택합니다.  
  
9. **고급** 페이지에서 캐싱 옵션을 검토합니다.  
  
10. **확인**을 선택하여 **데이터 흐름** 디자인 화면으로 돌아갑니다.  
  
11. **Lookup Date Key** 변환을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.
  
12. **속성** 창에서 **LocaleID** 속성이 **영어(미국)** 이고 **DefaultCodePage** 속성이 **1252**인지 확인합니다.  
  
## <a name="go-to-next-task"></a>다음 작업으로 이동
[7단계: OLE DB 대상 추가 및 구성](../integration-services/lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
## <a name="see-also"></a>참고 항목  
[조회 변환](../integration-services/data-flow/transformations/lookup-transformation.md)  
