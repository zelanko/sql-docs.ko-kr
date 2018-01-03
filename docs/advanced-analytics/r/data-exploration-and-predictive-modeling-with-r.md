---
title: "데이터 탐색 및 R을 통한 예측 모델링 | Microsoft 문서"
ms.custom: SQL2016_New_Updated
ms.date: 04/18/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf6de7e2-f394-4b8a-a4b7-0b8dadf25426
caps.latest.revision: "20"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c1586c23850daa679aa6804d946ceb0d0a98ad51
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="data-exploration-and-predictive-modeling-with-r"></a>데이터 탐색 및 R을 통한 예측 모델링

SQL Server와의 통합을 통해 사용할 수 있는 데이터 과학 프로세스에 향상 된 기능에 설명 합니다.

적용 대상: SQL Server 2016 R Services, SQL Server 2017 컴퓨터 Learnign 서비스

## <a name="the-data-science-process"></a>데이터 과학 프로세스

데이터 과학자는 R을 사용하여 데이터를 탐색하고 예상 모델을 작성합니다. 이것은 일반적으로 우수한 예측 모델이 제공될 때까지 반복되는 시행 착오 프로세스입니다. 숙련된 데이터 과학자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 연결한 후 RODBC 패키지를 사용하여 로컬 워크스테이션에 데이터를 패치하며 데이터를 탐색하고 표준 R 패키지를 사용하여 예상 모델을 작성합니다.

그러나이 방법에는 많은 단점이 해당 hae 엔터프라이즈의 R의 광범위 한 채택을 방해 합니다. 

+ 느리거나 비효율적 이며 안전 하지 않은 데이터를 이동 될 수 있습니다.
+ R 자체에 성능 및 확장성 제한이

이러한 단점은 대량의 데이터를 이동 및 분석하거나 데이터 세트가 컴퓨터에서 이용할 수 있는 메모리와 맞지 않는 경우 더 분명하게 나타납니다.

새 하 고 확장 가능한 패키지 및 R 함수에 포함 된 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 이러한 단점을 극복 하는 데 도움이 됩니다. 

## <a name="whats-different-about-revoscaler"></a>RevoScaleR에 대 한 다른 무엇입니까?

**RevoScaleR** 패키지에는 R의 인기 있는 일부 함수가 구현되었고 병렬 처리 및 확장성을 제공하도록 다시 설계되었습니다. 자세한 내용은 참조 [분산 RevoScaleR을 사용 하 여 컴퓨팅](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)합니다.

또한, RevoScaleR 패키지는 *실행 컨텍스트*변경을 지원합니다. 즉, 전체 솔루션 또는 하나의 함수에 대하여 로컬 워크스테이션이 아닌 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 호스팅하는 컴퓨터 리소스를 사용하여 계산이 수행되도록 지정할 수 있습니다. 이러한 방식은 불필요한 데이터 이동을 방지하고 서버 컴퓨터의 더 큰 계산 리소스를 활용할 수 있는 등의 여러 가지 장점이 있습니다.

## <a name="r-environment-and-packages"></a>R 환경 및 패키지

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에서 지원되는 R 환경은 런타임, 오픈 소스 언어 및 여러 패키지에서 지원 및 확장되는 그래픽 엔진으로 구성됩니다. 언어는 패키지를 사용하여 구현되는 다양한 확장을 허용합니다.  

### <a name="using-other-r-packages"></a>다른 R 패키지를 사용 하 여

Microsoft 기계 학습에 포함 된 소유 R 라이브러리 외에도 거의 모든 R 패키지, 솔루션에서 사용할 수 있습니다 포함 하 여:

+ 공용 리포지토리의 일반 용도 R 패키지. CRAN 등과 같은 공용 저장소에서 가장 인기 있는 오픈 소스 R 패키지를 가져올 수 있고 그러한 공용 저장소에는 데이터 과학자가 사용할 수 있는 6,000개 이상의 패키지가 호스팅되어 있습니다.
  
  Windows 플랫폼의 경우 R 패키지는 zip 파일로 제공되고 GPL 라이선스에 따라 다운로드 및 설치될 수 있습니다.  
  
  타사 패키지를 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]와(과) 함께 사용하는 방법에 대한 내용은 [Install Additional R Packages on SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
  
+ 추가 패키지 및 라이브러리는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]이(가) 제공합니다.   
  
     **RevoScaleR** 패키지에는 고성능 빅 데이터 분석, 일반 데이터 과학 작업을 지원하는 향상된 함수 버전, 최적화된 Naive Bayes 학습자, 선형 회귀, 시계열 모델 및 신경망과 고급 수학 라이브러리가 포함됩니다.  
  
     **RevoPemaR** 패키지를 사용하면 R에서 자체 병렬 외부 메모리 알고리즘을 개발할 수 있습니다.  
  
     이러한 패키지 및 사용 하는 방법에 대 한 자세한 내용은 참조 [RevoScaleR 이란](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) 및 [RevoPemaR 시작](https://msdn.microsoft.com/microsoft-r/pemar-getting-started)합니다. 

+ **MicrosoftML** 고도로 최적화 된 기계 학습 알고리즘 및 데이터 변환은 Microsoft 데이터 과학 팀의 컬렉션을 포함 합니다. 다양 한 알고리즘도 Azure 기계 학습에서 사용 됩니다. 자세한 내용은 참조 [MicrosoftML 패키지를 사용 하 여](../../advanced-analytics/using-the-microsoftml-package.md)합니다.

### <a name="r-development-tools"></a>R 개발 도구

R 솔루션을 개발할 때는 Microsoft R Client를 다운로드 해야 합니다. 이 무료 다운로드 하 고 확장 가능한 alorithms 원격 계산 컨텍스트를 지 원하는 데 필요한 라이브러리에 포함 됩니다.

+ **[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]:** 표준 R 작업 성능을 향상하는 패키지 집합(Intel 수학 커널 라이브러리 등) 및 R 런타임 배포입니다.  
  
+ **RevoScaleR:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 계산을 푸시할 수 있게 해주는 R 패키지입니다. [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]이(가) 포함된 R 기능을 사용하여 이러한 단점을 해결할 수 있습니다. 또한 향상된 성능 및 확장성을 제공하도록 다시 설계된 공통 R 함수 세트가 포함되어 있습니다. 이러한 향상된 함수의 이름에는 **rx** 라는 접두사가 사용됩니다. 다양한 원본의 향상된 데이터 공급자도 포함됩니다. 이러한 함수 앞에는 **Rx**가 추가됩니다.

와 같은 R을 지 원하는 모든 Windows 기반 코드 편집기를 사용할 수 있습니다 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 또는 RStudio 합니다. [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)] 다운로드에는 RGui.exe 등과 같은 R의 공통 명령줄 도구도 포함되어 있습니다.

