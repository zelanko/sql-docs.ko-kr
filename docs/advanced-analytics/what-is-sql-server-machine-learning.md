---
title: SQL Server Machine Learning Services의 SQL Server Machine Learning 서비스 (R, Python)-개요
description: SQL server에서 관계형 데이터에 대 한 데이터 과학 및 통계를 사용 하 여 Python 및 R을 통합할 수 있는 Machine Learning Services 기능의 개요 모델링, 기계 학습 모델, 예측 분석, 데이터 시각화 및 더 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: overview
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ea6db43d999c2c0102cde0c0b30867f255bce569
ms.sourcegitcommit: f7ad034f748ebc3e5691a5e4c3eb7490e5cf3ccf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469215"
---
# <a name="sql-server-machine-learning-services-r-python"></a>SQL Server Machine Learning 서비스 (R, Python)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Machine Learning 서비스에에서 in-database R 및 Python 스크립트를 실행 하는 데 사용 되는 SQL Server의 기능입니다. 기능이 포함 되어 있습니다 [Microsoft R 및 Python 패키지](#components) 고성능 예측 분석 및 기계 학습에 대 한 합니다. R 및 Python 코드 포함 하는 T-SQL 또는 저장된 프로시저에 R 및 Python 문이 포함 된 T-SQL 스크립트를 통해 R 및 Python 스크립트에서 관계형 데이터를 사용할 수 있습니다.

이전에 사용한 [SQL Server 2016 R Services](r/sql-server-r-services.md), SQL Server 2017 이상 Machine Learning 서비스는 기본 R, RevoScaleR MicrosoftML, 업데이트 된 버전을 사용 하 여 R 지원의 다음 세대 및 다른 라이브러리에 도입 된 2016 합니다.

Azure SQL Database에서 [Machine Learning 서비스 (R)을 통한](https://docs.microsoft.com/azure/sql-database/sql-database-machine-learning-services-overview) 현재 공개 미리 보기로 제공 됩니다.

## <a name="bring-compute-power-to-the-data"></a>데이터에 계산 능력을 가져오기

Machine Learning 서비스의 핵심 가치 제안을 소수 자릿수 및 계산 및 처리, 데이터 상주를 제공 하는 기능에 대 한 고급 분석을 제공 하는 엔터프라이즈 R 및 Python 패키지의 기능에서 데이터 끌어오기를 할 필요가 없습니다 네트워크입니다. 다음과 같은 여러 이점을 제공 합니다.

+ 데이터 보안. R 및 Python의 데이터 원본에 더 가깝게 실행 불필요 하거나 안전 하지 않은 데이터 이동을 방지할 수 있습니다.
+ 속도. 데이터베이스는 집합 기반 작업에 최적화됩니다. 메모리 내 테이블에 같은 데이터베이스의 최신 혁신 요약 및 번개, 집계 및 데이터 과학을 완벽 하 게 보완 됩니다.
+ 배포 및 통합 편의성입니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 다른 많은 데이터 관리 작업 및 응용 프로그램에 대 한 작업의 중앙 지점이입니다. 보고 웨어하우스 데이터베이스에 있는 데이터를 사용 하 여 기계 학습 솔루션에서 사용 하는 데이터가 일관성 있고 최신 인지 확인 합니다. 
+ 클라우드 및 온-프레미스에서 효율성입니다. R 또는 Python 세션에서 데이터를 처리 하는 대신 비롯 하 여 엔터프라이즈 데이터 파이프라인에 의존할 수 있습니다 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 및 Azure Data Factory 합니다. Power BI 또는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]를 통해 결과 또는 분석을 쉽게 보고할 수 있습니다.

다양한 데이터 처리 및 분석 작업에 SQL과 R을 적절하게 조합하여 사용하면 데이터 과학자와 개발자가 모두 생산성을 높일 수 있습니다.

<a name="components"></a>

## <a name="components"></a>구성 요소

SQL Server 2017은 R과 Python을 지원합니다. 다음 표에서 구성 요소를 설명 합니다.

