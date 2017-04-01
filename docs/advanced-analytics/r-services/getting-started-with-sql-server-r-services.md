---
title: "SQL Server R Services 시작하기 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 5b28a663-effe-41f6-9bda-eda95f0c6943
caps.latest.revision: 34
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 32
---
# SQL Server R Services 시작하기
 고급 분석 솔루션을 구축하는 일반적인 워크플로는 데이터 탐색 및 예측 모델링으로 시작하지만 데이터 과학자는 현재 작업에 효과적이라고 입증된 R 스크립트 및 모델을 개발합니다. 스크립트 및 모델이 준비되면 프로덕션 환경에 배포하고 기존 응용 프로그램이나 새 응용 프로그램과 통합할 수 있습니다.   
  
SQL Server R Services는 이러한 데이터 과학 작업을 완료하는 데 도움이 되도록 설계되었습니다. 선호하는 R 또는 SQL 도구를 계속 사용하면서도 추가 하드웨어 없이 수십억 개 레코드로 분석을 확장하고, 성능을 향상하고, 불필요한 데이터 이동을 방지할 수 있습니다. 이제 R 코드를 다른 언어로 다시 작성하지 않고도 프로덕션 환경에 배포할 수 있습니다. 또한 SQL을 사용하여 구현하기 어려울 수 있는 통계 계산에 R을 쉽게 사용할 수 있습니다. 뿐만 아니라 메모리 내 데이터베이스 엔진 및 columnstore 인덱스와 같은 기능을 사용하여 최대 성능을 얻기 위해 SQL Server의 성능을 활용할사용하여 최대 성능을 얻을 수 있습니다.  
  
다음 섹션에서는 몇 가지 일반적인 분석 워크플로와 SQL Server R Services로 이러한 워크플로를 지원하는 방법에 대한 간략한 개요를 제공합니다.  

> [!TIP] 빠르게 시작하려면 이 자습서를 참조하세요. 스키 대여 사업에서 기계 학습을 이용하여 향후 대여 상황을 예측하고 수요에 맞추기 위해 직원의 일정을 정하는 방법을 알아봅니다.
> 
> [Build an intelligent app with SQL Server and R](https://www.microsoft.com/sql-server/developer-get-started/r)(SQL Server 및 R을 사용하여 지능형 앱 구축)


  
-   **개발**  
  
     데이터 과학자는 대개 자신이 선택한 R IDE를 사용하여 자신의 워크스테이션에서 데이터를 탐색하고 예측 모델을 구축합니다. 데이터 과학자는 좋은 예측 모델을 얻을 때까지 테스트와 튜닝을 반복합니다. 
     
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 클라이언트 구성 요소는 데이터 과학자의 실험 및 개발에 필요한 모든 도구를 제공합니다. 이러한 도구에는 R 런타임, 표준 R 작업의 성능을 향상시키기 위한 인텔 수학 커널 라이브러리 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R 코드 실행을 지원하는 향상된 R 패키지 집합이 포함됩니다.  
  
     데이터 과학자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하여 평소와 같이 로컬 분석을 위해 클라이언트에 제공합니다. 그러나 더 나은 방법은 **ScaleR** API를 사용해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 계산을 푸시하여 비용이 많이 들고 안전하지 않은 데이터를 이동을 방지하는 것입니다.  
  
     R 솔루션을 개발하기 위해 데이터 과학자는 [R Tools for Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx) 또는 RStudio를 포함해 R을 지원하는 Windows 기반 IDE를 사용할 수 있습니다.  
 
    ![rsql_keyscenario2](../../advanced-analytics/r-services/media/rsql-keyscenario2.PNG) 
 
     자세한 내용은 [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)을 참조하세요.  

  
-   **최적화**  
  
     R로 큰 데이터 집합 분석 시 공용 런타임 구현이 단일 스레드이고 로컬 컴퓨터에서 사용 가능한 메모리에 적합한 데이터 집합만을 수용할 수 있으므로, 데이터 과학자는 성능 및 확장 문제에 직면합니다. 더 나은 성능을 얻고 더 많은 데이터를 사용하기 위해 데이터 과학자는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 일부로 제공되는 **ScaleR** API를 사용할 수 있습니다. **RevoScaleR** 패키지에는 R의 가장 인기 있는 일부 함수가 구현되었고 병렬 처리 및 확장성을 제공하도록 다시 설계되었습니다. 또한 일반적으로는 훨씬 큰 메모리와 계산력을 갖춘 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 계산을 푸시하여 성능과 확장을 더 증대하는 함수도 포함되어 있습니다.  
  
     자세한 내용은 [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md)을 참조하세요.  
  
-   **배포**  
  
     R 스크립트 또는 모델이 프로덕션 환경에 사용할 수 있게 준비되면 데이터베이스 개발자는 코드 또는 모델을 저장 프로시저에 포함하고 응용 프로그램에서 저장된 코드를 호출할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R 코드를 저장하고 실행하면 많은 이점이 있습니다. 편리한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 인터페이스를 사용하고 모든 계산이 데이터베이스에서 실행되어 불필요한 데이터 이동을 방지할 수 있습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하여 프로덕션의 예측 모델에서 점수를 생성하거나 R에서 생성된 플롯을 반환하고 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]과 같은 응용 프로그램에 제공할 수 있습니다.  
  
     시스템 저장 프로시저에 포함된 R 코드를 추가로 최적화하려면 더 큰 데이터 집합에서 작동할 수 있는 [ScaleR](https://msdn.microsoft.com/microsoft-r/rserver/rserver-scaler-getting-started) 패키지 API를 사용하는 것이 좋습니다. 이러한 패키지는 다중 스레드, 다중 코어 및 다중 프로세스 계산에 대해 데이터베이스 내 실행을 지원합니다.  
  
     R 코드를 프로덕션에 배포해야 할 경우 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 은 R 및 SQL의 장점을 제공합니다. SQL을 사용하여 구현하기 어려운 통계적 계산에 R을 사용할 수 있지만 메모리 내 데이터베이스 엔진 및 columnstore 인덱스 등의 기능을 사용하여 최고의 성능을 달성하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 성능을 활용할 수 있습니다.  
  
    ![rsql_keyscenario1](../../advanced-analytics/r-services/media/rsql-keyscenario1.PNG)  
  
     자세한 내용은 [작업에서 R 코드 활용](../../advanced-analytics/r-services/operationalizing-your-r-code.md)을 참조하세요.  
 
 > [!TIP] Microsoft Virtual Academy에서 무료로 다운로드할 수 있는 책 [Data Science with Microsoft SQL Server 2016](https://mva.microsoft.com/ebooks/)(데이터 과학 및 Microsoft SQL Server 2016)에서 SQL Server를 데이터 과학과 통합하는 방법을 알아보세요.

-   **관리 및 모니터링**  
  
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]는 데이터베이스 엔진의 보안을 유지하고 R 세션을 격리하는 새로운 확장성 아키텍처를 사용합니다. 또한, R 스크립트를 실행할 수 있는 사용자를 제어하고 R 코드로 액세스할 수 있는 데이터베이스를 지정할 수도 있습니다. 대규모 계산이 서버의 전반적인 성능을 저해하지 않도록 R 런타임에 할당된 리소스 양을 제어할 수 있습니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R 작업 실행 시 다른 저장 프로시저에서 하는 것과 마찬가지로, 분석에서 사용하는 데이터를 제어하고 감사하거나 작업을 예약하고 R 스크립트를 포함한 워크플로를 제작할 수도 있습니다.  
  
     자세한 내용은 [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)를 참조하세요.  
  
  
-   **통합**  
  
     더 이상 기업 도구가 일부 외부 R 런타임 환경에서 작동하도록 하는 데 IT 예산을 지출할 필요가 없습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 익숙한 환경에서 작업하며 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]을 사용하여 통합된 워크플로 및 보고 솔루션을 개발할 수 있습니다.  
  
     자세한 내용은 [SQL Server에서 R을 사용하는 워크플로 만들기](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md)를 참조하세요.  
  
  
