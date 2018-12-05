---
title: '2단계: 플랫 파일 연결 관리자 추가 및 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9a77dd32-d8c2-4961-ad37-2a971f9d6043
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cc3bd44753305f7509a8777c48265f3f0edd2f2c
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/29/2018
ms.locfileid: "52617663"
---
# <a name="lesson-1-2---adding-and-configuring-a-flat-file-connection-manager"></a>1-2단원: 플랫 파일 연결 관리자 추가 및 구성
이 태스크에서는 플랫 파일 연결 관리자를 방금 작성한 패키지에 추가합니다. 플랫 파일 연결 관리자를 통해 패키지가 플랫 파일에서 데이터를 추출할 수 있습니다. 플랫 파일 연결 관리자를 사용하여 패키지가 플랫 파일에서 데이터를 추출할 때 적용할 열 구분 기호를 포함한 파일 형식, 파일 이름과 위치 및 로캘과 코드 페이지를 지정할 수 있습니다. 또한 개별 열의 데이터 형식을 수동으로 지정하거나 **열 유형 제안** 대화 상자를 사용하여 추출된 데이터 열을 자동으로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 데이터 형식에 매핑할 수 있습니다.  
  
작업할 파일 형식마다 새 플랫 파일 연결 관리자를 만들어야 합니다. 이 자습서에서는 데이터 형식이 정확히 일치하는 여러 플랫 파일에서 데이터를 추출하므로 패키지에 하나의 플랫 파일 연결 관리자만 추가하고 구성해야 합니다.  
  
이 자습서에서는 플랫 파일 연결 관리자에서 다음 속성을 구성하는 과정을 다룹니다.  
  
-   **열 이름:** 플랫 파일에는 열 이름이 없으므로 플랫 파일 연결 관리자가 기본 열 이름을 만듭니다. 이러한 기본 이름은 각 열이 나타내는 내용을 식별하는 데 유용하지 않습니다. 이러한 기본 이름을 보다 유용하게 만들려면 기본 이름을 플랫 파일 데이터가 로드될 팩트 테이블과 일치하는 이름으로 변경해야 합니다.  
  
-   **데이터 매핑:** 플랫 파일 연결 관리자에서 지정하는 데이터 형식 매핑은 연결 관리자를 참조하는 모든 플랫 파일 데이터 원본 구성 요소에서 사용됩니다. 플랫 파일 연결 관리자를 사용하여 데이터 형식을 수동으로 매핑하거나 **열 유형 제안** 대화 상자를 사용할 수 있습니다. 이 자습서에서는 **열 유형 제안** 대화 상자에 제안된 매핑을 표시한 다음 **플랫 파일 연결 관리자 편집기** 대화 상자에서 필요한 매핑을 수동으로 만드는 과정을 다룹니다.  
  
플랫 파일 연결 관리자는 데이터 파일에 대한 로캘 정보를 제공합니다. 컴퓨터가 영어(미국) 국가별 옵션을 사용하도록 구성되지 않은 경우 **플랫 파일 연결 관리자 편집기** 대화 상자에서 추가 속성을 설정해야 합니다.  
  
### <a name="to-add-a-flat-file-connection-manager-to-the-ssis-package"></a>SSIS 패키지에 플랫 파일 연결 관리자를 추가하려면  
  
1.  **연결 관리자** 영역의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음 **새 플랫 파일 연결**을 클릭합니다.  
  
2.  **플랫 파일 연결 관리자 편집기** 대화 상자에서 **연결 관리자 이름**에 **Sample Flat File Source Data**를 입력합니다.  
  
3.  **찾아보기**를 클릭합니다.  
  
