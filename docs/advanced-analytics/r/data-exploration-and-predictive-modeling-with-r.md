---
title: R을 사용 하 여 데이터 탐색 및 예측 모델링
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 7cdd1e6dbb0438c1eb3d7404bc0aed672d088206
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470194"
---
# <a name="data-exploration-and-predictive-modeling-with-r-in-sql-server"></a>SQL Server에서 R을 사용 하 여 데이터 탐색 및 예측 모델링
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 SQL Server와의 통합을 통해 가능한 데이터 과학 프로세스에 대 한 향상 된 기능을 설명 합니다.

적용 대상: SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services

## <a name="the-data-science-process"></a>데이터 과학 프로세스

데이터 과학자는 R을 사용하여 데이터를 탐색하고 예상 모델을 작성합니다. 이것은 일반적으로 우수한 예측 모델이 제공될 때까지 반복되는 시행 착오 프로세스입니다. 숙련된 데이터 과학자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 연결한 후 RODBC 패키지를 사용하여 로컬 워크스테이션에 데이터를 패치하며 데이터를 탐색하고 표준 R 패키지를 사용하여 예상 모델을 작성합니다.

그러나이 방법에는 기업에서 R을 광범위 하 게 채택 하는 저하 hae 많은 단점이 있습니다. 

+ 데이터 이동이 느리거나 비효율적 이거나 안전 하지 않을 수 있습니다.
+ R 자체에는 성능 및 확장 제한이 있습니다.

이러한 단점은 많은 양의 데이터를 이동 하 고 분석 해야 하거나 컴퓨터에서 사용할 수 있는 메모리에 맞지 않는 데이터 집합을 사용 해야 하는 경우 더 분명 하 게 드러납니다.

에 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 포함 된 새로운 확장 가능한 패키지 및 R 함수를 통해 이러한 많은 문제를 해결할 수 있습니다. 

## <a name="whats-different-about-revoscaler"></a>RevoScaleR에 대 한 다른 사항은 무엇 인가요?

**RevoScaleR** 패키지에는 R의 인기 있는 일부 함수가 구현되었고 병렬 처리 및 확장성을 제공하도록 다시 설계되었습니다. 자세한 내용은 [RevoScaleR를 사용 하 여 분산 컴퓨팅](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)을 참조 하세요.

또한, RevoScaleR 패키지는 *실행 컨텍스트*변경을 지원합니다. 즉, 전체 솔루션 또는 하나의 함수에 대하여 로컬 워크스테이션이 아닌 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 호스팅하는 컴퓨터 리소스를 사용하여 계산이 수행되도록 지정할 수 있습니다. 이러한 방식은 불필요한 데이터 이동을 방지하고 서버 컴퓨터의 더 큰 계산 리소스를 활용할 수 있는 등의 여러 가지 장점이 있습니다.

## <a name="r-environment-and-packages"></a>R 환경 및 패키지

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에서 지원되는 R 환경은 런타임, 오픈 소스 언어 및 여러 패키지에서 지원 및 확장되는 그래픽 엔진으로 구성됩니다. 언어는 패키지를 사용하여 구현되는 다양한 확장을 허용합니다.  

### <a name="using-other-r-packages"></a>다른 R 패키지 사용

Microsoft Machine Learning에 포함 된 독점적인 R 라이브러리 외에도 다음을 포함 하 여 솔루션에서 거의 모든 R 패키지를 사용할 수 있습니다.

+ 공용 리포지토리의 일반 용도 R 패키지. CRAN 등과 같은 공용 저장소에서 가장 인기 있는 오픈 소스 R 패키지를 가져올 수 있고 그러한 공용 저장소에는 데이터 과학자가 사용할 수 있는 6,000개 이상의 패키지가 호스팅되어 있습니다.
  
  Windows 플랫폼의 경우 R 패키지는 zip 파일로 제공되고 GPL 라이선스에 따라 다운로드 및 설치될 수 있습니다.  
  
  타사 패키지를 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]와(과) 함께 사용하는 방법에 대한 내용은 [Install Additional R Packages on SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
  
+ 추가 패키지 및 라이브러리는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]이(가) 제공합니다.   
  
     **RevoScaleR** 패키지에는 고성능 빅 데이터 분석, 일반 데이터 과학 작업을 지원하는 향상된 함수 버전, 최적화된 Naive Bayes 학습자, 선형 회귀, 시계열 모델 및 신경망과 고급 수학 라이브러리가 포함됩니다.  
  
     **RevoPemaR** 패키지를 사용하면 R에서 자체 병렬 외부 메모리 알고리즘을 개발할 수 있습니다.  
  
     이러한 패키지 및 사용 방법에 대 한 자세한 내용은 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler) 를 참조 하 고 [RevoPemaR 시작](https://docs.microsoft.com/machine-learning-server/r/how-to-developer-pemar)하기를 참조 하세요. 

+ **MicrosoftML** 에는 Microsoft 데이터 과학 팀의 데이터 변환과 최적화 된 기계 학습 알고리즘의 컬렉션이 포함 되어 있습니다. 대부분의 알고리즘은 Azure Machine Learning 에서도 사용 됩니다. 자세한 내용은 [MicrosoftML in SQL Server](ref-r-microsoftml.md)항목을 참조 하세요.

### <a name="r-development-tools"></a>R 개발 도구

R 솔루션을 개발 하는 경우 Microsoft R Client를 다운로드 해야 합니다. 이 무료 다운로드에는 원격 계산 컨텍스트 및 확장 가능한 alorithms을 지 원하는 데 필요한 라이브러리가 포함 됩니다.

+ **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** 표준 R 작업의 성능을 향상 시키는 R 런타임 및 패키지 집합 (예: Intel math kernel library)을 배포 합니다.  
  
+ **RevoScaleR:** 인스턴스에 계산을 푸시할 수 있도록 하는 R 패키지입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]에서 분할된 테이블 또는 인덱스를 만들 수 있습니다. 또한 향상된 성능 및 확장성을 제공하도록 다시 설계된 공통 R 함수 세트가 포함되어 있습니다. 이러한 향상된 함수의 이름에는 **rx** 라는 접두사가 사용됩니다. 다양한 원본의 향상된 데이터 공급자도 포함됩니다. 이러한 함수 앞에는 **Rx**가 추가됩니다.