| 구성 요소 | Description |
|-----------|-------------|
| SQL Server 실행 패드 서비스 | 외부 R 및 Python 런타임 및 데이터베이스 엔진 인스턴스 간 통신을 관리 하는 서비스입니다. |
| R 패키지 | [**RevoScaleR**](r/ref-r-revoscaler.md)은 확장 가능한 R의 주요 라이브러리입니다. 이 라이브러리의 함수들은 가장 널리 사용됩니다. 데이터 변환 및 조작, 통계 요약, 시각화 및 다양한 형태의 모델링 및 분석을 이러한 라이브러리에서 찾을 수 있습니다. 또한 이 라이브러리의 함수는 계산 엔진에서 조정 및 관리하는 데이터 청크 작업을 수행할 수 있는 병렬 처리를 위해 사용 가능한 코어에 작업 부하를 자동으로 배포합니다.  <br/>[**MicrosoftML (R)** ](r/ref-r-microsoftml.md)은 텍스트 분석, 이미지 분석 및 감정 분석에 대한 사용자 지정 모델을 만드는 기계 학습 알고리즘을 추가합니다. <br/>[**sqlRUtils**](r/ref-r-sqlrutils.md)는 T-SQL 저장 프로시저에 R 스크립트를 배치하고, 데이터베이스에 저장 프로시저를 등록하고, R 개발 환경에서 저장 프로시저를 실행하는 것에 대한 도우미 함수를 제공합니다.<br/>[**olapR**](r/ref-r-olapr.md)은 R 스크립트에서 MDX 쿼리를 작성 또는 실행합니다.|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open)은 R의 Microsoft의 오픈 소스 배포입니다. 패키지 및 인터프리터를 포함합니다. 항상 설치 프로그램으로 설치되는 MRO의 버전을 사용합니다. |
| R 도구 | R 콘솔 창 및 명령 프롬프트를 R 배포에 표준 도구 이며  |
| R 샘플 및 스크립트 |  오픈 소스 R 및 RevoScaleR 패키지 만들기 및 미리 설치 된 데이터를 사용 하 여 스크립트를 실행할 수 있도록 기본 제공 데이터 집합을 포함 합니다. |
| Python 패키지 | [**revoscalepy** ](python/ref-py-revoscalepy.md) 데이터 조작, 변환, 시각화 및 분석에 대 한 함수를 사용 하 여 확장 가능한 Python 주 라이브러리입니다. <br/>[ **(Python) microsoftml** ](python/ref-py-microsoftml.md) 텍스트 분석, 이미지 분석 및 감정 분석에 대 한 사용자 지정 모델을 만드는 기계 학습 알고리즘을 추가 합니다.  |
| Python 도구 | 기본 제공 Python 명령줄 도구는 임시 테스트 및 작업에 유용 합니다.  |
| Anaconda | Anaconda는 Python 및 필수 패키지의 오픈 소스 배포입니다. |
| Python 샘플 및 스크립트 | R에서와 마찬가지로 Python 기본 제공 데이터 집합 및 스크립트를 포함 합니다.  |
| R 및 Python에서 미리 학습 된 모델 | 미리 학습 된 모델은 특정 사용 사례에 대 한 생성 되 고 microsoft 데이터 과학 엔지니어링 팀에서 유지 관리 합니다. 으로 미리 학습 된 모델을 사용할 수 있습니다-텍스트에서 양수 음수가 감정 점수 매기기 또는 기능에서 제공 하는 새 데이터 입력을 사용 하 여 이미지를 검색 하는 것입니다. 모델은 Machine Learning 서비스에서 실행 되지만 SQL Server 설치 프로그램을 통해 설치할 수 없습니다. 자세한 내용은 [설치 미리 학습 된 기계 학습 모델 SQL Server에서](install/sql-pretrained-models-install.md)합니다. |

## <a name="using-sql-mls"></a>SQL MLS를 사용 하 여

