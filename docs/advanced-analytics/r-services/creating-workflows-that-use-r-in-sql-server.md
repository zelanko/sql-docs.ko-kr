---
title: "SQL Server에서 R을 사용하는 워크플로 만들기 | Microsoft Docs"
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
ms.assetid: 34c3b1c2-97db-4cea-b287-c7f4fe4ecc1b
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# SQL Server에서 R을 사용하는 워크플로 만들기
  관계형 데이터베이스는 트랜잭션 처리, 저장소 및 쿼리 하는 데이터에 대 한 확장성이 뛰어난 솔루션을 제공 하는 고도로 최적화 된 기술입니다. 그러나 일반적으로 R 솔루션 일반적으로 사용 했었다면 CSV 형식으로 추가 데이터 탐색 및 모델링을 수행 하려면 대개에 다양 한 원본에서 데이터 가져오기. 그러한 작업은 비효율적일 뿐만 아니라 안전하지 않습니다.  
  
 사용 하 여 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 여러 이점을 제공 합니다.  
  
-   데이터 보안 합니다. 데이터베이스에 의해의 R의 데이터 원본에 더 가깝게 합니다. 낭비 나 안전 하지 않은 데이터 이동을 발생 하지 않습니다.  
  
-   속도입니다. 데이터베이스 집합 기반 작업을 위해 최적화 됩니다. 또한 데이터베이스의 최근 혁신 메모리 내 테이블 및 열 데이터 저장소 추가 같은 데이터 과학 함으로써 향상 빠른 번개 집계 합니다.  
  
-   통합 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다른 여러 데이터 관리 작업 및 엔터프라이즈를 사용 하는 응용 프로그램에 대 한 작업의 중앙 지점이입니다. 데이터베이스에 데이터를 이미 사용 하는 데이터가 일관 되 고 최신 되도록 합니다. R의 데이터를 처리 하는 대신 포함 하 여 엔터프라이즈 데이터 파이프라인에 의존할 수 있습니다 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 Azure 데이터 팩터리입니다. Power BI를 통해 쉽습니다 결과 또는 분석 등의 보고 또는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]합니다.  
  
 다양한 데이터 처리 및 분석 작업에 SQL과 R을 적절하게 조합하여 사용하면 데이터 과학자와 개발자가 모두 생산성을 높일 수 있습니다. 이 섹션에서는 데이터 변환, 분석, 보고를 위해 R을 다른 엔터프라이즈 솔루션과 통합하는 방법을 설명합니다.  
  
##  <a name="bkmk_ssis"></a> R과 데이터베이스를 포괄하는 효율적인 워크플로 만들기  
 데이터 과학 워크플로는 반복이 매우 빈번하며, 크기 조정, 집계, 확률 계산, 특성 병합 및 이름 변경을 비롯한 데이터 변환이 많이 이루어집니다. 데이터 과학자는 R, Python, 또는 다른 언어입니다; 이러한 작업의 대부분 작업을 수행 하는 데 익숙합니다. 그러나 엔터프라이즈 데이터에 대해 이러한 워크플로 실행 하려면 ETL 도구 및 프로세스와 원활 하 게 통합 합니다.  
  
 때문에 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] TRANSACT-SQL 및 저장된 프로시저를 통해 R의 복잡 한 작업을 실행할 수 있도록 다시 개발 최소한의 작업 없이 기존 ETL 프로세스와 R 관련 작업을 통합할 수 있습니다. 대신 메모리 ntensive 작업의 체인에 R을 수행 하는 보다 데이터 준비를 최적화할 수 있는 포함 하는 가장 효율적인 도구를 사용 하 여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다.  
  
 예를 들어 있는 R를 결합할 수 있습니다 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 같은 시나리오에서:  
  
-   사용 하 여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 작업을 SQL 데이터베이스에 필요한 개체를 만듭니다.  
  
-   조건부 분기를 사용하여 R 작업에 대한 계산 컨텍스트 전환  
  
-   자체 데이터를 생성하는 R 작업 실행  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을(를) 사용하여 텍스트 변수로 저장된 R 스크립트 호출  
  
### 샘플 및 리소스  
 [SQL Server 2016 SSIS 및 R 서비스를 사용 하 여 기계 학습 프로젝트를 운영 합니다.](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  
  
 이 블로그 게시물에서는 설명 하는 방법:  
  
-   SQL 실행 태스크에서 R을 사용 하 여 데이터를 생성 하 고에 저장 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   R 모델을 학습 하 고 데이터베이스에 저장 하려면 저장된 프로시저를 사용 합니다.  
  
-   스크립트 태스크와 SQL 실행 태스크를 사용 하 여 모델에 점수 매기기를 수행 합니다.  
  
##  <a name="bkmk_ssrs"></a> R과 엔터프라이즈 보고 도구를 포괄하는 시각화 만들기  
 R로 차트와 흥미로운 시각화를 만들 수 있지만, 외부 데이터 원본과 잘 통합되지 않기 때문에 각 차트와 그래프를 개별적으로 생성해야 합니다. 공유도 어려울 수 있습니다.  
  
 사용 하 여 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 를 통해 R의 복잡 한 작업을 실행할 수 있습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저, 다양 한 엔터프라이즈 보고 도구를 포함 하 여 쉽게 사용할 수 있는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 및 Power BI 합니다.  
  
-   R 스크립트에서 반환 된 그래픽 개체를 시각화 합니다.   
    사용 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   Power BI에서 테이블을 사용 합니다.  
  
## 샘플 및 리소스  
 [Microsoft Reporting Services (SSRS)에 대 한 R 그래픽 장치](https://rgraphicsdevice.codeplex.com/)  
  
 CodePlex 프로젝트를 제공 하는 사용자 지정 보고서 항목을 만드는 데 도움이 되는 코드에서 사용할 수 있는 이미지 형식으로 R의 그래픽 출력을 렌더링 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서입니다.  사용자 지정 보고서 항목을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   차트 및 플롯 R 그래픽 장치를 사용 하 여 만든 게시 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 대시보드  
  
-   전달 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] R 플롯 하는 매개 변수  
  
> [!NOTE]  
>  참고 하에 물론 Visual Studio의 Reporting Services 서버에 Reporting Services에 대 한 R 그래픽 장치를 지 원하는 코드를 설치 해야 합니다. 수동 컴파일 및 구성은도 필요 합니다.  
  
  