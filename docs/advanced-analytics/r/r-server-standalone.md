---
title: 독립 실행형 R Server 또는 Machine Learning Server 설치
description: 개요 SQL Server 설치 프로그램에서 독립 실행형 R 서버 및 Machine Learning Server 소개
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/18/2018
ms.topic: overview
author: dphansen
ms.author: davidph
ms.openlocfilehash: 84ef5d684e767016491baa6e47e37d1402fc6879
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470043"
---
# <a name="r-server-standalone-and-machine-learning-server-standalone-in-sql-server"></a>SQL Server에서 R Server (독립 실행형) 및 Machine Learning Server (독립 실행형)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server는 독립 실행형 R Server 또는 SQL Server와 독립적으로 실행하는 Machine Learning Server 설치 지원을 제공합니다. SQL Server 버전에 따라 독립 실행형 서버는 대규모 통계 및 예측 분석 기능을 추가하는 Microsoft 제공 고성능 라이브러리와 함께 오픈 소스 R 및 경우에 따라 Python을 기반으로합니다. 라이브러리는 또한 R 또는 Python으로 스크립팅된 머신 러닝 작업을 가능하게 합니다. 

이 기능은 SQL Server 2016에서 **R Server(독립 실행형)** 라고 하고 R 전용입니다. SQL Server 2017에서는 **Machine Learning Server(독립 실행형)** 라고 하며 R 및 Python 모두를 포함합니다.  

> [!Note]
> SQL Server 설치 프로그램에 의해 설치되는 독립 실행형 서버는 Microsoft SQL Server 브랜드 버전이 아닌 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)와 기능적으로 동일하며 원격 실행, 조작화 및 웹 서비스, R 및 Python 라이브러리 전체 컬렉션을 포함하여 동일한 사용자 시나리오를 지원합니다.

## <a name="components"></a>구성 요소

SQL Server 2016은 R 전용입니다. SQL Server 2017은 R과 Python을 지원합니다. 다음 표에서는 각 버전의 기능을 설명 합니다.

| 구성 요소 | 설명 |
|-----------|-------------|
| R 패키지 | [**RevoScaleR**](ref-r-revoscaler.md) 는 데이터 조작, 변환, 시각화 및 분석을 위한 함수를 사용 하는 확장 가능한 R의 기본 라이브러리입니다.  <br/>[**MicrosoftML**](ref-r-microsoftml.md) 는 기계 학습 알고리즘을 추가 하 여 텍스트 분석, 이미지 분석 및 감정 분석을 위한 사용자 지정 모델을 만듭니다. <br/>[**sqlRUtils**](ref-r-sqlrutils.md)는 T-SQL 저장 프로시저에 R 스크립트를 배치하고, 데이터베이스에 저장 프로시저를 등록하고, R 개발 환경에서 저장 프로시저를 실행하는 것에 대한 도우미 함수를 제공합니다.<br/>[**mrsdeploy**](operationalization-with-mrsdeploy.md) 는 웹 서비스 배포 (SQL Server 2017에만 해당)를 제공 합니다. <br/>[**Olapr**](ref-r-olapr.md) 는 R에서 MDX 쿼리를 지정 하는 데 사용할 수 있습니다.|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open)은 R의 Microsoft의 오픈 소스 배포입니다. 패키지 및 인터프리터를 포함합니다. 설치 프로그램에서 번들 버전을 항상 사용 합니다. |
| R 도구 | R 콘솔 창 및 명령 프롬프트는 R 배포의 표준 도구입니다. Files\Microsoft SQL Server\140\R_SERVER\bin\x64.에서 찾을 수 있습니다. |
| R 샘플 및 스크립트 |  오픈 소스 R 및 RevoScaleR 패키지에는 미리 설치 된 데이터를 사용 하 여 스크립트를 만들고 실행할 수 있도록 기본 제공 데이터 집합이 포함 되어 있습니다. Files\Microsoft SQL Server\140\R_SERVER\library\datasets 및 \library\RevoScaleR.에서 해당 파일을 찾습니다. |
| Python 패키지 | [**revoscalepy**](../python/ref-py-revoscalepy.md) 는 데이터 조작, 변환, 시각화 및 분석을 위한 함수를 사용 하는 확장 가능한 Python의 기본 라이브러리입니다. <br/>[**microsoftml**](../python/ref-py-microsoftml.md) 는 기계 학습 알고리즘을 추가 하 여 텍스트 분석, 이미지 분석 및 감정 분석을 위한 사용자 지정 모델을 만듭니다.  |
| Python 도구 | 기본 제공 Python 명령줄 도구는 임시 테스트 및 작업에 유용 합니다. Files\Microsoft SQL Server\140\PYTHON_SERVER\python.exe.에서 도구 찾기 |
| Anaconda | Anaconda는 Python 및 필수 패키지의 오픈 소스 배포입니다. |
| Python 샘플 및 스크립트 | R과 마찬가지로 Python에는 기본 제공 데이터 집합 및 스크립트가 포함 됩니다. Revoscalepy 데이터는 files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data.에서 찾을 것입니다. |
| R 및 Python의 미리 학습 된 모델 | 미리 학습 된 모델은 특정 사용 사례에 대해 만들어지며 Microsoft의 데이터 과학 엔지니어링 팀에서 유지 관리 합니다. 미리 학습 된 모델을 그대로 사용 하 여 긍정 부정 감정 텍스트의 점수를 매기 거 나 제공 된 새 데이터 입력을 사용 하 여 이미지의 기능을 검색할 수 있습니다. 사전 학습 된 모델은 독립 실행형 서버에서 지원 되 고 사용할 수 있지만 SQL Server 설치를 통해 설치할 수는 없습니다. 자세한 내용은 [SQL Server에 미리 학습 된 된 기계 학습 모델 설치](../install/sql-pretrained-models-install.md)를 참조 하세요. |