## <a name="use-new-data-sources-and-compute-contexts"></a>사용 하 여 새 데이터 원본 및 계산 컨텍스트

에 연결 하는 RevoScaleR 패키지를 사용 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], R 코드에서 사용 하기 위해 이러한 함수를 찾아보십시오.

+ **RxSqlServerData** 은(는) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이(가) 포함된 R 기능을 사용하여 이러한 단점을 해결할 수 있습니다.
  
     R 코드에서 이 함수를 사용하여 *데이터 원본*을 정의할 수 있습니다. 데이터 원본 개체는 데이터가 있고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 읽고 쓰는 작업을 관리하는 서버와 테이블을 지정합니다.
  
-   **RxInSqlServer** 함수를 사용하여 *계산 컨텍스트*를 지정할 수 있습니다.  즉, 로컬 워크스테이션 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 호스팅하는 컴퓨터 등 R 코드의 실행 위치를 나타낼 수 있습니다.  자세한 내용은 참조 [RevoScaleR 함수](https://msdn.microsoft.com/microsoft-r/scaler/scaler)합니다.
  
     계산 컨텍스트를 설정하는 경우 원격 실행 컨텍스트를 지원하는 계산, 즉 RevoScaleR 패키지에서 제공하는 R 작업 및 관련 함수에만 영향을 줍니다. 일반적으로 표준 CRAN 패키지를 기반으로 하는 R 솔루션은 원격 계산 컨텍스트에서 실행할 수 없습니다. 단, T-SQL에서 시작된 경우에는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터에서 실행할 수 있습니다. 그러나 `rxExec` 함수를 사용하여 개별 R 함수를 호출하고 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 원격으로 실행할 수 있습니다.

만들기 및 데이터 원본 및 실행 컨텍스트를 사용 하는 방법의 예 이러한 자습서를 참조:

+ [데이터 과학 심층 분석](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)  
+  [Microsoft R를 사용 하 여 데이터 분석](https://msdn.microsoft.com/en-us/microsoft-r/data-analysis-in-microsoft-r)

## <a name="deploy-r-code-to-production"></a>프로덕션 환경에 R 코드 배포

데이터 과학자의 중요한 역할은 분석을 다른 사용자에게 제공하거나 예측 모델을 사용하여 비즈니스 결과 또는 프로세스를 향상시키는 것입니다. R 스크립트 또는 모델이 준비된 경우 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 쉽게 프로덕션으로 이동할 수 있습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 실행하기 위해 사용자 코드를 이동하는 방법에 대한 자세한 내용은 [작업에서 R 코드 활용](../../advanced-analytics/r/operationalizing-your-r-code.md)을 참조하세요.

일반적으로 배포 프로세스는 스크립트를 정리하여 프로덕션에서 필요하지 않은 코드를 제거하는 것에서부터 시작됩니다. 계산에 가깝게 데이터를 이동 하면 알게 될 수 있습니다 더 효율적으로 이동, 요약 또는 보다 R에서 모든 항목을 수행 하는 데이터를 제공 하는 방법  성능을 향상 시키는 방법에 대 한 데이터베이스 개발자와 상의 하는 데이터 과학자,이 솔루션은 경우에 특히 데이터 정리 또는 엔지니어링 하는 기능 더 효과적일 sql에서 것이 좋습니다. 모델 작성 또는 점수 매기기 워크플로가 실패하지 않고 입력 데이터를 올바른 형식으로 사용할 수 있도록 ETL 프로세스를 변경해야 할 수도 있습니다.

## <a name="see-also"></a>관련 항목:

[기본 R 및 ScaleR 함수 비교](https://msdn.microsoft.com/microsoft-r/scaler/compare-base-r-scaler-functions)

[SQL Server를 사용하기 위한 ScaleR 함수](../../advanced-analytics/r/scaler-functions-for-working-with-sql-server-data.md)
