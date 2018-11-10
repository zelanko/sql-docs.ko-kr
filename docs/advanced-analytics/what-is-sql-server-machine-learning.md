---
title: R 및 Python Machine Learning Services에서 SQL Server | Microsoft Docs
description: SQL Server 및 SQL server에서 데이터 과학 및 통계 모델링, 기계 학습 모델, 예측 분석, 데이터 시각화 등에 대 한 관계형 데이터와 통합 하는 Python R입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0768ae40b110bbb2b85890f0a8b4eff0339cedde
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269706"
---
# <a name="machine-learning-services-r-python-in-sql-server-2017"></a>SQL server 2017 machine Learning Services (R, Python)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2017의 Machine Learning Services는 SQL Server에서 R 및 Python 코드를 실행 하는 데 사용 되는 데이터베이스 엔진 인스턴스를 추가 합니다. 핵심 엔진 프로세스 로부터 격리 하지만 저장된 프로시저, R 또는 Python 문이 포함 된 T-SQL 스크립트 또는 T-SQL을 포함 하는 R 또는 Python 코드와 관계형 데이터에 완벽 하 게 사용할 수 있는 코드는 확장성 프레임 워크에서 실행 됩니다. 

이전에 사용한 [SQL Server 2016 R Services](r/sql-server-r-services.md), SQL Server 2017의 Machine Learning 서비스는 기본 R, RevoScaleR MicrosoftML의 업데이트 된 버전을 사용 하 여 R 지원의 다음 세대 및 다른 라이브러리 2016에 도입 합니다. 

Azure SQL Database에서 [Machine Learning 서비스 (R)을 통한]((https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-r)) 현재 공개 미리 보기로 제공 됩니다.

Machine Learning 서비스의 핵심 가치 제안을 소수 자릿수 및 계산 및 처리, 데이터 상주를 제공 하는 기능에 대 한 고급 분석을 제공 하는 엔터프라이즈 R 및 Python 패키지의 기능에서 데이터 끌어오기를 할 필요가 없습니다 네트워크입니다.

## <a name="components"></a>구성 요소

SQL Server 2017은 R과 Python을 지원합니다. 다음 표에서 구성 요소를 설명 합니다.

| 구성 요소 | Description |
|-----------|-------------|
| SQL Server 실행 패드 서비스 | 외부 R 및 Python 런타임 및 데이터베이스 엔진 인스턴스 간 통신을 관리 하는 서비스입니다. |
| R 패키지 | [**RevoScaleR** ](r/revoscaler-overview.md) 가장 널리 사용 되는이 라이브러리의 확장 가능한 R. 함수는 주 라이브러리입니다. 데이터 변환 및 조작, 통계 요약, 시각화 및 모델링 및 분석의 다양 한 형태는 이러한 라이브러리에 있습니다. 또한 이러한 라이브러리의에서 함수에 병렬 처리를 조정 및 계산 엔진에 의해 관리 되는 데이터의 청크에서 작동 하는 기능에 대 한 사용 가능한 코어에서 워크 로드를 자동으로 배포 합니다.  <br/>[**MicrosoftML (R)** ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 텍스트 분석, 이미지 분석 및 감정 분석에 대 한 사용자 지정 모델을 만드는 기계 학습 알고리즘을 추가 합니다. <br/>[**sqlRUtils** ](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md) , T-SQL 저장 프로시저에 R 스크립트를 배치 하 고, 데이터베이스와 함께 저장된 프로시저를 등록 하 고, R 개발 환경에서 저장된 프로시저를 실행 하는 것에 대 한 도우미 함수를 제공 합니다.<br/>[**olapR** ](r/how-to-create-mdx-queries-using-olapr.md) 작성 또는 MDX 쿼리를 R 스크립트에서 실행 됩니다.|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open) 은 Microsoft의 오픈 소스 분산은 R입니다. 패키지 및 인터프리터를 포함 됩니다. 항상 설치 프로그램으로 설치 MRO의 버전을 사용 합니다. |
| R 도구 | R 콘솔 창 및 명령 프롬프트를 R 배포에 표준 도구 이며  |
| R 샘플 및 스크립트 |  오픈 소스 R 및 RevoScaleR 패키지 만들기 및 미리 설치 된 데이터를 사용 하 여 스크립트를 실행할 수 있도록 기본 제공 데이터 집합을 포함 합니다. |
| Python 패키지 | [**revoscalepy** ](python/what-is-revoscalepy.md) 데이터 조작, 변환, 시각화 및 분석에 대 한 함수를 사용 하 여 확장 가능한 Python 주 라이브러리입니다. <br/>[**(Python) microsoftml** ](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 텍스트 분석, 이미지 분석 및 감정 분석에 대 한 사용자 지정 모델을 만드는 기계 학습 알고리즘을 추가 합니다.  |
| Python 도구 | 기본 제공 Python 명령줄 도구는 임시 테스트 및 작업에 유용 합니다.  |
| Anaconda | Anaconda는 Python 및 필수 패키지를 오픈 소스 배포 됩니다. |
| Python 샘플 및 스크립트 | R에서와 마찬가지로 Python 기본 제공 데이터 집합 및 스크립트를 포함 합니다.  |
| R 및 Python에서 미리 학습 된 모델 | 미리 학습 된 모델은 특정 사용 사례에 대 한 생성 되 고 microsoft 데이터 과학 엔지니어링 팀에서 유지 관리 합니다. 으로 미리 학습 된 모델을 사용할 수 있습니다-텍스트에서 양수 음수가 감정 점수 매기기 또는 기능에서 제공 하는 새 데이터 입력을 사용 하 여 이미지를 검색 하는 것입니다. 모델은 Machine Learning 서비스에서 실행 되지만 SQL Server 설치 프로그램을 통해 설치할 수 없습니다. 자세한 내용은 [설치 미리 학습 된 기계 학습 모델 SQL Server에서](install/sql-pretrained-models-install.md)합니다. |

## <a name="using-sql-mls"></a>SQL MLS를 사용 하 여

개발자 및 분석가 로컬 SQL Server 인스턴스를 기반으로 실행 되는 코드에 있는 경우가 많습니다. SQL Server 형식에서 R 및 Python 코드를 실행 하는 기능을 얻게 Machine Learning 서비스를 추가 하 고 외부 스크립트 실행을 사용 하도록 설정 하 여: 저장된 프로시저에서 스크립트를 래핑, SQL Server 테이블에 모델을 저장 또는 T-SQL 및 R 또는 Python 함수를 결합 합니다. 쿼리에서 합니다.

데이터 보안 모델의 경계 내에서 스크립트 실행이: 관계형 데이터베이스에 대 한 권한이 스크립트에 대 한 데이터 액세스의 기반이 됩니다. R 또는 Python 스크립트를 실행 하는 사용자는 SQL 쿼리를 해당 사용자가 액세스할 수 없습니다는 모든 데이터를 사용할 수 없습니다. 표준 데이터베이스 읽기 및 쓰기 권한, 외부 스크립트를 실행 하는 추가 권한이 필요 합니다. 모델 및 관계형 데이터에 대 한 작성 하는 코드는 저장된 프로시저에서 래핑된 이진 형식으로 직렬화 및 테이블에 저장 또는 파일로 원시 바이트 스트림으로 직렬화 하는 경우 디스크에서 로드 합니다.

데이터베이스 내 분석에 대 한 가장 일반적인 방법은 사용 하는 것 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), R 또는 Python 스크립트를 입력된 매개 변수로 전달 합니다.

