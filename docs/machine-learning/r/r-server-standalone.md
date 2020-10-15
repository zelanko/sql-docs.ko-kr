---
title: 독립 실행형 Machine Learning Server 또는 R Server란?
description: SQL Server 설치 프로그램에서 독립 실행형 R Server와 Machine Learning Server 간의 차이점을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/13/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 342c9bd2f83fed2b74cbce1f5ea7b7d942e9fd63
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956914"
---
# <a name="what-are-standalone-machine-learning-server-or-r-server-in-sql-server"></a>SQL Server의 독립 실행형 Machine Learning Server 또는 R Server란?
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

SQL Server는 SQL Server와 독립적으로 실행되는 독립 실행형 R Server 또는 Machine Learning Server의 설치를 지원합니다. SQL Server 버전에 따라 독립 실행형 서버는 대규모의 통계 및 예측 분석을 추가하는 Microsoft의 고성능 라이브러리와 함께 오픈 소스 R 및 경우에 따라 Python의 기반을 제공합니다. 라이브러리를 사용하여 R 또는 Python에서 기계 학습 작업을 스크립팅할 수도 있습니다. 

SQL Server 2016에서는 이 기능을 **R Server(독립 실행형)** 라고 하며 R 전용입니다. SQL Server 2017에서는 **Machine Learning Server(독립 실행형)** 라고 하며 R과 Python을 모두 포함하고 있습니다.  

> [!Note]
> SQL Server 설치 프로그램을 통해 설치되는 독립 실행형 서버는 SQL 브랜드가 아닌 버전의 [Microsoft Machine Learning Server](/machine-learning-server/what-is-machine-learning-server)와 기능적으로 동일합니다. 즉, 원격 실행, 운영 및 웹 서비스, R 및 Python 라이브러리의 전체 컬렉션을 포함하여 동일한 사용자 시나리오를 지원합니다.

## <a name="components"></a>구성 요소

SQL Server 2016은 R 전용입니다. SQL Server 2017은 R과 Python을 지원합니다. 다음 표에서는 각 버전의 기능을 설명합니다.

