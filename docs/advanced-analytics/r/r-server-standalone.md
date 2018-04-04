---
title: SQL Server 컴퓨터 학습 서버 (독립 실행형) 및 R Server (독립 실행형) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
vms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.openlocfilehash: 3f6bb60e639517e458684486f36123d47a68dbf9
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="sql-server-machine-learning-server-standalone-and-r-server-standalone"></a>SQL Server 컴퓨터 학습 서버 (독립 실행형) 및 R Server (독립 실행형)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

독립 실행형 서버는 SQL Server 데이터베이스 엔진 인스턴스와 독립적으로 실행 하는 R 및 Python 기능으로 명시 컴퓨터 학습 구성 요소 설치. SQL Server에 종속성이 없는 단독으로 사용 하거나 독립 실행형 서버를 설치할 수 있습니다. 독립 실행형 서버는 SQL Server, 구성 및 관리 작업의 독립적인 및 도구는 비 SQL 버전에 대 한 읽을 수 있는 학습 서버, 컴퓨터의 더 유사 하기 때문에 [이 여기서](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)합니다.

독점 패키지 및 계산 엔진을 사용 하 여 작은-큰 데이터 집합을 통해 R 및 Python 작업의 분산 및 병렬 처리와 풍부한 개발 환경을 제공 하는 독립 실행형 컴퓨터 학습 서버 서버와 함께 설치 합니다. 독립 실행형 서버에서 R 및 Python 패키지 코드 이식성에 대 한 허용 하는 SQL Server (In-database) 설치에서 제공 된 것과 동일 하 고 [계산 컨텍스트 전환](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)합니다.

개발자는 주된 이유는 독립 실행형 컴퓨터 학습 서버는 오픈 소스 R 및 Python의 메모리와 처리 제약 조건 것 이상의 기능을 선택 합니다. 독립 실행형 서버 로드 및 여러 코어에 많은 양의 데이터 처리 고 하나의 통합 된 출력으로 결과 집계 합니다. 크기 조정 및 유틸리티 모두에 대 한 함수 및 알고리즘은 엔지니어링: 엔지니어링 및에서 지 원하는 예측 분석, 통계 모델링, 데이터 시각화 및 최신 기계 학습 상용 서버 제품의 알고리즘 제공 Microsoft 합니다.

일반적으로 것이 좋습니다 (독립 실행형)를 처리 하는 (In-database) 설치와 함께 사용할 수 있지만 충분 한 리소스가 있는 경우 리소스 경합을 방지 하려면 배타적는 모두 동일한 물리적 컴퓨터에서 설치에 대 한 금지 없습니다.

컴퓨터에 독립 실행형 서버를 하나만 사용할 수 있습니다: 어느 [SQL Server 2017 컴퓨터 학습 서버 (독립 실행형)](../install/sql-machine-learning-standalone-windows-install.md) 또는 [SQL Server 2016 R 서버 (독립 실행형)](../install/sql-r-standalone-windows-install.md)합니다. 다른 버전을 설치 하기 전에 한 버전을 수동으로 제거 해야 합니다.

## <a name="components-of-a-standalone-server"></a>독립 실행형 서버 구성 요소

SQL Server 2016은 R만 있습니다. SQL Server 2017은 R과 Python을 지원합니다. 다음 표에서 각 버전의 기능을 설명합니다.

