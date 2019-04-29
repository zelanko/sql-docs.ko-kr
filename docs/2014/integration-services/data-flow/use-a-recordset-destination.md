---
title: 레코드 집합 대상 사용 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Recordset destination
ms.assetid: a7b143dc-8008-404f-83b0-b45ffbca6029
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b87d71f8299c55e033adc21e25e29e8fb3d5e9d6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900003"
---
# <a name="use-a-recordset-destination"></a>레코드 집합 대상 사용
  레코드 집합 대상은 외부 데이터 원본에 데이터를 저장하지 않습니다. 대신 `Object` 데이터 형식의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지 변수에 저장된 레코드 집합의 데이터를 메모리에 저장합니다. 레코드 집합 대상이 데이터를 저장한 후에는 일반적으로 Foreach 루프 컨테이너를 Foreach ADO 열거자와 함께 사용하여 레코드 집합의 행을 한 번에 하나씩 처리합니다. Foreach ADO 열거자는 현재 행의 각 열 값을 개별 패키지 변수에 저장합니다. 그러면 Foreach 루프 컨테이너 내에 구성한 태스크가 변수에서 이러한 값을 읽어 와서 이를 가지고 몇 가지 동작을 수행합니다.  
  
 레코드 집합 대상은 다양한 시나리오에서 사용할 수 있습니다. 다음은 몇 가지 예입니다.  
  
-   메일 보내기 태스크와 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 식 언어를 사용하여 레코드 집합의 각 행에 대해 사용자 지정 전자 메일 메시지를 보낼 수 있습니다.  
  
-   데이터 흐름 태스크 내에서 원본으로 구성된 스크립트 구성 요소를 사용하여 열 값을 데이터 흐름의 열로 읽어올 수 있습니다. 그런 다음 변환 및 대상을 사용하여 행을 변환하고 저장할 수 있습니다. 이 예에서는 데이터 흐름 태스크가 각 행에 대해 한 번씩 실행됩니다.  
  
 다음 섹션에서는 먼저 레코드 집합 대상을 사용하는 일반적인 프로세스에 대해 설명한 다음 대상을 사용하는 방법에 대한 예를 보여 줍니다.  
  
## <a name="general-steps-to-using-a-recordset-destination"></a>레코드 집합 대상을 사용하는 일반적인 단계  
 다음 절차에서는 레코드 집합 대상에 데이터를 저장한 다음 Foreach 루프 컨테이너를 사용하여 각 행을 처리하는 데 필요한 단계를 요약합니다.  
  
#### <a name="to-save-data-to-a-recordset-destination-and-process-each-row-by-using-the-foreach-loop-container"></a>레코드 집합 대상에 데이터를 저장하고 Foreach 루프 컨테이너를 사용하여 각 행을 처리하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 만들거나 엽니다.  
  
2.  레코드 집합 대상이 메모리에 저장한 레코드 집합을 보유할 변수를 만든 다음 이 변수의 유형을 `Object`로 설정합니다.  
  
3.  사용할 레코드 집합의 각 열 값을 보유할 적절한 유형의 추가 변수를 만듭니다.  
  
4.  데이터 흐름에서 사용할 데이터 원본에 필요한 연결 관리자를 추가하고 구성합니다.  
  
5.  패키지에 데이터 흐름 태스크를 추가하고 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 데이터 흐름 탭에서 데이터를 로드하고 변환할 원본과 변환을 구성합니다.  
  
6.  데이터 집합 대상을 데이터 흐름에 추가하고 이를 변환에 연결합니다. 레코드 집합 대상의 `VariableName` 속성에 대해 레코드 집합을 보유하기 위해 만든 변수의 이름을 입력합니다.  
  
7.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 제어 흐름 탭에서 Foreach 루프 컨테이너를 추가하고 이 컨테이너를 데이터 흐름 태스크 뒤에 연결합니다. 그런 다음 **Foreach 루프 편집기** 를 열어 다음과 같이 컨테이너를 구성합니다.  
  
    1.  **컬렉션** 페이지에서 Foreach ADO 열거자를 선택합니다. 그런 다음 **ADO 개체 원본 변수**에 대해 레코드 집합이 들어 있는 변수를 선택합니다.  
  
    2.  **변수 매핑** 페이지에서 사용할 각 열의 0부터 시작하는 인덱스를 적절한 변수에 매핑합니다.  
  
         루프가 반복될 때마다 열거자는 현재 행의 열 값으로 이러한 변수를 채웁니다.  
  