기존 클라이언트-서버 상호 작용은 또 다른 방법은. IDE에 있는 모든 클라이언트 워크스테이션에서 설치할 수 있습니다 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) 또는 [Python 라이브러리](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter), 한 다음 실행을 푸시하는 코드 작성 (라고는 *원격 계산 상황에 맞는*) 데이터 및 원격 SQL Server에는 작업입니다. 

마지막으로 사용 하는 경우는 [독립 실행형 서버](r/r-server-standalone.md) 및 Developer 버전에서는 동일한 라이브러리 및 인터프리터를 사용 하 여 클라이언트 워크스테이션에서 솔루션을 구축 하 고 다음 SQL Server Machine Learning에서 프로덕션 코드를 배포할 수 있습니다 Services (In-database)입니다. 

## <a name="how-to-get-started"></a>시작 하는 방법

### <a name="step-1-install-the-software"></a>1 단계: 소프트웨어를 설치 합니다.

+ [SQL Server Machine Learning Services (In-database)](install/sql-machine-learning-services-windows-install.md)
 
### <a name="step-2-configure-a-development-tool"></a>2 단계: 구성 하는 개발 도구

데이터 과학자가 일반적으로 사용 하 여 R 또는 Python 자신의 랩톱 또는 개발 워크스테이션에서 데이터를 탐색 하 고 빌드, 우수한 예측 모델이 될 때까지 예측 모델을 조정 하 합니다. SQL Server에서 데이터베이스 내 분석을 사용 하 여이 프로세스를 변경할 필요가 없습니다 있습니다. 설치를 완료 한 후에 로컬 및 원격으로 SQL Server에서 R 또는 Python 코드를 실행할 수 있습니다.

![rsql_keyscenario2](r/media/rsql-keyscenario2.png) 

+ **원하는 IDE를 사용 하 여**입니다. 원하는 개발 도구에는 R 및 Python 라이브러리를 연결할 수 있습니다. 자세한 내용은 [R 도구 설정](r/set-up-a-data-science-client.md) 하 고 [Python 도구 설정](python/setup-python-client-tools-sql.md)합니다.  

+ **원격 또는 로컬로 작업**합니다. 데이터 과학자는 SQL Server에 연결 하 고 클라이언트 로컬 분석을 위해 일반적으로 가져올 수 있습니다. 그러나 더 나은 방법은 사용 하는 **RevoScaleR** 또는 **revoscalepy** 비용이 많이 들고 안전 하지 않은 데이터 이동을 방지할 SQL Server 컴퓨터에 계산 푸시 Api.

