---
title: "데이터 과학 종단 간 연습 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
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
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# 데이터 과학 종단 간 연습
이 연습에서는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 사용하여 예측 모델링을 위한 종단 간 솔루션을 개발합니다.  
  
이 연습은 잘 알려진 공용 데이터 집합인 뉴욕 시 택시 데이터 집합을 기반으로 합니다. R 코드, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 및 사용자 지정 SQL 함수의 조합을 사용하여 기사가 특정 택시 여정에 대한 팁을 얻을 확률을 나타내는 분류 모델을 작성합니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 R 모델을 배포하고 서버 데이터를 사용하여 모델을 기준으로 점수를 생성합니다.  
  
이 예제는 판매 캠페인에 대한 고객 응답 예측, 이벤트 방문자의 지출 예측 등 모든 종류의 현실적인 문제로 쉽게 확장할 수 있습니다. 저장 프로시저에서 모델을 호출할 수 있으므로 응용 프로그램에 쉽게 포함할 수도 있습니다.  
  
**대상 사용자**  
  
이 연습은 R 개발자를 위해 작성되었습니다. 데이터베이스 만들기, 테이블 만들기, 테이블로 데이터 가져오기, [!INCLUDE[tsql](../../includes/tsql-md.md)]사용하여 테이블 쿼리 등의 기본적인 데이터베이스 작업도 알고 있어야 합니다.  실행할 SQL 및 R 스크립트가 제공됩니다.  
  
R을 처음 사용하지만 데이터베이스를 잘 알고 있는 경우 이 자습서에서 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 사용하여 엔터프라이즈 워크플로에 R을 통합하는 방법을 설명합니다. R 코딩은 필요하지 않으며 모든 스크립트가 제공됩니다. 명령을 실행하려면 종류에 관계없이 R IDE가 설치되어 있어야 합니다.  
  
**필수 구성 요소**  
  
이 자습서를 수행하려면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이 설치되어 있는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 인스턴스에 액세스할 수 있어야 합니다. 로컬 환경에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있는 데이터 과학 워크스테이션을 준비한 다음 필요한 R 라이브러리를 설치합니다.  
  
자세한 내용은 [데이터 과학 연습의 필수 조건&#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/prerequisites-for-data-science-walkthroughs-sql-server-r-services.md)을 참조하세요.  
  
## <a name="overview"></a>개요  
이 연습에서는 고급 분석을 위한 일반적인 종단 간 솔루션을 보여 줍니다. 단원을 순서대로 완료해야 합니다.  
  
||소요되는 예상 시간|  
|-|------------------------------|  
|[1단원: 데이터 준비&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)<br /><br />분석 프로세스는 모델 작성에 사용되는 데이터를 가져오는 것으로 시작합니다. 공용 데이터 집합을 다운로드하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장합니다.|30분|  
|[2단원: 데이터 보기 및 탐색&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)<br /><br />데이터 과학자는 대개 데이터를 탐색하고 모델링을 준비하거나, 새로운 기능을 만들거나, 필요에 따라 데이터를 변환하는 데 상당한 시간을 소비합니다.  SQL 및 R을 함께 사용하여 데이터를 탐색하고 요약을 생성합니다.|20분|  
|[3단원: 데이터 기능 만들기&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)<br /><br />R과 [!INCLUDE[tsql](../../includes/tsql-md.md)]사용자 지정 함수를 사용하여 새로운 데이터 기능을 만듭니다.|10분|  
|[4단원: 모델 작성 및 저장&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)<br /><br />데이터가 준비되면 데이터 과학자는 성능을 평가하고 다양한 매개 변수를 시도하여 모델을 학습 및 조정합니다. 이 연습에서는 분류 모델을 만들고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 데이터를 사용하여 예측을 생성합니다. 또한 R을 사용하여 모델의 정확도를 그립니다.|15분|  
|[5단원: 모델 배포 및 사용&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough.md)<br /><br />최종적으로, 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장하여 프로덕션에 모델을 배포하고 저장 프로시저에서 모델을 호출하여 예측을 생성합니다.|10분|  
  
## <a name="notes"></a>참고  
이 연습은 R 개발자에게 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 소개하기 위해 작성되었으므로 R을 사용하여 최대한 많은 작업을 수행합니다. R이 각 작업에 가장 적합한 도구인 것은 아닙니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 대부분의 경우, 특히 데이터 집계, 기능 엔지니어링 등의 작업에서 더 나은 성능을 제공할 수 있습니다. 이러한 작업은 메모리 액세스에 최적화된 columnstore 인덱스 등 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 새로운 기능을 활용할 수 있습니다.  
  
## <a name="next-step"></a>다음 단계  
[1단원: 데이터 준비&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