8.  Foreach 루프 컨테이너 내에서 변수의 값을 읽어 와서 레코드 집합의 행을 한 번에 하나씩 처리하는 태스크를 추가하고 구성합니다.  
  
## <a name="example-of-using-the-recordset-destination"></a>레코드 집합 대상을 사용하는 예  
 다음 예에서는 데이터 흐름 태스크가 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 직원에 대한 정보를 Sales.SalesPerson 테이블에서 레코드 집합 대상으로 로드합니다. 그러면 Foreach 루프 컨테이너에서 데이터 행을 한 번에 하나씩 읽고 메일 보내기 태스크를 호출합니다. 메일 보내기 태스크는 식을 사용하여 보너스 금액에 관한 사용자 지정 전자 메일 메시지를 각 판매 직원에 보냅니다.  
  
#### <a name="to-create-the-project-and-configure-the-variables"></a>프로젝트를 만들고 변수를 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 새 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 만듭니다.  
  
2.  **SSIS** 메뉴에서 **변수**를 선택합니다.  
  
3.  **변수** 창에서 다음과 같이 레코드 집합과 현재 행의 열 값을 보유할 변수를 만듭니다.  
  
    1.  `BonusRecordset`이라는 변수를 만들고 이 변수의 유형을 `Object`로 설정합니다.  
  
         `BonusRecordset` 변수는 레코드 집합을 보유합니다.  
  
    2.  `EmailAddress`이라는 변수를 만들고 이 변수의 유형을 `String`로 설정합니다.  
  
         `EmailAddress` 변수는 판매 직원의 전자 메일 메시지를 보유합니다.  
  
    3.  `FirstName`이라는 변수를 만들고 이 변수의 유형을 `String`로 설정합니다.  
  
         `FirstName` 변수는 판매 직원의 이름을 보유합니다.  
  
    4.  `Bonus`이라는 변수를 만들고 이 변수의 유형을 `Double`로 설정합니다.  
  
         `Bonus` 변수는 판매 직원의 보너스를 보유합니다.  
  
#### <a name="to-configure-the-connection-managers"></a>연결 관리자를 구성하려면  
  
1.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 연결 관리자 영역에서 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 예제 데이터베이스에 연결하는 새 OLE DB 연결 관리자를 추가하고 구성합니다.  
  
     데이터 흐름 태스크의 OLE DB 원본은 이 연결 관리자를 사용하여 데이터를 검색합니다.  
  
2.  연결 관리자 영역에서 사용 가능한 SMTP 서버에 연결하는 새 SMTP 연결 관리자를 추가하고 구성합니다.  
  
     Foreach 루프 컨테이너 내의 메일 보내기 태스크는 이 연결 관리자를 사용하여 전자 메일을 보냅니다.  
  
#### <a name="to-configure-the-data-flow-and-the-recordset-destination"></a>데이터 흐름 및 레코드 집합 대상을 구성하려면  
  
1.  **디자이너의** 제어 흐름 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 탭에서 디자인 화면에 데이터 흐름 태스크를 추가합니다.  
  
2.   **데이터 흐름** tab, add an OLE DB source to the 데이터 흐름 task, and then open the **OLE DB 원본 편집기**를 엽니다.  
  
3.  OLE DB 원본 편집기의 **연결 관리자** 페이지에서 다음과 같이 원본을 구성합니다.  
  
    1.  **OLE DB 연결 관리자**에 대해 이전에 만든 OLE DB 연결 관리자를 선택합니다.  
  
    2.  **데이터 액세스 모드**에 대해 **SQL 명령**을 선택합니다.  
  
    3.  **SQL 명령 텍스트**에 대해 다음 쿼리를 입력합니다.  
  
        ```  
        SELECT     Person.Contact.EmailAddress, Person.Contact.FirstName, CONVERT(float, Sales.SalesPerson.Bonus) AS Bonus  
        FROM         Sales.SalesPerson INNER JOIN  
                              Person.Contact ON Sales.SalesPerson.SalesPersonID = Person.Contact.ContactID  
        ```  
  
        > [!NOTE]  
        >  Bonus 열의 `currency` 값을 `float` 유형의 패키지 변수에 로드하려면 먼저 이 값을 `Double`로 변환해야 합니다.  
  
