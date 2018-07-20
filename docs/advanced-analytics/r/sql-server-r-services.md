---
title: SQL Server Machine Learning 및 R Services (In-database) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 05a2a17988912d7066b0d9f6bf398b889a3cd882
ms.sourcegitcommit: c37da15581fb34250d426a8d661f6d0d64f9b54c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39174780"
---
# <a name="sql-server-machine-learning-and-r-services-in-database"></a>SQL Server Machine Learning 및 R Services (In-database)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 인스턴스에 있는 데이터에 대 한 R 및 Python 외부 스크립트 지원을 제공 하는 SQL Server 데이터베이스 엔진 인스턴스 컨텍스트 내에서 작동 하는 기계 학습의 데이터베이스에 설치 합니다. Machine learning 통합 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 데이터에 근접 한 분석을 유지 하 고 비용 및 데이터 이동과 관련 된 보안 위험을 제거할 수 있습니다.

데이터베이스 엔진은 다중 인스턴스 이기 때문에 이전 또는 데이터베이스 내 분석의 인스턴스가 둘 이상 및 최신 버전으로 나란히 설치할 수 있습니다. 선택 사항 중 하나 [SQL Server 2017 Machine Learning Services (In-database)](../install/sql-machine-learning-standalone-windows-install.md) R 및 Python을 사용 하 여 또는 [SQL Server 2016 R Services (In-database)](../install/sql-r-standalone-windows-install.md) R.만을 사용 하 여 

알 수 없는 인스턴스도 기계 학습 구성 요소를 설치할 수도 있습니다 [독립 실행형 서버](r-server-standalone.md)합니다. 일반적으로 것이 좋습니다 (독립 실행형)를 처리 하는 (In-database) 설치와 함께 사용할 수 있지만 충분 한 리소스가 있는 경우 리소스 경합을 방지 하려면 배타적 가지 둘 다 동일한 물리적 컴퓨터에 설치 하는 것에 대 한 금지 없습니다.

## <a name="choosing-between-in-database-and-standalone-analytics"></a>데이터베이스 및 독립 실행형 분석 중에서 선택

개발 요구 사항을 이해 하면 도움이 (In-database) 간에 선택 하 고 (독립 실행형)에 도달 합니다. 독립 실행형 서버를 구성 하 고, 사용 방법에서 최대한의 유연성을 하려는 경우 또는 다양 한 SQL Server 외부의 데이터 원본에 연결 하려는 경우 관리 쉽습니다. 

데이터베이스 내 분석을 SQL Server 내에서 데이터를 사용 하 여 심층 통합을 위해 설계 되었습니다. R 또는 Python 함수를 호출 하 고 SQL Server Management Studio 도구 또는 외부 또는 포함 된 T-SQL에 사용 되는 앱에서 스크립트를 실행 하는 T-SQL 쿼리를 작성할 수 있습니다. R 또는 Python 코드를 실행 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 저장된 프로시저를 사용 하거나 SQL Server를 사용 하 여 인스턴스를 [계산 컨텍스트](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context), 데이터베이스 내 분석을 설치 해야 합니다. 최대 데이터 보안 및 SQL Server 도구와의 통합을 제공합니다이.

둘 다에서 데이터베이스 및 독립 실행형 서버에는 오픈 소스 R 및 Python의 메모리 및 처리 제약 조건 완화할 수 있습니다. 로드 및 다중 코어에서 많은 양의 데이터를 처리 하 고, 통합 된 단일 출력으로 결과 집계 하는 기능을 사용 하 여 동일한 패키지 및 도구를 포함 하는 옵션을 모두 합니다. 함수 및 알고리즘은 확장성과 유틸리티에 대 한 엔지니어링: 엔지니어링 예측 분석, 통계 모델링, 데이터 시각화 및 첨단 기계 학습 알고리즘 상용 서버 제품에서 제공 하 고 지 Microsoft입니다. 

## <a name="components-of-an-in-database-installation"></a>데이터베이스 설치의 구성 요소