개발자 및 분석가 로컬 SQL Server 인스턴스를 기반으로 실행 되는 코드에 있는 경우가 많습니다. SQL Server 형식에서 R 및 Python 코드를 실행 하는 기능을 얻게 Machine Learning 서비스를 추가 하 고 외부 스크립트 실행을 사용 하도록 설정 하 여: 저장된 프로시저에서 스크립트를 래핑, SQL Server 테이블에 모델을 저장 또는 T-SQL 및 R 또는 Python 함수를 결합 합니다. 쿼리에서 합니다.

데이터 보안 모델의 경계 내에서 스크립트 실행이: 관계형 데이터베이스에 대 한 권한이 스크립트에 대 한 데이터 액세스의 기반이 됩니다. R 또는 Python 스크립트를 실행 하는 사용자는 SQL 쿼리를 해당 사용자가 액세스할 수 없습니다는 모든 데이터를 사용할 수 없습니다. 표준 데이터베이스 읽기 및 쓰기 권한, 외부 스크립트를 실행 하는 추가 권한이 필요 합니다. 모델 및 관계형 데이터에 대 한 작성 하는 코드는 저장된 프로시저에서 래핑된 이진 형식으로 직렬화 및 테이블에 저장 또는 파일로 원시 바이트 스트림으로 직렬화 하는 경우 디스크에서 로드 합니다.

데이터베이스 내 분석에 대 한 가장 일반적인 방법은 사용 하는 것 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), R 또는 Python 스크립트를 입력된 매개 변수로 전달 합니다.

기존 클라이언트-서버 상호 작용은 또 다른 방법은. IDE에 있는 모든 클라이언트 워크스테이션에서 설치할 수 있습니다 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) 또는 [Python 라이브러리](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter), 한 다음 실행을 푸시하는 코드 작성 (라고는 *원격 계산 상황에 맞는*) 데이터 및 원격 SQL Server에는 작업입니다. 

마지막으로 사용 하는 경우는 [독립 실행형 서버](r/r-server-standalone.md) 및 Developer 버전에서는 동일한 라이브러리 및 인터프리터를 사용 하 여 클라이언트 워크스테이션에서 솔루션을 구축 하 고 다음 SQL Server Machine Learning에서 프로덕션 코드를 배포할 수 있습니다 Services (In-database)입니다. 

## <a name="how-to-get-started"></a>시작하는 방법

### <a name="step-1-install-the-software"></a>1단계: 소프트웨어 설치