## <a name="how-do-i-get-it"></a>얻는 방법  
   
  
+   **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이상 설치 및 R Services(In-Database)를 사용하도록 설정**  
  
    [SQL Server R Services&#40;In-Database&#41; 설치](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  
-   **클라이언트 워크스테이션 설정**  
  
     [Set Up a Data Science Client](../../advanced-analytics/r-services/set-up-a-data-science-client.md)(데이터 과학 클라이언트 설정)  
   
> [!TIP]   
>   
> R 작업용 서버는 만들어야 하지만 SQL Server는 필요하지 않나요? [Microsoft R Server](https://msdn.microsoft.com/library/mt674874.aspx)를 사용해 보세요.  
  
## <a name="how-to-run-r-code-using-sql-server-r-services"></a>SQL Server R Services를 사용하여 R 코드를 실행하는 방법  
 설치가 완료되면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저에 R을 포함하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터에서 사용 가능한 임시 R 스크립트를 작성하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R 코드를 실행할 수 있습니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 R을 호출하고 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 결과를 반환하는 방법을 알아봅니다.  
  
     [Transact-SQL에서 R 코드 사용](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)  
  
-   고급 분석 솔루션을 만들고 SQL Server R Services를 사용하여 배포하는 전체 흐름 이해  
  
     [데이터 과학 종단 간 연습](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  
  
-   확장 가능한 고성능 분석에 RevoScaleR 패키지를 사용하는 방법 및 SQL Server 컴퓨터에 R 계산을 푸시하는 방법을 알아봅니다.  
  
     [데이터 과학 심층 분석: RevoScaleR 패키지 사용](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
-   예측용 모델을 호출하거나 모델을 사용하지 않거나 응용 프로그램에서 예측 정보를 얻을 수 있도록 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저에 작동하는 R 스크립트를 포함합니다.  
  
     [SQL 개발자를 위한 데이터베이스 내 고급 분석](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
  
-   기계 학습 프로세스를 자동화하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 스택에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 관련 비즈니스 인텔리전스 도구를 사용합니다. 데이터 준비 및 보고는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 사용하여 자동화하여 R 도표 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 또는 Power View를 사용하는 다른 보고서를 표시할 수 있습니다.  
  
+ 솔루션 템플릿과 샘플 R 코드를 포함한 추가 샘플  
   [SQL Server R Services 자습서](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Microsoft R Server&#40;독립 실행형&#41; 시작](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  