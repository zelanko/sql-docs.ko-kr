---
title: "데이터 과학 심층 분석: RevoScaleR 패키지 사용 | Microsoft Docs"
ms.custom: ""
ms.date: "09/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# 데이터 과학 심층 분석: RevoScaleR 패키지 사용
이 자습서에서는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 제공하는 향상된 R 패키지를 소개합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 R 패키지를 실행하기 위해 확장 가능한 엔터프라이즈 프레임워크를 사용하는 방법을 알아봅니다.   데이터 과학자는 이러한 확장 가능한 R 함수를 사용하여 고성능 빅 데이터 분석을 지원하기 위해 로컬 또는 서버 컨텍스트에서 실행되는 사용자 지정 R 솔루션을 빌드할 수 있습니다.  
  
이 자습서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 R 워크스테이션 간에 데이터를 이동하고, 데이터를 분석하고 그림으로 나타내며, 모델을 만들고 배포하는 방법을 알아봅니다.  
    
## 개요 
 
ScaleR 패키지의 유연성 및 처리 능력을 설명하기 위해 이 자습서에서는 자주 데이터를 이동하고 계산 컨텍스트를 바꿉니다.

+ 데이터는 처음에 CSV 파일 또는 XDF 파일에서 가져온 것입니다. RevoScaleR 패키지의 함수를 사용하여 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 가져옵니다.    
+ 모델 학습 및 점수 매기기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계산 컨텍스트에서 수행됩니다. 
    **rx** 함수를 사용해 새로운 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 만들어 점수 매기기 결과를 저장합니다.    
+ 서버 계산 컨텍스트와 로컬 계산 컨텍스트에서 모두 그림을 만듭니다.  
+ 모델을 학습하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 이미 저장되어 있는 데이터를 사용합니다. 모든 계산은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 수행됩니다.    
+ 데이터의 하위 집합을 추출한 다음 로컬 워크스테이션에서 분석에 다시 사용하기 위해 XDF 파일로 저장합니다.    
+ 점수 매기기 프로세스 중에 사용되는 새 데이터는 ODBC 연결을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 추출됩니다. 모든 계산은 로컬 워크스테이션에서 수행됩니다. 
+ 마지막으로 서버 계산 컨텍스트를 사용하여 사용자 지정 R 함수를 기반으로 시뮬레이션을 수행합니다.

### 지금 시작  

설치를 포함하지 않고 이 자습서를 완료하는 데 약 1시간 정도 걸립니다.  