4.  **열기** 대화 상자에서 컴퓨터에 있는 SampleCurrencyData.txt 파일을 찾습니다.  
  
    예제 데이터는 [!INCLUDE[ssIS](../includes/ssis-md.md)] 단원 패키지에 포함되어 있습니다. 예제 데이터 및 단원 패키지를 다운로드하려면 다음을 수행합니다.  
  
    1.   [Integration Services 제품 예제](https://www.microsoft.com/download/details.aspx?id=56827)로 이동합니다.  
  
    2.  **DOWNLOADS** 탭을 클릭합니다.  
  
    3.  SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 파일을 클릭합니다.  
  
5.  첫 번째 데이터 행 확인란에서 열 이름의 선택을 취소합니다.  
  
### <a name="to-set-locale-sensitive-properties"></a>로캘 구분 속성을 설정하려면  
  
1.  **플랫 파일 연결 관리자 편집기** 대화 상자에서 **일반**을 클릭합니다.  
  
2.  **로캘** 을 영어(미국)로 설정하고 **코드 페이지** 를 1252로 설정합니다.  
  
### <a name="to-rename-columns-in-the-flat-file-connection-manager"></a>플랫 파일 연결 관리자에서 열 이름을 바꾸려면  
  
1.  **플랫 파일 연결 관리자 편집기** 대화 상자에서 **고급**을 클릭합니다.  
  
2.  속성 창에서 다음 내용을 변경합니다.  
  
    -   **Column 0** 이름 속성을 **AverageRate**로 변경합니다.  
  
    -   **Column 1** 이름 속성을 **CurrencyID**로 변경합니다.  
  
    -   **Column 2** 이름 속성을 **CurrencyDate**로 변경합니다.  
  
    -   **Column 3** 이름 속성을 **EndOfDayRate**로 변경합니다.  
  
    > [!NOTE]  
    > 기본적으로 4개의 열이 모두 초기에 **OutputColumnWidth** 가 50인 문자열 데이터 형식 [DT_STR]로 설정되어 있습니다.  
  
### <a name="to-remap-column-data-types"></a>열 데이터 형식을 다시 매핑하려면  
  
1.  **플랫 파일 연결 관리자 편집기** 대화 상자에서 **유형 제안**을 클릭합니다.  
  
    [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 처음 200개의 데이터 행에 기초하여 가장 적합한 데이터 형식을 자동으로 제안합니다. 또한 이러한 제안 옵션을 변경하여 더 많거나 적은 데이터를 샘플링하거나 정수 또는 부울 데이터의 기본 데이터 형식을 지정하거나 공백을 안쪽 여백으로 문자열 열에 추가할 수 있습니다.  
  
    여기에서는 **열 유형 제안** 대화 상자의 옵션을 변경하지 않고 **확인** 을 클릭하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 열의 데이터 형식을 제안하게 합니다. 이렇게 하면 **에서 제안하는 열 데이터 형식을 볼 수 있는** 플랫 파일 연결 관리자 편집기 **대화 상자의** 고급 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]창으로 돌아갑니다. **취소**를 클릭하면 열 메타데이터에 대한 제안이 생성되지 않고 기본 문자열(DT_STR) 데이터 형식이 사용됩니다.  
  
    이 자습서에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 SampleCurrencyData.txt 파일 데이터에 대해 다음 테이블의 두 번째 열에 표시된 데이터 형식을 제안합니다. 그러나 이후 단계에서 정의할 대상 열에 필요한 데이터 형식은 다음 표의 마지막 열에서 확인할 수 있습니다.  
  
    |플랫 파일 열|제안 형식|대상 열|대상 유형|  
    |--------------------|------------------|----------------------|--------------------|  
    |AverageRate|float [DT_R4]|FactCurrencyRate.AverageRate|FLOAT|  
    |CurrencyID|string [DT_STR]|DimCurrency.CurrencyAlternateKey|nchar(3)|  
    |CurrencyDate|date [DT_DATE]|DimDate.FullDateAlternateKey|날짜|  
    |EndOfDayRate|float [DT_R4]|FactCurrencyRate.EndOfDayRate|FLOAT|  
  
    **CurrencyID** 열에 제안된 데이터 형식은 대상 테이블의 필드 데이터 형식과 호환되지 않습니다. `DimCurrency.CurrencyAlternateKey` 데이터 형식은 nchar(3)이므로 **CurrencyID**를 문자열 [DT_STR]에서 유니코드 문자열 [DT_WSTR]로 변경해야 합니다. 또한 `DimDate.FullDateAlternateKey` 필드는 Date 데이터 형식으로 정의되므로 **CurrencyDate** 를 날짜 [DT_Date]에서 데이터베이스 날짜 [DT_DBDATE]로 변경해야 합니다.  
  
2.  목록에서 CurrencyID 열을 선택하고 속성 창에서 **CurrencyID** 열의 데이터 형식을 문자열 [DT_STR]에서 유니코드 문자열 [DT_WSTR]로 변경합니다.  
  
3.  속성 창에서 **CurrencyDate** 열의 데이터 형식을 날짜 [DT_DATE]에서 데이터베이스 날짜 [DT_DBDATE]로 변경합니다.  
  
4.  **확인**을 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[3단계: OLE DB 연결 관리자 추가 및 구성](../integration-services/lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
## <a name="see-also"></a>참고 항목  
[플랫 파일 연결 관리자](../integration-services/connection-manager/flat-file-connection-manager.md)  
[Integration Services 데이터 형식](../integration-services/data-flow/integration-services-data-types.md)  
  
  
  