SQL Server 2016은 R만 있습니다. SQL Server 2017은 R과 Python을 지원합니다. 다음 표에 각 버전의 기능을 보여 줍니다. SQL Server 실행 패드 서비스를 제외 하 고이 테이블은에서 제공 하는 것과 동일 합니다 [독립 실행형 서버 문서](r-server-standalone.md)합니다.

| 구성 요소 | Description |
|-----------|-------------|
| SQL Server 실행 패드 서비스 | 외부 R 및 Python 런타임 간의 통신을 관리 하는 서비스 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스. |
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

+ [SQL Server 2017 Machine Learning Services (In-database)](../install/sql-machine-learning-services-windows-install.md)

+ [SQL Server 2016 R Services (In-database)-R만](../install/sql-r-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>2 단계: 구성 하는 개발 도구

Machine Learning Server 이진 파일을 사용 하 여 개발 도구를 구성 합니다. Python에 대 한 자세한 내용은 참조 하세요. [링크 Python 이진 파일](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)합니다. R 스튜디오에 연결 하는 방법에 지침은 [서로 다른 버전의 R에 사용 하 여](https://support.rstudio.com/hc/en-us/articles/200486138-Using-Different-Versions-of-R) 도구를 C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64 가리킵니다. 시도해 볼 수도 있습니다 [R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)합니다. 

데이터 과학자가 일반적으로 사용 하 여 R 또는 Python 자신의 랩톱 또는 개발 워크스테이션에서 데이터를 탐색 하 고 빌드, 우수한 예측 모델이 될 때까지 예측 모델을 조정 하 합니다. 

SQL Server에서 데이터베이스 내 분석을 사용 하 여이 프로세스를 변경할 필요가 없습니다 있습니다. 설치가 완료 되 면에서 R 또는 Python 코드를 실행할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로컬 또는 원격으로:

![rsql_keyscenario2](media/rsql-keyscenario2.png) 

+ **원하는 IDE를 사용 하 여**입니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 클라이언트 구성 요소는 데이터 과학자의 실험 및 개발에 필요한 모든 도구를 제공합니다. 이러한 도구에는 R 런타임, 표준 R 작업의 성능을 향상시키기 위한 인텔 수학 커널 라이브러리 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R 코드 실행을 지원하는 향상된 R 패키지 집합이 포함됩니다.  

+ **원격 또는 로컬로 작업**합니다. 데이터 과학자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하여 평소와 같이 로컬 분석을 위해 클라이언트에 제공합니다. 그러나 더 나은 솔루션을 사용 하는 합니다 **RevoScaleR** 또는 **revoscalepy** 계산을 푸시 Api를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 비용이 많이 들고 안전 하지 않은 데이터 이동을 방지 하는 컴퓨터를 합니다.

+ **R 또는 Python 스크립트를 포함 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저**합니다. 코드를 완전히 최적화 하는 경우 불필요 한 데이터 이동을 방지 하 고 데이터 처리 작업을 최적화 하는 저장된 프로시저에 래핑하십시오.

### <a name="step-3-write-your-first-script"></a>3 단계: 첫 번째 스크립트를 작성 합니다.

T-SQL 스크립트 내에서 R 또는 Python 함수를 호출 합니다.
  
  + [R: Transact-SQL에서 R 코드 사용](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md) 
  + [R: SQL 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)
  + [Python: T-SQL을 사용하여 Python 실행](../tutorials/run-python-using-t-sql.md)
  + [Python: SQL 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)

작업을 위한 최상의 언어를 선택 합니다. R은 SQL을 사용 하 여 구현 하기 어려운 통계적 계산에 적합 합니다. 데이터 집합 기반 작업에 대 한의 기능을 활용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 최대 성능을 얻을 수 있습니다. 열에 대해 매우 빠른 계산에 대 한 메모리 내 데이터베이스 엔진을 사용 합니다.

### <a name="step-4-optimize-your-solution"></a>4 단계: 솔루션을 최적화

모델이 엔터프라이즈 데이터의 크기를 조정 하는 준비 되 면 데이터 과학자는 종종 같은 프로세스를 최적화 하기 위해 DBA 또는 SQL 개발자를 사용 하 여 작동 합니다.

+ 기능 엔지니어링
+ 데이터 수집 및 데이터 변환
+ 점수 매기기

일반적으로 큰 데이터 집합을 사용 하는 경우에 특히 데이터 과학자가 R을 사용 하 여 성능 및 확장성 문제가 되었습니다. 이것은 공용 런타임 구현이 단일 스레드 이며 로컬 컴퓨터에서 사용 가능한 메모리에 맞는 데이터 집합만 수용할 수 있습니다. 더 많은 데이터를 사용 하 여 성능 향상을 위해 여러 기능을 제공 하는 SQl Server Machine Learning Services와 통합:

+ **RevoScaleR**:이 R 패키지에 병렬 처리 및 확장성을 제공 하도록 다시 설계 된 가장 인기 있는 R 함수 중 일부는 구현이 포함 되어 있습니다. 또한 일반적으로는 훨씬 큰 메모리와 계산력을 갖춘 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 계산을 푸시하여 성능과 확장을 더 증대하는 함수도 포함되어 있습니다.

+ **revoscalepy**합니다. SQL Server 2017에서 사용할 수 있는이 Python 라이브러리 RevoScaleR의 원격 계산 컨텍스트 등 가장 인기 있는 기능을 구현 및 지 원하는 많은 알고리즘 분산 처리 합니다.

**리소스**

+ [성능 사례 연구](../../advanced-analytics/r/performance-case-study-r-services.md)
+ [R 및 데이터 최적화](../../advanced-analytics/r/r-and-data-optimization-r-services.md)

### <a name="step-5-deploy-and-consume"></a>5 단계: 배포 및 사용

스크립트 또는 모델이 프로덕션 사용 준비가 되 면 응용 프로그램에서 저장 된 R 또는 Python 코드를 호출할 수 있도록 데이터베이스 개발자 저장된 프로시저에는 코드 또는 모델 포함 될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 R 코드를 저장하고 실행하면 많은 이점이 있습니다. 편리한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 인터페이스를 사용하고 모든 계산이 데이터베이스에서 실행되어 불필요한 데이터 이동을 방지할 수 있습니다.

![rsql_keyscenario1](media/rsql-keyscenario1.png)

+ **안전 하 고 확장 가능한**합니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 데이터베이스 엔진의 보안을 유지 하 고 R 및 Python 세션을 격리 하는 새로운 확장성 아키텍처를 사용 합니다. 스크립트를 실행할 수 있는 사용자를 제어 해야 하 고 코드에서 액세스할 수 있는 데이터베이스를 지정할 수 있습니다. 대규모 계산이 서버의 전반적인 성능을 저해 하지 않도록 런타임에 할당 된 리소스의 양을 제어할 수 있습니다.

+ **일정 및 감사**합니다. 외부 스크립트 작업에서 실행 되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 제어할 수 있습니다 및 감사 데이터는 데이터 과학자가 사용 합니다. 또한 작업 및 다른 T-SQL 작업 또는 저장된 프로시저를 예약 하는 것 처럼 외부 R 또는 Python 스크립트를 포함 하는 만든 워크플로 예약할 수 있습니다.

이점은 리소스 관리 및 보안 기능을 SQL server에서를 사용 하려면 배포 프로세스는 이러한 작업 포함 될 수 있습니다.

+ 저장된 프로시저에서 최적으로 실행할 수 있는 함수에 yourcode 변환
+ 보안을 설정 하 고 특정 작업에 의해 사용 되는 패키지를 잠그는
+ 리소스 거 버 넌 스 (Enterprise edition 필요)를 사용 하도록 설정

**리소스**

+ [R에 대 한 리소스 거 버 넌 스](resource-governance-for-r-services.md)
+ [SQL Server에 대 한 R 패키지 관리](install-additional-r-packages-on-sql-server.md)

## <a name="see-also"></a>참고자료

 [SQL Server Machine Learning 및 R Server (독립 실행형)](sql-server-r-services.md)