| 구성 요소 | Description |
|-----------|-------------|
| R 패키지 | [RevoScaleR](revoscaler-overview.md) 함수와 데이터 조작, 변환, visualzation, 및 분석에 대 한 확장 가능한 R에 대 한 주 라이브러리는 합니다.  <br/>[MicrosoftML (R)](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 텍스트 분석, 이미지 분석 및 감성 분석에 대 한 사용자 지정 모델을 만드는 기계 학습 알고리즘을 추가 합니다. <br/>[mrsdeploy](operationalization-with-mrsdeploy.md) 웹 (SQL Server 2017에만 해당)에서 서비스 배포를 제공 합니다. <br/>[olapR](how-to-create-mdx-queries-using-olapr.md) R에서 MDX 쿼리를 지정 하는|
| Microsoft R Open (MRO) | [MRO](https://mran.microsoft.com/open) 는 Microsoft의 오픈 소스 분포는 R입니다. 패키지 및 인터프리터 포함 됩니다. 항상 설치 프로그램에 번들로 묶이는 MRO의 버전을 사용 합니다. |
| R 도구 | R 콘솔 창 및 명령 프롬프트는 R 분포에서 표준 도구입니다. \Program files\microsoft SQL Server\140\R_SERVER\bin\x64 찾아서 합니다. |
| R 샘플 및 스크립트 |  오픈 소스 R 및 RevoScaleR 패키지는 만들고 사전 설치 된 데이터를 사용 하 여 스크립트를 실행할 수 있도록 기본 제공 데이터 집합을 포함 합니다. Files\microsoft SQL Server\140\R_SERVER\library\datasets 및 \library\RevoScaleR에서 검색 합니다. |
| Python 패키지 | [revoscalepy](../python/what-is-revoscalepy.md) 확장 가능한 Python 데이터 조작, 변환, visualzation, 및 분석에 대 한 함수 사용에 대 한 주 라이브러리는 합니다. <br/>[microsoftml (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 텍스트 분석, 이미지 분석 및 감성 분석에 대 한 사용자 지정 모델을 만드는 기계 학습 알고리즘을 추가 합니다.  |
| Python 도구 | 기본 제공 된 Python 명령줄 도구는 임시 테스트 및 작업에 유용 합니다. \Program files\microsoft SQL Server\140\PYTHON_SERVER\python.exe 도구를 찾습니다. |
| Anaconda | Anaconda는 Python 및 필수 패키지를 오픈 소스 배포입니다. |
| Python 샘플 및 스크립트 | R을와 마찬가지로 Python 기본 제공 데이터 집합 및 스크립트를 포함 합니다. \Program files\microsoft SQL revoscalepy 데이터를 찾는 Server\140\PYTHON_SERVER\lib\site packages\revoscalepy\data\sample 데이터입니다. |
| R 및 Python에서 미리 학습 된 모델 | 미리 학습 된 모델은 지원 되 고 독립 실행형 서버에서 사용할 수 있지만 SQL Server 설치 프로그램을 통해 설치할 수 없습니다. 설치할 수 있는 모델을 제공 하는 Microsoft 학습 서버 컴퓨터에 대 한 설치 프로그램 무료입니다. 자세한 내용은 참조 [설치 기계 학습 모델 SQL Server에서 미리 학습 된](install-pretrained-models-sql-server.md)합니다. |

## <a name="get-started-step-by-step"></a>단계별 시작

설치 프로그램을 시작한 바이너리 즐겨 찾는 개발 도구에 연결할 첫 번째 스크립트를 작성 합니다.

### <a name="step-1-install-the-software"></a>1 단계: 소프트웨어를 설치 합니다.

이러한 버전 중 하나를 설치 합니다.

+ [SQL Server 2017 컴퓨터 학습 서버 (독립 실행형)](../install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Server (독립 실행형)-R만](../install/sql-r-standalone-windows-install.md)

### <a name="step-2-configure-a-development-tool"></a>개발 도구를 구성 하는 2 단계:

컴퓨터 학습 서버 이진 파일을 사용 하 여 개발 도구를 구성 합니다. Python에 대 한 자세한 내용은 참조 [링크 Python 바이너리](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)합니다. R 스튜디오에 연결 하는 방법에 지침은 [서로 다른 버전의 R에 사용 하 여](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R) 도구를 C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64 가리키도록 합니다. 시도할 수 있습니다 [R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)합니다. 

### <a name="step-3-write-your-first-script"></a>3 단계: 첫 번째 스크립트를 작성 합니다.

RevoScaleR, revoscalepy, 및 기계 학습 알고리즘에서 함수를 사용 하 여 Python 또는 R 스크립트를 작성 합니다.
  
  + [R과 25 함수에서 RevoScaleR 탐색](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler): R의 기본 명령을 한 높은 성능을 제공 하는 RevoScaleR 배포 가능한 분석 함수에 처리 및 R 솔루션을 확장을 다음 시작 합니다. K-means 클러스터링, 의사 결정 트리, 의사 결정 포리스트, 데이터 조작 도구 등 가장 많이 사용되는 R 모델링 패키지의 병렬 처리 버전을 포함합니다.

  + [빠른 시작: microsoftml Python 패키지와 함께 이진 분류의 예](https://docs.microsoft.com/machine-learning-server/python/quickstart-binary-classification-with-microsoftml): microsoftml 및 잘 알려진 breast 유방암 데이터 집합에서 함수를 사용 하 여 이진 분류 모델을 만듭니다.

작업에 대 한 적합 한 언어를 선택 합니다. R은 SQL을 사용 하 여 구현 하기 어려운 통계적 계산에 가장 적합 합니다. 데이터에 대해 집합 기반 작업에 대 한 성능을 활용해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 최대 성능을 얻을 수 있도록 합니다. 열에 대해 매우 빠른 계산을 위한 메모리 내 데이터베이스 엔진을 사용 합니다.

### <a name="step-4-operationalize-your-solution"></a>4 단계: 솔루션 운영 화

독립 실행형 서버에서 사용할 수는 [해결해줍니다](https://docs.microsoft.com//machine-learning-server/what-is-operationalization) 는 SQL-브랜딩되지의 기능 [Microsoft 컴퓨터 학습 서버](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server)합니다. 운영 화, 다음과 같은이 이점을 제공 하는 독립 실행형 서버를 구성할 수 있습니다: 배포 및 테스트에 웹 서비스 용량 진단을 실행 하는 웹 서비스 코드를 호스트 합니다.

## <a name="see-also"></a>참고 항목

 [SQL Server 컴퓨터 학습 Services (In-database)](sql-server-r-services.md)