4.  **데이터 흐름** 탭에서 레코드 집합 대상을 추가하고 이 대상을 OLE DB 원본 뒤에 연결합니다.  
  
5.  **레코드 집합 대상 편집기**를 열고 다음과 같이 대상을 구성합니다.  
  
    1.  에 **구성 요소 속성** 탭에 대 한 `VariableName` 속성을 선택 `User::BonusRecordset`합니다.  
  
    2.  **입력 열** 탭에서 사용 가능한 열 세 개를 모두 선택합니다.  
  
#### <a name="to-configure-the-foreach-loop-container-and-run-the-package"></a>Foreach 루프 컨테이너를 구성하고 패키지를 실행하려면  
  
1.  **디자이너의** 제어 흐름 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 탭에서 Foreach 루프 컨테이너를 추가하고 이 컨테이너를 데이터 흐름 태스크 뒤에 연결합니다.  
  
2.  **Foreach 루프 편집기**를 열고 다음과 같이 컨테이너를 구성합니다.  
  
    1.  에 **컬렉션** 페이지에 대 한 **열거자**를 선택 **Foreach ADO 열거자**, 및에 대 한 **ADO 개체 원본 변수**, 선택`User::BonusRecordset`.  
  
    2.  에 **변수 매핑** 페이지, 지도 `User::EmailAddress` 인덱스 0으로, 하 `User::FirstName` , 인덱스 1 및 `User::Bonus` 를 인덱스 2입니다.  
  
3.  **제어 흐름** 탭에서 Foreach 루프 컨테이너 내에 메일 보내기 태스크를 추가합니다.  
  
4.  **메일 보내기 태스크 편집기**를 열고 **메일** 페이지에서 다음과 같이 태스크를 구성합니다.  
  
    1.  **SmtpConnection**에 대해 이전에 구성한 SMTP 연결 관리자를 선택합니다.  
  
    2.  **보낸 사람**에 대해 적절한 전자 메일 주소를 입력합니다.  
  
         자신의 전자 메일 주소를 사용하면 패키지가 성공적으로 실행되는지 확인할 수 있습니다. 메일 보내기 태스크를 통해 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]의 가상 판매 직원에게 메시지를 보내면 해당 수신인에게 메시지를 배달할 수 없다는 내용의 메시지가 반환됩니다.  
  
    3.  **받는 사람**에 대해 기본 전자 메일 주소를 입력합니다.  
  
         이 값은 사용되지 않지만 런타임에 각 판매 직원의 전자 메일 주소로 대체됩니다.  
  
    4.  **제목**에 대해 "연간 보너스 안내"를 입력합니다.  
  
    5.  **MessageSourceType**에 대해 **직접 입력**을 선택합니다.  
  
5.  **메일 보내기 태스크 편집기** 의 **식**페이지에서 줄임표 단추(**...**)를 클릭하여 **속성 식 편집기**를 엽니다.  
  
6.  **속성 식 편집기**에서 다음 정보를 입력합니다.  
  
    1.  **ToLine**에 대해 다음 식을 추가합니다.  
  
        ```  
        @[User::EmailAddress]  
        ```  
  
    2.  **MessageSource** 속성에 대해 다음 식을 추가합니다.  
  
        ```  
        "Dear " +  @[User::FirstName] + ": The amount of your bonus for this year is $" +  (DT_WSTR, 12) @[User::Bonus] + ". Thank you!"  
        ```  
  
7.  패키지를 실행합니다.  
  
     올바른 SMTP 서버를 지정하고 자신의 전자 메일 주소를 입력한 경우 메일 보내기 태스크를 통해 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]의 가상 판매 직원에게 메시지를 보내면 해당 수신인에게 메시지를 배달할 수 없다는 내용의 메시지가 반환됩니다.  
  
  