-   [1단원: R을 사용하여 SQL Server 데이터 작업](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
-   [2단원: R 스크립트 만들기 및 실행](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
-   [3단원: R을 사용하여 데이터 변환](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
-   [4단원: 로컬 계산 컨텍스트에서 데이터 분석](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
-   [5단원: 간단한 시뮬레이션 만들기](../../advanced-analytics/r-services/lesson-5-create-a-simple-simulation-data-science-deep-dive.md)  

      
### 대상 사용자  
  
이 자습서는 데이터 과학자나 탐색, 통계 분석 및 모델 튜닝을 비롯한 데이터 과학 작업과 R에 어느 정도 익숙한 사용자를 위해 작성되었습니다.  그러나 모든 코드가 제공되므로 필요한 서버 및 클라이언트 환경이 있다고 가정하면 쉽게 코드를 실행하고 내용을 따라갈 수 있습니다.  
  
또한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문과 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 Visual Studio 등의 다른 데이터베이스 도구를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 액세스하는 방법을 알고 있어야 합니다.  
  
> [!TIP]  
> 중단한 위치부터 다시 시작하기 쉽도록 다음 단원으로 넘어가기 전에 R 작업 영역을 저장하세요.  
  
### 필수 구성 요소  
  
-   **R을 지원하는 데이터베이스 서버**  
  
    [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 설치하고 SQL Server R Services(in-Database)를 사용하도록 설정합니다. 이 프로세스는 [SQL Server 2016 온라인 설명서](http://msdn.microsoft.com/library/mt696069(SQL.130).aspx)에 설명되어 있습니다.  
  
-   **데이터베이스 사용 권한**  
  
    모델 학습에 사용되는 쿼리를 실행하려면 데이터가 저장된 **db_datareader** 데이터베이스에 대한 권한이 있어야 합니다.  
  
  
-   **데이터 과학 워크스테이션**  
  
    RevoScaleR 패키지를 설치해야 합니다. 이 작업을 수행하는 가장 쉬운 방법은 Microsoft R Server(독립 실행형) 또는 Microsoft R Client를 설치하는 것입니다. 자세한 내용은 [데이터 과학 클라이언트 설정](http://msdn.microsoft.co/library/mt696067(SQL.130).aspx)을 참조하세요.
      
    > [!NOTE] 
    > 다른 버전의 Revolution R Enterprise 또는 Revolution R Open은 지원되지 않습니다. 
    > 
    > ScaleR 함수만 원격 계산 컨텍스트를 사용할 수 있으므로 R 3.2.2와 같은 R의 오픈 소스 배포는 이 자습서에서 작동하지 않습니다. 
  
-   **추가 R 패키지**  
  
    이 자습서에서는 **dplyr**, **ggplot2**, **ggthemes**, **reshape2** 및 **e1071** 패키지를 설치해야 합니다. 지침은 자습서에 설명되어 있습니다.  
  
    학습이 수행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에도 모든 패키지를 설치해야 합니다. SQL Server에서 사용하는 R 패키지 라이브러리에 패키지를 설치해야 합니다. **사용자 라이브러리에 패키지를 설치하지 마세요.** 이 폴더에 패키지를 설치할 수 있는 권한이 없으면 패키지를 추가하도록 데이터베이스 관리자에게 요청하세요.   
  
자세한 내용은 [데이터 과학 연습의 필수 조건&#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/prerequisites-for-data-science-walkthroughs-sql-server-r-services.md)을 참조하세요.  
  
## 분산 R 솔루션을 위한 데이터 전략
    
일반적으로 로컬 개발 환경에서 R 스크립트 작성 및 실행을 시작하기 전에 항상 데이터 사용을 계획하고 최상의 성능을 위해 솔루션의 각 부분을 실행할 위치를 결정해야 합니다.  

이 자습서에서는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에 포함된 데이터 분석, 모델 작성 및 그림 만들기를 위한 고성능 함수를 사용합니다. 여기서는 일반적으로 이러한 함수를 ScaleR 또는 Microsoft R로 지칭하여 다른 오픈 소스 R 패키지에서 파생된 함수와 구분합니다. Microsoft R이 오픈 소스 R과 어떻게 다른지에 대한 자세한 내용은 이 [Getting Started guide](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#microsoft-r-products)(시작 가이드)를 참조하세요. 

ScaleR 함수를 사용할 경우 주요 이점은 이러한 함수가 로컬 또는 서버 *데이터 원본* 및 로컬 또는 원격 *계산 컨텍스트*를 지원한다는 것입니다.  따라서 이 자습서를 진행하면서 사용자 고유의 솔루션에 채택해야 할 수 있는 데이터 전략을 고려하세요.
  
-   **어떤 유형의 분석을 수행하고 싶으세요?** 혼자만 사용하기 위한 것인가요, 아니면 모델, 결과 또는 차트를 다른 사용자와 공유할 예정인가요?
 
    이 자습서에서는 개발 환경과 서버 간에 결과를 이동하여 쉽게 공유 및 분석하는 방법을 알아봅니다. 
  
-   **필요한 R 패키지가 원격 실행을 지원하나요?** [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 제공하는 ScaleR 패키지의 모든 함수는 원격 계산 컨텍스트에서 실행될 수 있으며 병렬 실행을 사용할 수도 있습니다. 반면, 타사 패키지의 함수는 단일 스레드 실행을 위한 추가 리소스가 필요할 수 있습니다. 
    
    이 자습서에서는 필요한 경우 로컬 계산 컨텍스트와 원격 계산 컨텍스트 간에 전환하여 서버 리소스를 활용하는 방법을 알아봅니다. 또한 *rxExec*에 표준 R 함수를 래핑하여 임의 R 함수의 원격 실행을 지원하는 방법을 알아봅니다.
    
  
-   **데이터가 어디에 있고 특성은 무엇인가요?**  데이터가 로컬에 있는 경우 모든 새 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 업로드할지 또는 로컬로 학습하고 모델을 데이터베이스에만 저장할지 결정해야 합니다. 그러나 프로덕션 환경에 배포하는 경우 엔터프라이즈 데이터에서 학습하고 ETL 프로세스를 사용하여 데이터를 정리하고 로드해야 할 수 있습니다.  
  
-   점수 매기기 데이터에도 비슷한 질문이 적용됩니다. 워크스테이션에서 점수 매기기 데이터에 대한 데이터 파이프라인을 만들 예정인가요, 아니면 엔터프라이즈 데이터 원본을 사용할 예정인가요? 데이터 정리 및 준비가 ETL 프로세스의 일부로 수행되어야 하나요, 아니면 일회성 실험을 수행할 예정인가요?  

    이 자습서에서는 효율적이고 안전하게 로컬 R 환경과 SQL Server 간에 데이터를 이동하는 방법을 알아봅니다. 
  
-   **어떤 계산 컨텍스트를 사용해야 하나요?** 샘플링된 데이터에서 로컬로 모델을 학습한 다음 테스트 및 프로덕션 환경을 위해 서버 데이터 사용으로 전환하려고 할 수 있습니다.

    이 자습서에서는 R을 사용하여 SQL Server와 R 간에 데이터를 이동하는 방법을 알아봅니다. 또한 XDF 파일을 사용하여 데이터 작업을 수행하는 방법과 ScaleR 함수를 사용하여 데이터를 청크로 처리하는 방법을 알아봅니다.  
  
 
  
## 다음 단계  
[1단원: R을 사용하여 SQL Server 데이터 작업&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
  
  