+ [SQL Server Machine Learning Services (In-database)](install/sql-machine-learning-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>2단계: 개발 도구를 구성 합니다.

데이터 과학자들은 일반적으로 랩톱이나 개발 워크스테이션에서 R 또는 Python을 사용하여 데이터를 탐색하고 좋은 예측 모델을 얻을 때까지 예측 모델을 작성 및 조정합니다. SQL Server의 데이터베이스 내 분석 기능을 사용하면 이 프로세스를 변경할 필요가 없습니다. 설치가 완료되면 SQL Server에서 R 또는 Python 코드를 로컬 및 원격으로 실행할 수 있습니다.

![rsql_keyscenario2](r/media/rsql-keyscenario2.png) 

+ **원하는 IDE를 사용**합니다. 원하는 개발 도구에 R 및 Python 라이브러리를 연결할 수 있습니다. 자세한 내용은 [R 도구 설정](r/set-up-a-data-science-client.md)과 [Python 도구 설정](python/setup-python-client-tools-sql.md)을 참조합니다.  

+ **원격 또는 로컬로 작업**합니다. 데이터 과학자는 평소와 같이 SQL Server에 연결하여 로컬 분석을 위해 클라이언트에 데이터를 가져올 수 있습니다. 그러나 더 나은 솔루션은 **RevoScaleR** 또는 **revoscalepy** API를 사용하여 계산을 SQL Server 컴퓨터로 푸시하여 비용이 많이 들고 안전하지 않은 데이터 이동을 방지하는 것입니다.

+ **SQL Server 저장 프로시저에 R 또는 Python 스크립트를 포함**합니다. 코드가 완전히 최적화되면 불필요한 데이터 이동을 방지하고 데이터 처리 작업을 최적화하기 위해 저장된 프로시저로 래핑하십시오.

### <a name="step-3-write-your-first-script"></a>3단계: 첫 번째 스크립트를 작성 합니다.

T-SQL 스크립트 내에서 R 또는 Python 함수를 호출 합니다.

+ [R: R을 사용 하 여 데이터베이스 내 분석에 알아봅니다.](tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [R: R 사용 하 여 종단 간 연습](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
+ [Python: T-SQL을 사용 하 여 Python 실행](tutorials/run-python-using-t-sql.md)
+ [Python: Python을 사용 하 여 데이터베이스 내 분석에 알아봅니다.](tutorials/sqldev-in-database-python-for-sql-developers.md)

작업에 가장 적합한 언어를 선택하십시오. R은 SQL을 사용하여 구현하기 어려운 통계 계산에 가장 적합합니다. 데이터를 통한 집합 기반 작업의 경우 SQL Server의 성능을 최대한 활용하여 성능을 극대화하십시오. 열에 대한 매우 빠른 계산을 위해 메모리 내 데이터베이스 엔진을 사용하십시오.

### <a name="step-4-optimize-your-solution"></a>4단계: 솔루션을 최적화

모델이 엔터프라이즈 데이터의 크기를 조정 하는 준비 되 면 데이터 과학자는 종종 같은 프로세스를 최적화 하기 위해 DBA 또는 SQL 개발자를 사용 하 여 작동 합니다.

+ 기능(Feature) 엔지니어링
+ 데이터 수집 및 데이터 변환
+ 점수 매기기

일반적으로 R을 사용하는 데이터 과학자들은 특히 대규모 데이터 세트를 사용할 때 성능과 규모면에서 문제가 있었습니다. 이는 일반적인 런타임 구현이 단일 스레드이며 로컬 컴퓨터의 사용 가능한 메모리에 맞는 데이터 세트만 수용할 수 있기 때문입니다. SQL Server Machine Learning Services와의 통합은 더 많은 데이터와 함께 더 나은 성능을 위한 여러 가지 기능을 제공합니다:

+ **RevoScaleR**: 이 R 패키지는 병렬 처리 및 확장성을 제공 하도록 다시 설계 된 가장 인기 있는 R 함수 중 일부는 구현이 포함 되어 있습니다. 또한 이 패키지에는 계산을 SQL Server 컴퓨터로 밀어넣어 성능과 확장성을 높이는 기능이 포함되어 있습니다. SQL Server 컴퓨터는 대개 메모리와 계산 능력이 훨씬 뛰어납니다.

+ **revoscalepy**. 이 Python 라이브러리는 원격 계산 컨텍스트와 분산 처리를 지원하는 많은 알고리즘과 같이 RevoScaleR에서 가장 많이 사용되는 함수를 구현합니다.

성능에 대한 자세한 내용은 [성능 사례 연구](r/performance-case-study-r-services.md)와 [R 및 데이터 최적화](r/r-and-data-optimization-r-services.md)를 참조합니다.

### <a name="step-5-deploy-and-consume"></a>5단계: 배포 및 사용

스크립트 또는 모델이 프로덕션 사용 준비가 되 면 응용 프로그램에서 저장 된 R 또는 Python 코드를 호출할 수 있도록 데이터베이스 개발자 저장된 프로시저에는 코드 또는 모델 포함 될 수 있습니다. 저장 하 고 SQL Server에서 R 코드를 실행 중인 많은 이점이 있습니다: 편리한 SQL Server 인터페이스를 사용할 수 있으며 모든 계산이 데이터베이스에서 불필요 한 데이터 이동을 방지할 수행 합니다.

![rsql_keyscenario1](r/media/rsql-keyscenario1.png)

+ **안전 하 고 확장 가능한**합니다. SQL Server 데이터베이스 엔진의 보안을 유지 하 고 R 및 Python 세션을 격리 하는 새로운 확장성 아키텍처를 사용 합니다. 스크립트를 실행할 수 있는 사용자를 제어 해야 하 고 코드에서 액세스할 수 있는 데이터베이스를 지정할 수 있습니다. 대규모 계산이 서버의 전반적인 성능을 저해 하지 않도록 런타임에 할당 된 리소스의 양을 제어할 수 있습니다.

+ **일정 및 감사**합니다. SQL Server에서 외부 스크립트 작업 실행을 제어할 수 있으며 데이터 과학자가 사용 되는 데이터를 감사 수 있습니다. 또한 작업 및 다른 T-SQL 작업 또는 저장된 프로시저를 예약 하는 것 처럼 외부 R 또는 Python 스크립트를 포함 하는 만든 워크플로 예약할 수 있습니다.

를 이용 하려면 리소스 관리 및 보안 기능에 SQL Server 배포 프로세스는 이러한 작업 포함 될 수 있습니다.

+ 저장된 프로시저에서 최적으로 실행할 수 있는 함수 코드 변환
+ 보안을 설정 하 고 특정 작업에 의해 사용 되는 패키지를 잠그는
+ 리소스 거 버 넌 스 (Enterprise edition 필요)를 사용 하도록 설정

자세한 내용은 [R에 대 한 리소스 거 버 넌 스](r/resource-governance-for-r-services.md) 하 고 [SQL Server에 대 한 R 패키지 관리](r/install-additional-r-packages-on-sql-server.md)합니다.

## <a name="version-history"></a>버전 기록

SQL Server 2017의 Machine Learning Services는 SQL Server 2016 R Services에 Python을 포함 하도록 개선의 다음 세대입니다. 다음 표는 현재 버전에는 처음부터 모든 제품 버전의 전체 목록을 합니다. 

| 제품 이름 | 엔진 버전 | 릴리스 날짜 |
|--------------|---------|--------------|
| SQL Server 2017 Machine Learning Services (In-database) | R Server 9.2.1 <br/> Python Server 9.2 | 2017년 10월 |
| SQL Server 2017 Machine Learning Server (독립 실행형) | R Server 9.2.1 <br/> Python Server 9.2 | 2017년 10월 |
| SQL Server 2016 R Services (In-database) | R Server 9.1  | 2017 년 7 월  |
| SQL Server 2016 R Server (독립 실행형)  |  R Server 9.1 | 2017 년 7 월 |

릴리스에서 패키지 버전을 버전에 매핑할을 참조 하세요 [업그레이드 하는 R 및 Python 구성 요소](install/upgrade-r-and-python.md#version-map)합니다.

## <a name="portability-and-related-products"></a>이식성 및 관련된 제품

사용자 지정 R 및 Python 코드의 이식성은 패키지 배포 및 여러 제품에 내장 된 인터프리터를 통해 처리 됩니다. SQL Server에서 제공 되는 동일한 패키지도 다른 여러 Microsoft 제품 및 서비스를 호출 하는 SQL이 아닌 버전을 포함 하 여에서 사용할 수 있습니다 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/)합니다. 

R 및 Python 인터프리터를 포함 하는 무료 클라이언트가 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) 하며 [Python 라이브러리](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)합니다.

Azure에서 Microsoft R 및 Python 패키지 및 인터프리터에서 사용할 수 있습니다 Azure Machine Learning 및 Azure 서비스와 같은 [HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview), 및 [Azure virtual machines](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux)합니다. 합니다 [데이터 과학 Virtual Machine](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/) 여러 공급 업체와 라이브러리 도구 및 Microsoft에서 인터프리터를 사용 하 여 준비를 모두 갖추게 개발 워크스테이션을 포함 합니다.

## <a name="see-also"></a>참고자료

[SQL Server Machine Learning 서비스 설치](install/sql-machine-learning-services-windows-install.md)
