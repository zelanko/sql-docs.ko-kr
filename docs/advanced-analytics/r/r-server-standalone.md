---
title: SQL Server의 독립 실행형 R Server 또는 Machine Learning Server 설치 | Microsoft Docs
description: 독립 실행형 R 서버 개요를 소개 하 고 SQL Server 설치 프로그램에서 Machine Learning Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9cb0cecaef28d512cf36e694344e62b01df88ebf
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51657502"
---
# <a name="r-server-standalone-and-machine-learning-server-standalone-in-sql-server"></a>R Server (독립 실행형) 및 SQL server에서 Machine Learning Server (독립 실행형)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server는 독립 실행형 R Server 또는 SQL Server와 독립적으로 실행하는 Machine Learning Server 설치 지원을 제공합니다. SQL Server 버전에 따라 독립 실행형 서버는 대규모 통계 및 예측 분석 기능을 추가하는 Microsoft 제공 고성능 라이브러리와 함께 오픈 소스 R 및 경우에 따라 Python을 기반으로합니다. 라이브러리는 또한 R 또는 Python으로 스크립팅된 머신 러닝 작업을 가능하게 합니다. 

이 기능은 SQL Server 2016에서 **R Server(독립 실행형)** 라고 하고 R 전용입니다. SQL Server 2017에서는 **Machine Learning Server(독립 실행형)** 라고 하며 R 및 Python 모두를 포함합니다.  

> [!Note]
> SQL Server 설치 프로그램에 의해 설치되는 독립 실행형 서버는 Microsoft SQL Server 브랜드 버전이 아닌 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)와 기능적으로 동일하며 원격 실행, 조작화 및 웹 서비스, R 및 Python 라이브러리 전체 컬렉션을 포함하여 동일한 사용자 시나리오를 지원합니다.

## <a name="components"></a>구성 요소

SQL Server 2016은 R만 있습니다. SQL Server 2017은 R과 Python을 지원합니다. 다음 표에 각 버전의 기능을 보여 줍니다.

