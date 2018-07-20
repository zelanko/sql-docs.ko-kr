---
title: SQL Server Machine Learning Server (독립 실행형) 및 R Server (독립 실행형) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a8cdceabc26c55b6eade57712fa610d3e84808f5
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174790"
---
# <a name="sql-server-machine-learning-server-standalone-and-r-server-standalone"></a>SQL Server Machine Learning Server (독립 실행형) 및 R Server (독립 실행형)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

독립 실행형 서버는 SQL Server 데이터베이스 엔진 인스턴스와 독립적으로 실행 되는 R 및 Python 기능으로 명시 기계 학습 구성 요소를 설치 합니다. 자체적으로 종속성이 없는 SQL Server에서 독립 실행형 서버를 설치할 수 있습니다. 독립 실행형 서버는 SQL Server, 구성 및 관리 작업의 독립적 이므로 도구는 SQL이 아닌 버전에 대 한 읽을 수 있는 Machine Learning Server의 유사한 [이 문서에서는](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)합니다.

R 및 Python 워크 로드 전용 패키지 및 계산 엔진을 사용 하 여 작은 규모 및 대규모 데이터 집합을 통해 분산 및 병렬 처리와는 다양 한 개발 환경을 제공 하는 독립 실행형 machine learning server 서버를 사용 하 여 설치 합니다. 독립 실행형 서버에서 R 및 Python 패키지는 코드 이식성에 대 한 허용 SQL Server (In-database) 설치에서 제공 하는 것과 동일 하 고 [계산 컨텍스트 전환](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)합니다.

기본 이유 개발자 독립 실행형 machine learning server 오픈 소스 R 및 Python의 메모리 및 처리 제약 조건 초과 이동 하는 것을 선택 합니다. 독립 실행형 서버 로드 및 다중 코어에서 많은 양의 데이터 처리 고 통합 된 단일 출력으로 결과 집계할 수 있습니다. 함수 및 알고리즘은 확장성과 유틸리티에 대 한 엔지니어링: 엔지니어링 예측 분석, 통계 모델링, 데이터 시각화 및 첨단 기계 학습 알고리즘 상용 서버 제품에서 제공 하 고 지 Microsoft입니다.

일반적으로 것이 좋습니다 (독립 실행형)를 처리 하는 (In-database) 설치와 함께 사용할 수 있지만 충분 한 리소스가 있는 경우 리소스 경합을 방지 하려면 배타적는 둘 다 동일한 물리적 컴퓨터에 설치 하는 것에 대 한 대 한 금지 없습니다.

컴퓨터의 한 독립 실행형 서버를 하나만 사용할 수 있습니다: 어느 [SQL Server 2017 Machine Learning Server (독립 실행형)](../install/sql-machine-learning-standalone-windows-install.md) 또는 [SQL Server 2016 R Server (독립 실행형)](../install/sql-r-standalone-windows-install.md)합니다. 다른 버전을 설치 하기 전에 하나의 버전을 수동으로 제거 해야 합니다.

## <a name="components-of-a-standalone-server"></a>독립 실행형 서버 구성 요소

SQL Server 2016은 R만 있습니다. SQL Server 2017은 R과 Python을 지원합니다. 다음 표에 각 버전의 기능을 보여 줍니다.