| 구성 요소 | Description |
|-----------|-------------|
| R 패키지 | [**RevoScaleR**](ref-r-revoscaler.md)은 데이터 조작, 변환, 시각화 및 분석 기능을 제공하는 확장 가능한 R의 기본 라이브러리입니다.  <br/>[**MicrosoftML**](ref-r-microsoftml.md)은 텍스트 분석, 이미지 분석 및 감정 분석을 위한 사용자 지정 모델을 만들기 위한 기계 학습 알고리즘을 추가합니다. <br/>[**sqlRUtils**](ref-r-sqlrutils.md)는 R 스크립트를 T-SQL 저장 프로시저에 배치하고, 저장 프로시저를 데이터베이스에 등록하고, R 개발 환경에서 저장 프로시저를 실행할 수 있는 도우미 함수를 제공합니다.<br/>[**olapR**](ref-r-olapr.md)은 R에서 MDX 쿼리를 지정하는 데 사용됩니다.|
| Microsoft R Open(MRO) | [**MRO**](https://mran.microsoft.com/open)는 Microsoft의 오픈 소스 R 배포판입니다. 패키지와 인터프리터가 포함되어 있습니다. 항상 설치 프로그램에 번들로 제공되는 MRO 버전을 사용합니다. |
| R 도구 | R 콘솔 창 및 명령 프롬프트는 R 배포판의 표준 도구입니다. \Program files\Microsoft SQL Server\140\R_SERVER\bin\x64에서 찾을 수 있습니다. |
| R 샘플 및 스크립트 |  오픈 소스 R 및 RevoScaleR 패키지에는 미리 설치된 데이터를 사용하여 스크립트를 만들고 실행할 수 있도록 기본 제공 데이터 세트가 포함되어 있습니다. \Program files\Microsoft SQL Server\140\R_SERVER\library\datasets and \library\RevoScaleR에서 찾을 수 있습니다. |
| Python 패키지 | [**revoscalepy**](../python/ref-py-revoscalepy.md)는 데이터 조작, 변환, 시각화 및 분석 기능을 제공하는 확장 가능한 Python의 기본 라이브러리입니다. <br/>[**microsoftml**](../python/ref-py-microsoftml.md)은 텍스트 분석, 이미지 분석 및 감정 분석을 위한 사용자 지정 모델을 만들기 위한 기계 학습 알고리즘을 추가합니다.  |
| Python 도구 | 기본 제공 Python 명령줄 도구는 임시 테스트 및 작업에 유용합니다. 이 도구는 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\python.exe에서 찾을 수 있습니다. |
| Anaconda | Anaconda는 Python 및 필수 패키지의 오픈 소스 배포판입니다. |
| Python 샘플 및 스크립트 | R과 마찬가지로, Python에는 기본 제공 데이터 세트와 스크립트가 포함되어 있습니다. revoscalepy 데이터는 \Program files\Microsoft SQL Server\140\PYTHON_SERVER\lib\site-packages\revoscalepy\data\sample-data에서 찾을 수 있습니다. |
| R 및 Python의 미리 학습된 모델 | 미리 학습된 모델은 특정 사용 사례를 위해 만들어지며 Microsoft의 데이터 과학 엔지니어링 팀에서 유지 관리합니다. 미리 학습된 모델을 그대로 사용하여 텍스트의 긍정-부정 감정을 채점하거나, 원하는 새 데이터 입력을 사용하여 이미지의 특징을 감지할 수 있습니다. 미리 학습된 모델은 독립 실행형 서버에서 지원되고 사용할 수 있지만, SQL Server 설치 프로그램을 통해 설치할 수는 없습니다. 자세한 내용은 [SQL Server에 미리 학습된 기계 학습 모델 설치](../install/sql-pretrained-models-install.md)를 참조하세요. |

## <a name="using-a-standalone-server"></a>독립 실행형 서버 사용

R 및 Python 개발자는 오픈 소스 R 및 Python의 메모리 및 처리 제약 조건을 극복하기 위해 일반적으로 독립 실행형 서버를 선택합니다. 독립 실행형 서버에서 실행되는 R 및 Python 라이브러리는 대량의 데이터를 여러 코어에 로드하여 처리하고, 그 결과를 하나의 통합 출력으로 집계할 수 있습니다. 확장성과 유용성 중심으로 엔지니어링되는 고성능 함수는 Microsoft에서 엔지니어링하고 지원하는 상용 서버 제품에 예측 분석, 통계 모델링, 데이터 시각화 및 첨단 기계 학습 알고리즘을 제공합니다.

SQL Server에서 분리된 독립 서버인 R 및 Python 환경은 SQL Server가 아닌 독립 실행형 서버에서 제공하는 기본 운영 체제 및 표준 도구를 사용하여 구성, 보호 및 액세스됩니다. SQL Server 관계형 데이터를 기본적으로 지원하지 않습니다. SQL Server 데이터를 사용하려면 다른 클라이언트에서 하듯이 데이터 원본 개체 및 연결을 만들면 됩니다.

SQL Server의 보충 모델인 독립 실행형 서버는 로컬 및 원격 컴퓨팅이 모두 필요한 경우에 유용하게 사용할 수 있는 강력한 개발 환경이기도 합니다. 독립 실행형 서버의 R 및 Python 패키지는 데이터베이스 엔진 설치와 함께 제공되는 패키지와 동일하며, 코드 이식 및 [컴퓨팅 컨텍스트 전환](/machine-learning-server/r/concept-what-is-compute-context)이 가능합니다.

## <a name="how-to-get-started"></a>시작하는 방법

설치 프로그램을 시작하고, 선호하는 개발 도구에 이진 파일을 연결하고, 첫 번째 스크립트를 작성합니다.

### <a name="step-1-install-the-software"></a>1단계: 소프트웨어 설치

다음 버전 중 하나를 설치합니다.

+ [SQL Server 2017 Machine Learning Server(독립 실행형)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server(독립 실행형) - R 전용](../install/sql-machine-learning-standalone-windows-install.md?view=sql-server-2016)

### <a name="step-2-configure-a-development-tool"></a>2단계: 개발 도구 구성

독립 실행형 서버의 경우 동일한 컴퓨터에 설치된 개발 도구를 사용하여 로컬에서 작업하는 것이 일반적입니다.

+ [R 도구 설정](set-up-a-data-science-client.md)
+ [Python 도구 설정](../python/setup-python-client-tools-sql.md)

### <a name="step-3-write-your-first-script"></a>3단계: 첫 번째 스크립트 작성

RevoScaleR, revoscalepy 및 기계 학습 알고리즘의 함수를 사용하여 R 또는 Python 스크립트를 작성합니다.
  
  + [25개 함수의 R 및 RevoScaleR 살펴보기](/machine-learning-server/r/tutorial-r-to-revoscaler): 기본 R 명령으로 시작한 다음, R 솔루션에 고성능 및 확장성을 제공하는 RevoScaleR 배포 가능 분석 함수로 넘어갑니다. K-means 클러스터링, 의사 결정 트리, 의사 결정 포리스트, 데이터 조작 도구 등 가장 많이 사용되는 R 모델링 패키지의 병렬 처리 버전을 포함합니다.

  + [빠른 시작: microsoftml Python 패키지를 사용하는 이진 분류의 예](/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): microsoftml의 함수와 잘 알려진 유방암 암 데이터 세트를 사용하여 이진 분류 모델을 만듭니다.

작업에 가장 적합한 언어를 선택합니다. SQL을 사용하여 구현하기 어려운 통계 컴퓨팅에는 R이 가장 적합합니다. 데이터에 대한 세트 기반 작업의 경우 강력한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 활용하여 성능을 극대화합니다. 열에 대한 컴퓨팅을 매우 빠르게 수행할 수 있는 메모리 내 데이터베이스 엔진을 사용합니다.

### <a name="step-4-operationalize-your-solution"></a>4단계: 솔루션 운영

독립 실행형 서버는 SQL 브랜드가 아닌 [Microsoft Machine Learning Server](/machine-learning-server/what-is-machine-learning-server)의 [운영](//machine-learning-server/what-is-operationalization) 기능을 사용할 수 있습니다. 독립 실행형 서버의 운영을 구성할 수 있으며, 이를 통해 코드를 웹 서비스로 배포 및 호스팅하고, 진단을 실행하고, 웹 서비스 용량을 테스트할 수 있습니다.

### <a name="step-5-maintain-your-server"></a>5단계: 서버 유지 관리

SQL Server는 정기적으로 누적 업데이트가 출시됩니다. 누적 업데이트를 적용하면 기존에 설치된 버전의 보안과 기능이 향상됩니다. 

새 기능 또는 변경된 기능에 대한 설명은 [CAB 다운로드](../install/sql-ml-cab-downloads.md) 문서와 [SQL Server 2016 누적 업데이트](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions) 및 [SQL Server 2017 누적 업데이트](https://support.microsoft.com/help/4047329)에 대한 웹 페이지에서 찾을 수 있습니다. 

기존 인스턴스에 업데이트를 적용하는 방법에 대한 자세한 내용은 설치 지침의 [업데이트 적용](../install/sql-machine-learning-standalone-windows-install.md#apply-cu)을 참조하세요.

## <a name="see-also"></a>참고 항목

 [R Server(독립 실행형) 또는 Machine Learning Server(독립 실행형) 설치](../install/sql-machine-learning-standalone-windows-install.md)