| 구성 요소 | 설명 |
|-----------|-------------|
| R 패키지 | [**RevoScaleR** ](revoscaler-overview.md) 데이터 조작, 변환, 시각화 및 분석에 대 한 함수를 사용 하 여 확장 가능한 R 주 라이브러리입니다.  <br/>[**MicrosoftML** ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 텍스트 분석, 이미지 분석 및 감정 분석에 대 한 사용자 지정 모델을 만드는 기계 학습 알고리즘을 추가 합니다. <br/>[**sqlRUtils** ](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md) , T-SQL 저장 프로시저에 R 스크립트를 배치 하 고, 데이터베이스와 함께 저장된 프로시저를 등록 하 고, R 개발 환경에서 저장된 프로시저를 실행 하는 것에 대 한 도우미 함수를 제공 합니다.<br/>[**mrsdeploy** ](operationalization-with-mrsdeploy.md) 제품 웹 서비스 배포 (SQL Server 2017에만 해당)에 있습니다. <br/>[**olapR** ](how-to-create-mdx-queries-using-olapr.md) R에서 MDX 쿼리를 지정 하는 데는|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open) 은 Microsoft의 오픈 소스 분산은 R입니다. 패키지 및 인터프리터를 포함 됩니다. 항상 설치 프로그램의 번들 MRO의 버전을 사용 합니다. |
| R 도구 | R 콘솔 창 및 명령 프롬프트를 R 배포에 표준 도구 이며 SQL Server\140\R_SERVER\bin\x64 \Program files\Microsoft에서 찾을 있습니다. |
| R 샘플 및 스크립트 |  오픈 소스 R 및 RevoScaleR 패키지 만들기 및 미리 설치 된 데이터를 사용 하 여 스크립트를 실행할 수 있도록 기본 제공 데이터 집합을 포함 합니다. SQL Server\140\R_SERVER\library\datasets \Program files\Microsoft 및 \library\RevoScaleR에 확인 합니다. |
| Python 패키지 | [**revoscalepy** ](../python/what-is-revoscalepy.md) 데이터 조작, 변환, 시각화 및 분석에 대 한 함수를 사용 하 여 확장 가능한 Python 주 라이브러리입니다. <br/>[**microsoftml** ](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 텍스트 분석, 이미지 분석 및 감정 분석에 대 한 사용자 지정 모델을 만드는 기계 학습 알고리즘을 추가 합니다.  |
| Python 도구 | 기본 제공 Python 명령줄 도구는 임시 테스트 및 작업에 유용 합니다. SQL Server\140\PYTHON_SERVER\python.exe \Program files\Microsoft에서 도구를 찾습니다. |
| Anaconda | Anaconda는 Python 및 필수 패키지를 오픈 소스 배포 됩니다. |
| Python 샘플 및 스크립트 | R에서와 마찬가지로 Python 기본 제공 데이터 집합 및 스크립트를 포함 합니다. Revoscalepy 데이터 \Program files\Microsoft SQL 영문 Server\140\PYTHON_SERVER\lib\site packages\revoscalepy\data\sample 데이터입니다. |
| R 및 Python에서 미리 학습 된 모델 | 미리 학습 된 모델은 특정 사용 사례에 대 한 생성 되 고 microsoft 데이터 과학 엔지니어링 팀에서 유지 관리 합니다. 으로 미리 학습 된 모델을 사용할 수 있습니다-텍스트에서 양수 음수가 감정 점수 매기기 또는 기능에서 제공 하는 새 데이터 입력을 사용 하 여 이미지를 검색 하는 것입니다. 미리 학습 된 모델 지원 되며 독립 실행형 서버에서 사용할 수 있지만 SQL Server 설치 프로그램을 통해 설치할 수 없습니다. 자세한 내용은 [SQL Server에서 기계 학습 모델을 미리 학습 된 설치](../install/sql-pretrained-models-install.md)합니다. |

## <a name="using-a-standalone-server"></a>독립 실행형 서버 사용

R 및 Python 개발자는 일반적으로 독립형 서버를 선택하여 오픈 소스 R 및 Python의 메모리 및 처리 제한을 뛰어넘습니다. 독립 실행형 서버에서 실행되는 R 및 Python 라이브러리는 여러 코어에서 많은 양의 데이터를 로드하고 처리할 수 있으며 결과를 단일 통합 출력으로 집계할 수 있습니다. Microsoft에서 엔지니어링 및 지원하는 상용 서버 제품의 예측 분석, 통계 모델링, 데이터 시각화 및 최첨단 기계 학습 알고리즘을 제공하는 고성능 기능은 확장 및 유틸리티 모두를 위해 설계되었습니다.

SQL Server와 분리된 독립 서버로서, R 및 Python 환경은 SQL Server가 아닌 독립 실행형 서버에서 제공되는 기본 운영 체제 및 표준 도구를 사용하여 구성, 보안 및 액세스됩니다. SQL Server 관계형 데이터에 대한 기본 제공 지원은 없습니다. SQL Server 데이터를 사용하려는 경우 다른 클라이언트에서와 마찬가지로 데이터 원본 개체와 연결을 만들 수 있습니다.

SQL Server의 보조 도구로서 독립 실행형 서버는 로컬 및 원격 컴퓨팅이 모두 필요한 경우 강력한 개발 환경으로 유용합니다. 독립 실행형 서버의 R 및 Python 패키지는 데이터베이스 엔진 설치 시 제공되는 패키지와 동일하므로 코드 이식성 및 [계산 컨텍스트 전환](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)을 제공합니다.

## <a name="how-to-get-started"></a>시작하는 방법

설치 프로그램을 시작한 하 여 즐겨 찾는 개발 도구, 바이너리 연결할 첫 번째 스크립트를 작성 합니다.

### <a name="step-1-install-the-software"></a>1 단계: 소프트웨어를 설치 합니다.

이러한 버전 중 하나를 설치 합니다.

+ [SQL Server 2017 Machine Learning Server (독립 실행형)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (독립 실행형)-R만](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>2 단계: 구성 하는 개발 도구

독립 실행형 서버에서 동일한 컴퓨터에 설치 된 개발을 사용 하 여 로컬 작업에 공통적으로 적용 됩니다.

+ [R 도구 설정](set-up-a-data-science-client.md)
+ [Python 도구 설정](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>3 단계: 첫 번째 스크립트를 작성 합니다.

기계 학습 알고리즘, RevoScaleR 및 revoscalepy를에서 함수를 사용 하 여 R 또는 Python 스크립트를 작성 합니다.
  
  + [Explore R and 알아보기 25 함수에서 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): 기본 R 명령 및 높은 성능을 제공 하는 RevoScaleR 배포 가능한 분석 함수는 진행률 및 R 솔루션에 확장을 다음으로 시작 합니다. K-means 클러스터링, 의사 결정 트리, 의사 결정 포리스트, 데이터 조작 도구 등 가장 많이 사용되는 R 모델링 패키지의 병렬 처리 버전을 포함합니다.

  + [빠른 시작: microsoftml Python 패키지를 사용 하 여 이진 분류 예제](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): microsoftml 및 잘 알려진 breast cancer 데이터 집합에서 함수를 사용 하 여 이진 분류 모델을 만듭니다.

작업을 위한 최상의 언어를 선택 합니다. R은 SQL을 사용 하 여 구현 하기 어려운 통계적 계산에 적합 합니다. 데이터 집합 기반 작업에 대 한의 기능을 활용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 최대 성능을 얻을 수 있습니다. 열에 대해 매우 빠른 계산에 대 한 메모리 내 데이터베이스 엔진을 사용 합니다.

### <a name="step-4-operationalize-your-solution"></a>4 단계: 솔루션 운영 화

독립 실행형 서버를 사용 하는 [운영 화](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) 기능을 SQL-브랜딩되지 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)합니다. 이러한 혜택을 제공 하는 운영 화를 위한 독립 실행형 서버를 구성할 수 있습니다: 배포 및 웹 서비스 용량을 테스트 하는 웹 서비스에서 진단을 실행 하는 대로 코드를 호스트 합니다.

## <a name="see-also"></a>참고자료

 [R Server (독립 실행형) 또는 Machine Learning Server (독립 실행형) 설치](../install/sql-machine-learning-standalone-windows-install.md)

