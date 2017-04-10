---
title: "데이터 탐색 및 R을 통한 예측 모델링 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bf6de7e2-f394-4b8a-a4b7-0b8dadf25426
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# 데이터 탐색 및 R을 통한 예측 모델링
  데이터 과학자는 R을 사용하여 데이터를 탐색하고 예상 모델을 작성합니다. 이것은 일반적으로 우수한 예측 모델이 제공될 때까지 반복되는 시행 착오 프로세스입니다. 숙련된 데이터 과학자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 연결한 후 RODBC 패키지를 사용하여 로컬 워크스테이션에 데이터를 패치하며 데이터를 탐색하고 표준 R 패키지를 사용하여 예상 모델을 작성합니다.  
  
 그러나 이 방법에는 단점이 있습니다. 데이터 이동이 느리거나 비효율적이거나 보안이 제공되지 않을 수 있고 R 자체에 성능 및 확장성 제한이 있을 수 있습니다. 이러한 단점은 대량의 데이터를 이동 및 분석하거나 데이터 세트가 컴퓨터에서 이용할 수 있는 메모리와 맞지 않는 경우 더 분명하게 나타납니다.  
  
 새 확장 가능한 패키지를 사용 하 여 이러한 문제를 해결할 수 및 R 함수에 포함 된 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]합니다. **RevoScaleR** 패키지에는 R의 인기 있는 일부 함수가 구현되었고 병렬 처리 및 확장성을 제공하도록 다시 설계되었습니다. 또한, RevoScaleR 패키지는 *실행 컨텍스트*변경을 지원합니다. 즉, 전체 솔루션 또는 하나의 함수에 대하여 로컬 워크스테이션이 아닌 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 호스팅하는 컴퓨터 리소스를 사용하여 계산이 수행되도록 지정할 수 있습니다. 이러한 방식은 불필요한 데이터 이동을 방지하고 서버 컴퓨터의 더 큰 계산 리소스를 활용할 수 있는 등의 여러 가지 장점이 있습니다.  
  
 이 섹션에서는 데이터 과학자에게 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 사용 방법 및 R 솔루션 개발 및 테스트 관련 작업 수행 방법에 대한 안내를 제공합니다.  
  
##  <a name="bkmk_RDevTools"></a> R 개발 도구  
 Microsoft R 클라이언트는 데이터 과학자가 개발 및 예측 모델을 테스트 하기 위한 완벽 한 환경을 제공 합니다. R 클라이언트에는 다음이 포함 됩니다.  
  
-  **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** R 런타임과 표준 R 작업의 성능을 향상 하는 패키지, Intel 수학 커널 라이브러리와 같은 집합을 배포 합니다.  
  
-   **RevoScaleR:** 수 있는 R 패키지의 인스턴스로 계산을 푸시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]. 또한 성능 및 확장성 향상을 위해 새롭게 디자인 된 일반 R 함수 집합이 포함 되어 있습니다. 이러한 향상된 함수의 이름에는 **rx** 라는 접두사가 사용됩니다. 다양 한 원본;에 대 한 향상 된 데이터 공급자도 포함 됩니다. 이러한 함수에 접두사로 **Rx**합니다.  
  
-   **다양 한 개발 도구를 확보:** 같이 지 원하는 R, 모든 Windows 기반 코드 편집기를 사용할 수 있습니다 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 또는 RStudio 합니다. 다운로드 [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] RGui.exe 같은 R에 대 한 일반적인 명령줄 도구도 포함 되어 있습니다.  
  
##  <a name="bkmk_packages"></a> R 환경 및 패키지  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에서 지원되는 R 환경은 런타임, 오픈 소스 언어 및 여러 패키지에서 지원 및 확장되는 그래픽 엔진으로 구성됩니다. 언어는 패키지를 사용하여 구현되는 다양한 확장을 허용합니다.  
  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 와(과) 함께 사용할 수 있는 여러 가지 추가 R 패키지 소스:  
  
  
