---
title: "변경 데이터의 간격 지정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "증분 로드 [Integration Services], 간격 지정"
ms.assetid: 17899078-8ba3-4f40-8769-e9837dc3ec60
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# 변경 데이터의 간격 지정
  변경 데이터를 증분 로드하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 제어 흐름에서 첫 번째 태스크는 변경 간격의 끝점을 계산하는 것입니다. 이러한 끝점은 **datetime** 값이며 패키지에서 나중에 사용하기 위해 패키지 변수에 저장됩니다.  
  
> [!NOTE]  
>  제어 흐름 디자인의 전체 프로세스에 대한 설명은 [데이터 캡처 변경&#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)을 참조하세요.  
  
## 끝점에 대한 패키지 변수 설정  
 SQL 실행 태스크를 구성하여 끝점을 계산하기 전에 끝점을 저장할 패키지 변수를 정의해야 합니다.  
  
#### 패키지 변수를 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 새 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  **변수** 창에서 다음 변수를 만듭니다.  
  
    1.  간격의 시작 지점을 보관할 **datetime** 데이터 형식의 변수를 만듭니다.  
  
         이 예에서는 변수 이름으로 ExtractStartTime을 사용합니다.  
  
    2.  간격의 끝 지점을 보관할 **datetime** 데이터 형식의 다른 변수를 만듭니다.  
  
         이 예에서는 변수 이름으로 ExtractEndTime을 사용합니다.  
  
 여러 자식 패키지를 실행하는 마스터 패키지에서 끝점을 계산하는 경우 부모 패키지 변수 구성을 사용하여 이러한 변수 값을 각 자식 패키지에 전달할 수 있습니다. 자세한 내용은 [패키지 실행 태스크](../../integration-services/control-flow/execute-package-task.md) 및 [자식 패키지에서 변수 및 매개 변수의 값 사용](../../integration-services/packages/use-the-values-of-variables-and-parameters-in-a-child-package.md)을 참조하세요.  
  
## 변경 데이터의 시작 지점 및 끝 지점 계산  
 간격 끝점에 대한 패키지 변수를 설정한 후 해당 끝점의 실제 값을 계산하고 이러한 값을 해당 패키지 변수에 매핑할 수 있습니다. 이러한 끝점은 **datetime** 값이므로 **datetime** 값을 계산하거나 사용할 수 있는 함수를 사용해야 합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 식 언어와 Transact-SQL 모두에 **datetime** 값을 사용하는 함수가 있습니다.  
  
 **datetime** 값을 사용하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 식 언어의 함수  
 -   [DATEADD&#40;SSIS 식&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)  
  
-   [DATEDIFF&#40;SSIS 식&#41;](../../integration-services/expressions/datediff-ssis-expression.md)  
  
-   [DATEPART&#40;SSIS 식&#41;](../../integration-services/expressions/datepart-ssis-expression.md)  
  
-   [DAY&#40;SSIS 식&#41;](../../integration-services/expressions/day-ssis-expression.md)  
  
-   [GETDATE&#40;SSIS 식&#41;](../../integration-services/expressions/getdate-ssis-expression.md)  
  
-   [GETUTCDATE&#40;SSIS 식&#41;](../../integration-services/expressions/getutcdate-ssis-expression.md)  
  
-   [MONTH&#40;SSIS 식&#41;](../../integration-services/expressions/month-ssis-expression.md)  
  
-   [YEAR&#40;SSIS 식&#41;](../../integration-services/expressions/year-ssis-expression.md)  
  
 **datetime** 값을 사용하는 Transact-SQL의 함수  
 [날짜 및 시간 데이터 형식 및 함수&#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 이러한 **datetime** 함수 중 하나를 사용하여 끝점을 계산하기 전에 간격이 고정되어 있고 정기적으로 발생하는지 확인해야 합니다. 일반적으로 원본 테이블에서 발생한 변경 내용을 정기적으로 대상 테이블에 적용합니다. 예를 들어 이러한 변경 내용을 매시간, 매일 또는 매주 적용할 수 있습니다.  
  
 변경 간격이 고정적인지, 아니면 보다 임의적인지 이해한 후 끝점을 계산할 수 있습니다.  
  
-   **시작 날짜 및 시간 계산**. 이전 로드의 종료 날짜 및 시간을 현재 시작 날짜 및 시간으로 사용합니다. 증분 로드에 고정 간격을 사용하는 경우 Transact-SQL 또는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 식 언어의 **datetime** 함수를 사용하여 이 값을 계산할 수 있습니다. 그렇지 않은 경우 실행 간 끝점을 유지하고 SQL 실행 태스크 또는 스크립트 태스크를 사용하여 이전 끝점을 로드해야 할 수 있습니다.  
  
-   **종료 날짜 및 시간 계산**. 증분 로드에 고정 간격을 사용하는 경우 현재 종료 날짜 및 시간을 시작 날짜 및 시간의 오프셋으로 계산합니다. Transact-SQL 또는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 식 언어의 **datetime** 함수를 사용하여 이 값을 계산할 수도 있습니다.  
  
 다음 절차에서는 변경 간격에 고정 간격을 사용하며 증분 로드 패키지가 예외 없이 매일 실행된다고 가정합니다. 그렇지 않으면 누락된 간격의 변경 데이터가 손실됩니다. 간격의 시작 지점은 이틀 전 자정입니다. 즉, 24-48시간 전입니다. 간격의 끝 지점은 어제 자정입니다. 즉, 0-24시간 전의 전날 밤입니다.  
  
#### 캡처 간격의 시작 지점 및 끝 지점을 계산하려면  
  
1.  **디자이너의** 제어 흐름 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 탭에서 패키지에 SQL 실행 태스크를 추가합니다.  
  
2.  **SQL 실행 태스크 편집기**의 **일반** 페이지에서 다음 옵션을 선택합니다.  
  
    1.  **ResultSet**에 **단일 행**을 선택합니다.  
  
    2.  원본 데이터베이스에 대한 올바른 연결을 구성합니다.  
  
    3.  **SQLSourceType**에 **직접 입력**을 선택합니다.  
  
    4.  **SQLStatement**에 다음 SQL 문을 입력합니다.  
  
        ```  
        SELECT DATEADD(dd,0, DATEDIFF(dd,0,GETDATE()-1)) AS ExtractStartTime,  
          DATEADD(dd,0, DATEDIFF(dd,0,GETDATE())) AS ExtractEndTime  
  
        ```  
  
3.  **SQL 실행 태스크 편집기** 의 **결과 집합**페이지에서 ExtractStartTime 결과를 ExtractStartTime 패키지 변수에 매핑하고 ExtractEndTime 결과를 ExtractEndTime 패키지 변수에 매핑합니다.  
  
    > [!NOTE]  
    >  식을 사용하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 변수의 값을 설정하면 변수의 값에 액세스할 때마다 식이 평가됩니다.  
  
## 다음 단계  
 변경 범위의 시작 지점 및 끝 지점을 계산한 후 다음 단계는 변경 데이터가 준비되었는지 여부를 확인하는 것입니다.  
  
 **다음 항목:** [변경 데이터의 준비 여부 확인](../../integration-services/change-data-capture/determine-whether-the-change-data-is-ready.md)  
  
## 관련 항목:  
 [패키지에서 변수 사용](../Topic/Use%20Variables%20in%20Packages.md)   
 [Integration Services&#40;SSIS&#41; 식](../../integration-services/expressions/integration-services-ssis-expressions.md)   
 [SQL 실행 태스크](../../integration-services/control-flow/execute-sql-task.md)   
 [스크립트 태스크](../../integration-services/control-flow/script-task.md)  
  
  