또는 rstudio와 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 같은 R을 지 원하는 모든 Windows 기반 코드 편집기를 사용할 수 있습니다. [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] 다운로드에는 RGui.exe 등과 같은 R의 공통 명령줄 도구도 포함되어 있습니다.

## <a name="use-new-data-sources-and-compute-contexts"></a>새 데이터 원본 및 계산 컨텍스트 사용

RevoScaleR 패키지를 사용 하 여에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결 하는 경우 R 코드에서 사용할 함수를 찾습니다.

+ **RxSqlServerData** 은(는) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이(가) 포함된 R 기능을 사용하여 이러한 단점을 해결할 수 있습니다.
  
     R 코드에서 이 함수를 사용하여 *데이터 원본*을 정의할 수 있습니다. 데이터 원본 개체는 데이터가 있고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 읽고 쓰는 작업을 관리하는 서버와 테이블을 지정합니다.
  
-   **RxInSqlServer** 함수를 사용하여 *계산 컨텍스트*를 지정할 수 있습니다.  즉, 로컬 워크스테이션 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 호스팅하는 컴퓨터 등 R 코드의 실행 위치를 나타낼 수 있습니다.  자세한 내용은 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)를 참조 하세요.
  
     컴퓨팅 컨텍스트를 설정하는 경우 원격 실행 컨텍스트를 지원하는 컴퓨팅, 즉 RevoScaleR 패키지에서 제공하는 R 작업 및 관련 함수에만 영향을 줍니다. 일반적으로 표준 CRAN 패키지를 기반으로 하는 R 솔루션은 원격 컴퓨팅 컨텍스트에서 실행할 수 없습니다. 단, T-SQL에서 시작된 경우에는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터에서 실행할 수 있습니다. 그러나 `rxExec` 함수를 사용하여 개별 R 함수를 호출하고 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 원격으로 실행할 수 있습니다.

데이터 원본 및 실행 컨텍스트를 만들고 사용 하는 방법에 대 한 예는 다음 자습서를 참조 하세요.

+ [데이터 과학 심층 분석](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)  
+  [Microsoft R을 사용 하 여 데이터 분석](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)

## <a name="deploy-r-code-to-production"></a>프로덕션에 R 코드 배포

데이터 과학자의 중요한 역할은 분석을 다른 사용자에게 제공하거나 예측 모델을 사용하여 비즈니스 결과 또는 프로세스를 향상시키는 것입니다. R 스크립트 또는 모델이 준비된 경우 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 쉽게 프로덕션으로 이동할 수 있습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행하기 위해 사용자 코드를 이동하는 방법에 대한 자세한 내용은 [작업에서 R 코드 활용](../../advanced-analytics/r/operationalizing-your-r-code.md)을 참조하세요.

일반적으로 배포 프로세스는 스크립트를 정리하여 프로덕션에서 필요하지 않은 코드를 제거하는 것에서부터 시작됩니다. 계산을 데이터에 더 가깝게 이동할 때 R의 모든 작업을 수행 하는 것 보다 더 효율적으로 데이터를 이동, 요약 또는 제공 하는 방법을 찾을 수 있습니다.  데이터 과학자는 성능 향상을 위해 데이터베이스 개발자에 게 문의 하는 것이 좋습니다. 특히 솔루션이 SQL에서 더 효과적일 수 있는 데이터 정리 또는 기능 엔지니어링을 수행 하는 경우에 해당 합니다. 모델 작성 또는 점수 매기기 워크플로가 실패하지 않고 입력 데이터를 올바른 형식으로 사용할 수 있도록 ETL 프로세스를 변경해야 할 수도 있습니다.

## <a name="see-also"></a>관련 항목

[Base R 및 RevoScaleR 함수 비교](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)

[SQL Server의 RevoScaleR 라이브러리](ref-r-revoscaler.md)