-   공용 저장소에서 일반 용도의 R 패키지 합니다. CRAN 등과 같은 공용 저장소에서 가장 인기 있는 오픈 소스 R 패키지를 가져올 수 있고 그러한 공용 저장소에는 데이터 과학자가 사용할 수 있는 6,000개 이상의 패키지가 호스팅되어 있습니다.  
  
     금융, 유전자 등 특정 영역에 대한 예측 분석을 지원하는 추가 패키지를 사용할 수 있습니다.  
  
     Windows 플랫폼에 대 한 R 패키지 zip 파일로 제공 됩니다 및 수 다운로드 되어 설치 GPL 라이선스.  
  
     사용 하도록 타사 패키지를 설치 하는 방법에 대 한 내용은 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 참조 [SQL Server에 추가 R 패키지 설치](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
-   추가 패키지 및 라이브러리에서 제공 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]합니다.   
  
      **RevoScaleR** 패키지 고성능 빅 데이터 분석, 향상 된 버전의 함수를 지 원하는 일반적인 데이터 과학 작업을 Naive Bayes, 선형 회귀, 시계열 모델의 경우 및 신경망 및 고급 수학 라이브러리에 대 한 최적화 된 학습자를 포함 합니다.  
  
     **RevoPemaR** 패키지를 사용하면 R에서 자체 병렬 외부 메모리 알고리즘을 개발할 수 있습니다.  
  
     이러한 패키지와 사용 하는 방법에 대 한 자세한 내용은 참조 [데이터 탐색 및 예측 모델링 & #40; 자습서: SQL Server R 서비스 & #41;](../../advanced-analytics/r-services/sql-server-r-services.md)합니다.  
  
## 데이터 원본 및 계산 컨텍스트 사용  
 RevoScaleR 패키지를 사용 하 여 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 몇 가지 중요 한 새로운 함수 R 코드에 사용할 수 있습니다.  
  
-   [RxSqlServerData](RxSqlServerData.md) 는 향상 된 데이터 연결을 지원 하도록 RevoScaleR 패키지에서 제공 하는 함수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
     R 코드에서 이 함수를 사용하여 *데이터 원본*을 정의할 수 있습니다. 데이터 원본 개체는 데이터가 있고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 읽고 쓰는 작업을 관리하는 서버와 테이블을 지정합니다.  
  
-    [RxInSqlServer](rxInSqlServer.md) 함수를 사용 하 여 지정할 수 있습니다는 *계산 컨텍스트*합니다.  R 코드를 실행 하는 위치를 나타낼 수 있습니다 즉,: 호스팅하는 컴퓨터 또는 로컬 워크스테이션에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.  
  
     계산 컨텍스트를 설정 하면 R 작업 RevoScaleR 패키지에서 제공 하 고 관련 함수는 원격 실행 컨텍스트를 지원 하는 유일한 계산을 영향을 줍니다. 실행할 수 있지만 원격 계산 컨텍스트에서 표준 CRAN 패키지를 기반으로 하는 R 솔루션 실행할 수 없습니다는 일반적으로 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] T-SQL에서 시작 하는 경우에 컴퓨터입니다. 그러나 사용할 수는 `rxExec` 개별 R 함수를 호출 하에서 원격으로 실행할 함수 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다.  
  
 만들기 및 데이터 소스 및 실행 컨텍스트를 사용 하는 방법의 예 참조 드리 면 자습서:
 
 + [데이터 과학에 대 한 심층 정보](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
 +  [RevoScaleR SQL Server 시작](https://msdn.microsoft.com/microsoft-r/rserver/rserver-scaler-sql-server-getting-started)합니다.  
  
## 프로덕션에 R 코드 배포  
 데이터 과학자의 중요한 역할은 분석을 다른 사용자에게 제공하거나 예측 모델을 사용하여 비즈니스 결과 또는 프로세스를 향상시키는 것입니다. R 스크립트 또는 모델이 준비된 경우 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 쉽게 프로덕션으로 이동할 수 있습니다.  
  
 사용자 코드에서 실행 하도록 옮기는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 참조 [R 코드 운용성](../../advanced-analytics/r-services/operationalizing-your-r-code.md)합니다.  
  
 일반적으로 배포 프로세스는 스크립트를 정리하여 프로덕션에서 필요하지 않은 코드를 제거하는 것에서부터 시작됩니다. 데이터에 더 가깝게 계산을 이동 하면 알게 될 것 보다 효율적으로 이동 하 고, 요약 하면, 또는, R.의 모든 기능을 수행할 때 보다 데이터를 제공 하는 방법  
  
 데이터 과학자 문의 성능을 향상 시키는 방법에 대 한 데이터베이스 개발자를 수행 하는 경우에 특히 데이터 정리 또는 기능 하는 엔지니어링 더 효과적일 sql에서 것이 좋습니다. ETL 프로세스에 대 한 변경 내용은 작성 하거나 모델 점수 매기기에 대 한 워크플로 실패 하지 않도록 하 고 입력된 데이터를 올바른 형식에 사용할 수 있는지 필요할 수 있습니다.  
  
##  <a name="bkmk_SQLInR"></a> 섹션 내용  

[ScaleR 함수와 CRAN R 함수 비교](Summary%20of%20rx%20Functions.md)

[SQL Server를 사용 하기 위한 scaleR 기능](../../advanced-analytics/r-services/scaler-functions-for-working-with-sql-server-data.md)
   
## 참고 항목  

 
 [SQL Server R Services 기능 및 태스크](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)   
 
 [작업에서 R 코드 활용](../../advanced-analytics/r-services/operationalizing-your-r-code.md)  
  
  