+ **SQL Server 저장 프로시저에 R 또는 Python 스크립트를 포함할**합니다. 코드를 완전히 최적화 하는 경우 불필요 한 데이터 이동을 방지 하 고 데이터 처리 작업을 최적화 하는 저장된 프로시저에 래핑하십시오.

### <a name="step-3-write-your-first-script"></a>3 단계: 첫 번째 스크립트를 작성 합니다.

T-SQL 스크립트 내에서 R 또는 Python 함수를 호출 합니다.

+ [R: R을 사용 하 여 데이터베이스 내 분석에 알아봅니다](tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [R: R 사용 하 여 종단 간 연습](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
+ [Python: T-SQL을 사용하여 Python 실행](tutorials/run-python-using-t-sql.md)
+ [Python: Python을 사용 하 여 데이터베이스 내 분석에 알아봅니다](tutorials/sqldev-in-database-python-for-sql-developers.md)

작업을 위한 최상의 언어를 선택 합니다. R은 SQL을 사용 하 여 구현 하기 어려운 통계적 계산에 적합 합니다. 데이터 집합 기반 작업에 대 한 최대 성능을 얻기 위해 SQL Server의 기능을 활용 합니다. 열에 대해 매우 빠른 계산에 대 한 메모리 내 데이터베이스 엔진을 사용 합니다.

### <a name="step-4-optimize-your-solution"></a>4 단계: 솔루션을 최적화

모델이 엔터프라이즈 데이터의 크기를 조정 하는 준비 되 면 데이터 과학자는 종종 같은 프로세스를 최적화 하기 위해 DBA 또는 SQL 개발자를 사용 하 여 작동 합니다.

+ 기능 엔지니어링
+ 데이터 수집 및 데이터 변환
+ 점수 매기기

일반적으로 큰 데이터 집합을 사용 하는 경우에 특히 데이터 과학자가 R을 사용 하 여 성능 및 확장성 문제가 되었습니다. 이것은 공용 런타임 구현이 단일 스레드 이며 로컬 컴퓨터에서 사용 가능한 메모리에 맞는 데이터 집합만 수용할 수 있습니다. 더 많은 데이터를 사용 하 여 성능 향상을 위해 여러 기능을 제공 하는 SQL Server Machine Learning Services와 통합:

+ **RevoScaleR**:이 R 패키지에 병렬 처리 및 확장성을 제공 하도록 다시 설계 된 가장 인기 있는 R 함수 중 일부는 구현이 포함 되어 있습니다. 패키지는 또한 훨씬 큰 메모리와 계산력 일반적으로 SQL Server 컴퓨터에 계산을 푸시하여 성능과 확장을 더 증대 하는 함수를 포함 합니다.

+ **revoscalepy**합니다. 이 Python 라이브러리 RevoScaleR의 원격 계산 컨텍스트 등 가장 인기 있는 기능을 구현 및 지 원하는 많은 알고리즘 분산 처리 합니다.

이 성능에 대 한 자세한 내용은 참조 [성능 사례 연구](r/performance-case-study-r-services.md) 하 고 [R 및 데이터 최적화](r/r-and-data-optimization-r-services.md)합니다.

### <a name="step-5-deploy-and-consume"></a>5 단계: 배포 및 사용

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
| SQL Server 2017 Machine Learning Services (In-database) | R Server 9.2.1 <br/> Python 서버 9.2 | 2017년 10월 |
| SQL Server 2017 Machine Learning Server (독립 실행형) | R Server 9.2.1 <br/> Python 서버 9.2 | 2017년 10월 |
| SQL Server 2016 R Services (In-database) | R Server 9.1의 경우  | 2017 년 7 월  |
| SQL Server 2016 R Server (독립 실행형)  |  R Server 9.1의 경우 | 2017 년 7 월 |

릴리스에서 패키지 버전을 버전에 매핑할을 참조 하세요 [업그레이드 하는 R 및 Python 구성 요소](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md#version-map)합니다.

## <a name="portability-and-related-products"></a>이식성 및 관련된 제품

사용자 지정 R 및 Python 코드의 이식성은 패키지 배포 및 여러 제품에 내장 된 인터프리터를 통해 처리 됩니다. SQL Server에서 제공 되는 동일한 패키지도 다른 여러 Microsoft 제품 및 서비스를 호출 하는 SQL이 아닌 버전을 포함 하 여에서 사용할 수 있습니다 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/)합니다. 

R 및 Python 인터프리터를 포함 하는 무료 클라이언트가 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) 하며 [Python 라이브러리](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)합니다.

Azure에서 Microsoft R 및 Python 패키지 및 인터프리터에서 사용할 수 있습니다 Azure Machine Learning 및 Azure 서비스와 같은 [HDInsight](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-on-azure-hdinsight), 및 [Azure virtual machines](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux)합니다. 합니다 [데이터 과학 Virtual Machine](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/) 여러 공급 업체와 라이브러리 도구 및 Microsoft에서 인터프리터를 사용 하 여 준비를 모두 갖추게 개발 워크스테이션을 포함 합니다.

## <a name="see-also"></a>참고자료

[SQL Server Machine Learning 서비스 설치](install/sql-machine-learning-services-windows-install.md)