| 구성 요소 | Description |
|-----------|-------------|
| R 패키지 | [RevoScaleR](revoscaler-overview.md) 데이터 조작, 변환, visualzation, 및 분석에 대 한 함수를 사용 하 여 확장 가능한 R 주 라이브러리입니다.  <br/>[MicrosoftML (R)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 텍스트 분석, 이미지 분석 및 감정 분석에 대 한 사용자 지정 모델을 만드는 기계 학습 알고리즘을 추가 합니다. <br/>[mrsdeploy](operationalization-with-mrsdeploy.md) 제품 웹 서비스 배포 (SQL Server 2017에만 해당)에 있습니다. <br/>[olapR](how-to-create-mdx-queries-using-olapr.md) R에서 MDX 쿼리를 지정 하는 데는|
| Microsoft R Open (MRO) | [MRO](https://mran.microsoft.com/open) 은 Microsoft의 오픈 소스 분산은 R입니다. 패키지 및 인터프리터를 포함 됩니다. 항상 설치 프로그램의 번들 MRO의 버전을 사용 합니다. |
| R 도구 | R 콘솔 창 및 명령 프롬프트를 R 배포에 표준 도구 이며 SQL Server\140\R_SERVER\bin\x64 \Program files\Microsoft에서 찾을 있습니다. |
| R 샘플 및 스크립트 |  오픈 소스 R 및 RevoScaleR 패키지 만들기 및 미리 설치 된 데이터를 사용 하 여 스크립트를 실행할 수 있도록 기본 제공 데이터 집합을 포함 합니다. SQL Server\140\R_SERVER\library\datasets \Program files\Microsoft 및 \library\RevoScaleR에 확인 합니다. |
| Python 패키지 | [revoscalepy](../python/what-is-revoscalepy.md) 데이터 조작, 변환, visualzation, 및 분석에 대 한 함수를 사용 하 여 확장 가능한 Python 주 라이브러리입니다. <br/>[microsoftml (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 텍스트 분석, 이미지 분석 및 감정 분석에 대 한 사용자 지정 모델을 만드는 기계 학습 알고리즘을 추가 합니다.  |
| Python 도구 | 기본 제공 Python 명령줄 도구는 임시 테스트 및 작업에 유용 합니다. SQL Server\140\PYTHON_SERVER\python.exe \Program files\Microsoft에서 도구를 찾습니다. |
| Anaconda | Anaconda는 Python 및 필수 패키지를 오픈 소스 배포 됩니다. |
| Python 샘플 및 스크립트 | R에서와 마찬가지로 Python 기본 제공 데이터 집합 및 스크립트를 포함 합니다. Revoscalepy 데이터 \Program files\Microsoft SQL 영문 Server\140\PYTHON_SERVER\lib\site packages\revoscalepy\data\sample 데이터입니다. |
| R 및 Python에서 미리 학습 된 모델 | 미리 학습 된 모델 지원 되며 독립 실행형 서버에서 사용할 수 있지만 SQL Server 설치 프로그램을 통해 설치할 수 없습니다. Microsoft Machine Learning Server 설치 프로그램을 설치할 수 있는 모델을 제공 무료입니다. 자세한 내용은 [SQL Server에서 기계 학습 모델을 미리 학습 된 설치](../install/sql-pretrained-models-install.md)합니다. |

## <a name="get-started-step-by-step"></a>단계별 시작

설치 프로그램을 시작한 하 여 즐겨 찾는 개발 도구, 바이너리 연결할 첫 번째 스크립트를 작성 합니다.

### <a name="step-1-install-the-software"></a>1 단계: 소프트웨어를 설치 합니다.

이러한 버전 중 하나를 설치 합니다.

+ [SQL Server 2017 Machine Learning Server (독립 실행형)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (독립 실행형)-R만](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>2 단계: 구성 하는 개발 도구

Machine Learning Server 이진 파일을 사용 하 여 개발 도구를 구성 합니다. Python에 대 한 자세한 내용은 참조 하세요. [링크 Python 이진 파일](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)합니다. R 스튜디오에 연결 하는 방법에 지침은 [서로 다른 버전의 R에 사용 하 여](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R) 도구를 C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64 가리킵니다. 시도해 볼 수도 있습니다 [R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)합니다. 

### <a name="step-3-write-your-first-script"></a>3 단계: 첫 번째 스크립트를 작성 합니다.

기계 학습 알고리즘, RevoScaleR 및 revoscalepy를에서 함수를 사용 하 여 R 또는 Python 스크립트를 작성 합니다.
  
  + [Explore R and 알아보기 25 함수에서 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): 기본 R 명령 및 높은 성능을 제공 하는 RevoScaleR 배포 가능한 분석 함수는 진행률 및 R 솔루션에 확장을 다음으로 시작 합니다. K-means 클러스터링, 의사 결정 트리, 의사 결정 포리스트, 데이터 조작 도구 등 가장 많이 사용되는 R 모델링 패키지의 병렬 처리 버전을 포함합니다.

  + [빠른 시작: microsoftml Python 패키지를 사용 하 여 이진 분류 예제](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): microsoftml 및 잘 알려진 breast cancer 데이터 집합에서 함수를 사용 하 여 이진 분류 모델을 만듭니다.

작업을 위한 최상의 언어를 선택 합니다. R은 SQL을 사용 하 여 구현 하기 어려운 통계적 계산에 적합 합니다. 데이터 집합 기반 작업에 대 한의 기능을 활용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 최대 성능을 얻을 수 있습니다. 열에 대해 매우 빠른 계산에 대 한 메모리 내 데이터베이스 엔진을 사용 합니다.

### <a name="step-4-operationalize-your-solution"></a>4 단계: 솔루션 운영 화

독립 실행형 서버를 사용 하는 [운영 화](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) 기능을 SQL-브랜딩되지 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)합니다. 이러한 혜택을 제공 하는 운영 화를 위한 독립 실행형 서버를 구성할 수 있습니다: 배포 및 웹 서비스 용량을 테스트 하는 웹 서비스에서 진단을 실행 하는 대로 코드를 호스트 합니다.

## <a name="see-also"></a>참고자료

 [SQL Server Machine Learning Services (In-database)](sql-server-r-services.md)