## <a name="using-a-standalone-server"></a>독립 실행형 서버 사용

R 및 Python 개발자는 일반적으로 독립형 서버를 선택하여 오픈 소스 R 및 Python의 메모리 및 처리 제한을 뛰어넘습니다. 독립 실행형 서버에서 실행되는 R 및 Python 라이브러리는 여러 코어에서 많은 양의 데이터를 로드하고 처리할 수 있으며 결과를 단일 통합 출력으로 집계할 수 있습니다. Microsoft에서 엔지니어링 및 지원하는 상용 서버 제품의 예측 분석, 통계 모델링, 데이터 시각화 및 최첨단 기계 학습 알고리즘을 제공하는 고성능 기능은 확장 및 유틸리티 모두를 위해 설계되었습니다.

SQL Server와 분리된 독립 서버로서, R 및 Python 환경은 SQL Server가 아닌 독립 실행형 서버에서 제공되는 기본 운영 체제 및 표준 도구를 사용하여 구성, 보안 및 액세스됩니다. SQL Server 관계형 데이터에 대한 기본 제공 지원은 없습니다. SQL Server 데이터를 사용하려는 경우 다른 클라이언트에서와 마찬가지로 데이터 원본 개체와 연결을 만들 수 있습니다.

SQL Server의 보조 도구로서 독립 실행형 서버는 로컬 및 원격 컴퓨팅이 모두 필요한 경우 강력한 개발 환경으로 유용합니다. 독립 실행형 서버의 R 및 Python 패키지는 데이터베이스 엔진 설치 시 제공되는 패키지와 동일하므로 코드 이식성 및 [계산 컨텍스트 전환](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)을 제공합니다.

## <a name="how-to-get-started"></a>시작하는 방법

설치 프로그램을 시작 하 고, 선호 하는 개발 도구에 이진 파일을 연결 하 고, 첫 번째 스크립트를 작성 합니다.

### <a name="step-1-install-the-software"></a>1단계: 소프트웨어 설치

다음 버전 중 하나를 설치 합니다.

+ [SQL Server 2017 Machine Learning Server (독립 실행형)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R 서버 (독립 실행형)-R만](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>2단계: 개발 도구 구성

독립 실행형 서버에서는 일반적으로 동일한 컴퓨터에 설치 된 개발을 사용 하 여 로컬에서 작업을 수행 하는 것이 일반적입니다.

+ [R 도구 설정](set-up-a-data-science-client.md)
+ [Python 도구 설정](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>3단계: 첫 번째 스크립트 작성

RevoScaleR, revoscalepy 및 기계 학습 알고리즘의 함수를 사용 하 여 R 또는 Python 스크립트를 작성 합니다.
  
  + [25 개 함수에서 R 및 RevoScaleR 살펴보기](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): 기본 R 명령으로 시작한 다음, R 솔루션에 고성능 및 크기 조정을 제공 하는 RevoScaleR 배포 가능한 분석 함수를 진행 합니다. K-means 클러스터링, 의사 결정 트리, 의사 결정 포리스트, 데이터 조작 도구 등 가장 많이 사용되는 R 모델링 패키지의 병렬 처리 버전을 포함합니다.

  + [빠른 시작: Microsoftml Python 패키지](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml)를 사용 하는 이진 분류의 예는 다음과 같습니다. Microsoftml의 함수 및 잘 알려진 유방암 암 데이터 집합을 사용 하 여 이진 분류 모델을 만듭니다.

작업에 가장 적합한 언어를 선택하십시오. R은 SQL을 사용하여 구현하기 어려운 통계 계산에 가장 적합합니다. 데이터에 대 한 집합 기반 작업의 경우의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 활용 하 여 성능을 극대화 합니다. 열에 대한 매우 빠른 계산을 위해 메모리 내 데이터베이스 엔진을 사용하십시오.

### <a name="step-4-operationalize-your-solution"></a>4단계: 솔루션 운영

독립 실행형 서버는 SQL 브랜드가 아닌 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)의 [운영 화](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) 기능을 사용할 수 있습니다. 운영 화에 대 한 독립 실행형 서버를 구성할 수 있습니다 .이를 통해 코드를 웹 서비스로 배포 및 호스팅하고 진단, 테스트 웹 서비스 용량을 테스트 합니다.

### <a name="step-5-maintain-your-server"></a>5단계: 서버 유지 관리

SQL Server은 정기적으로 누적 업데이트를 해제 합니다. 누적 업데이트를 적용 하면 기존 설치에 대 한 보안 및 기능 향상 기능이 추가 됩니다. 

새 기능 또는 변경 된 기능에 대 한 설명은 [CAB 다운로드](../install/sql-ml-cab-downloads.md) 문서와 [SQL Server 2016 누적 업데이트](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions) 및 [SQL Server 2017 누적 업데이트](https://support.microsoft.com/help/4047329)에 대 한 웹 페이지에서 찾을 수 있습니다. 

기존 인스턴스에 업데이트를 적용 하는 방법에 대 한 자세한 내용은 설치 지침의 [업데이트 적용](../install/sql-machine-learning-standalone-windows-install.md#apply-cu) 을 참조 하세요.

## <a name="see-also"></a>참조

 [R Server (독립 실행형) 또는 Machine Learning Server (독립 실행형) 설치](../install/sql-machine-learning-standalone-windows-install.md)

