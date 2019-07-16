---
title: RevoScaleR R 함수 라이브러리-SQL Server Machine Learning 서비스
description: SQL Server 2016 R Services 및 R. 사용 하 여 SQL Server 2017 Machine Learning Services의 RevoScaleR 함수 라이브러리 소개
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: d0691508ff3be52a4af744c1167ca799f8d23050
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962482"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR (SQL Server의 R 라이브러리)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**RevoScaleR** Microsoft의 고성능 데이터 과학 함수 라이브러리입니다. 함수는 데이터 가져오기, 데이터 변환, 요약, 시각화 및 분석을 지원 합니다.

기본 R 함수, 달리 RevoScaleR 작업 분산된 파일 시스템에서 동시에 매우 큰 데이터 집합에 대해 수행할 수 있습니다. 함수에에서 맞지 않는 메모리 청크를 사용 하 고 다시 어셈블하기 때문 결과 여 작업이 완료 되는 데이터 집합을 통해 작동할 수 있습니다.

RevoScaleR 함수는 표시 되는 **rx** 또는 **Rx** 접두사를 쉽게 식별할 수 있도록 합니다.

RevoScaleR 분산된 데이터 과학을 위한 플랫폼으로 사용 됩니다. 예를 들어 사용할 수 있습니다 RevoScaleR 계산 컨텍스트 및 변환에서의 최신 알고리즘을 사용 하 여 [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)합니다. 사용할 수도 있습니다 [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) 기본 R 함수를 병렬로 실행 합니다.

## <a name="full-reference-documentation"></a>전체 참조 설명서

합니다 **RevoScaleR** 라이브러리는 여러 Microsoft 제품을 배포 하지만 SQL Server 또는 다른 제품에서 라이브러리를 표시 하는지 여부를 사용량은 동일 합니다. 함수는 동일 하므로 [개별 RevoScaleR 함수에 대 한 설명서](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 아래에 있는 하나의 위치에 게시 되는 [R 참조](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) Microsoft Machine Learning Server에 대 한 합니다. 모든 제품별 해야 동작 존재, 불일치 함수 도움말 페이지에 표시 됩니다.

## <a name="versions-and-platforms"></a>버전 및 플랫폼

합니다 **RevoScaleR** 라이브러리 이며 R 3.4.3에 따라 사용 가능한 다음 Microsoft 제품 또는 다운로드 중 하나를 설치 하는 경우에:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning 서비스](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 이상](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> 전체 제품 릴리스 버전은 Windows 전용 SQL Server 2017을 사용 하 여 시작 합니다. 에 대 한 Linux 지원을 **RevoScaleR** 의 새로운 [SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md)합니다.

## <a name="functions-by-category"></a>범주별으로 함수

이 섹션에서는 범주를 각각 사용 하는 방법의 아이디어를 제공 하 여 함수를 나열 합니다. 사용할 수도 있습니다는 [목차](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 알파벳 순서로 함수를 찾으려고 합니다.

## <a name="1-data-source-and-compute"></a>1-데이터 원본 및 계산

**RevoScaleR** 데이터 원본을 만들고 위치를 설정 하기 위한 함수가 포함 됩니다 또는 *계산 컨텍스트*, 계산이 수행 되는 중입니다. 데이터 원본 개체는 원하는 데이터 집합과 함께 연결 문자열을 지정하는 컨테이너로서, 테이블, 뷰 또는 쿼리로 정의됩니다. 저장 프로시저 호출은 지원되지 않습니다. SQL Server 시나리오와 관련 된 함수는 아래 표에 나열 됩니다.

SQL Server 및 R에 따라서는 다른 데이터 형식을 사용합니다. SQL 및 R 데이터 형식 간의 매핑 목록을 참조 하세요 [R-SQL 데이터 형식](r-libraries-and-data-types.md)합니다.

| 함수| 설명|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  푸시 계산을 원격 인스턴스를 SQL Server 계산 컨텍스트 개체를 만듭니다. 몇 가지 **RevoScaleR** 함수 인수로 계산 컨텍스트를 고려 합니다. |
|[rxGetComputeContext / rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | Get 또는 활성 계산 컨텍스트를 설정 합니다. |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | SQL Server 쿼리 또는 테이블 기반 데이터 개체를 만듭니다. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | ODBC 연결에 따라 데이터 원본을 만듭니다. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | 로컬 XDF 파일을 기반으로 데이터 원본을 만듭니다. XDF 파일을 메모리 내 데이터 디스크를 오프 로드 자주 사용 됩니다. XDF 파일을 하나의 일괄 처리를 데이터베이스에서 전송할 수 있습니다 보다 더 많은 데이터 또는 메모리에 맞출 수 있는 수보다 더 많은 데이터를 작업할 때 유용할 수 있습니다. 예를 들어, 주기적으로 이동 하면 많은 양의 데이터를 데이터베이스에서 로컬 워크스테이션, 쿼리 하는 대신 각 R 작업에 대해 반복 해 서 데이터베이스 사용할 수 있습니다 XDF 파일 캐시의 한 종류로 로컬로 데이터를 저장 하 고 다음 R 작업 영역에서 작업에.|

> [!TIP]
> 새 데이터 원본의 개념을 하거나 하는 경우 계산 컨텍스트를 시작 하는 것이 좋습니다 [분산 컴퓨팅](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) Microsoft Machine Learning Server 문서의 합니다.

### <a name="perform-ddl-statements"></a>DDL 문을 수행 합니다.

인스턴스 및 데이터베이스에 필요한 권한이 있는 경우 R에서 DDL 문을 실행할 수 있습니다. 다음 함수는 DDL 문을 실행 하거나 데이터베이스 스키마를 검색할 ODBC 호출을 사용 합니다.

| 함수| 설명|
| ------- | ---------- |
| [rxSqlServerTableExists 및 rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | 삭제는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 테이블 또는 데이터베이스 테이블 또는 개체의 존재 여부를 확인 합니다. |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | 정의 또는 데이터베이스 개체를 조작 하는 데이터 정의 언어 (DDL) 명령을 실행 합니다. 이 함수는 데이터를 반환할 수 없습니다 하 고 검색 하거나 메타 데이터를 개체 스키마 수정에 사용 됩니다.|

## <a name="2-data-manipulation-etl"></a>2-데이터 조작 (ETL)

데이터 원본 개체를 만든 후 데이터를 로드, 데이터를 변환 또는 지정된 된 대상에 새 데이터를 작성 하는 개체를 사용할 수 있습니다. 원본의 데이터 크기에 따라 일괄 처리 크기를 데이터 원본의 일부로 정의하고 데이터를 청크로 이동할 수도 있습니다.

| 함수 | 설명 |
|----------|-------------|
| [rxOpen 메서드](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | 데이터 소스는 개방적이 고 사용할 수 있는지 여부를 확인 또는 데이터 원본을 닫습니다, 그리고 원본에서 데이터 읽기, 대상에 데이터를 작성 및 데이터 원본을 닫습니다.|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | File storage로 또는 데이터 프레임으로 데이터 원본에서 데이터를 이동 합니다.|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | 데이터 원본 간에 이동 하는 동안 데이터를 변환 합니다.|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3-그래프 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |데이터에서 히스토그램을 만듭니다. | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |데이터에서 선 표시를 만듭니다. | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |그릴 수 있는 로렌츠 곡선을 계산 합니다. | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |계산 하 고 실제 및 예측 데이터에서 ROC 곡선을 표시 합니다. | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4-기술 통계

| 함수 이름 | 설명 |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |정렬 하지 않고.xdf 파일 및 데이터 프레임에 대 한 사분 위 수를 추정 하는 계산 합니다. | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |그룹별 계산을 포함 하 여 데이터의 기본 요약 통계입니다. 그룹 계산 지원 되지 않는.xdf 파일을 여 작성 합니다. | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |수식을 기반으로 교차 집계 데이터입니다. | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |대체 수식을 기반으로 교차 집계 큐브 결과 반환 하는 효율적인 표현을 위해 설계 되었습니다. 지원 되지 않는.xdf 파일에 출력을 작성 합니다. | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |교차 비용의 한계 요약 합니다. | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |Xtabs 개체로 교차 집계 결과 변환 합니다. | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Xtabs 개체에서 카이 제곱 검정을 수행합니다. 작은 데이터 집합을 사용 하 고 데이터를 청크 하지 않습니다. | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Xtabs 개체에서 피셔의 정확 하 게 테스트를 수행합니다. 작은 데이터 집합을 사용 하 고 데이터를 청크 하지 않습니다. | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Xtabs 개체를 사용 하 여 켄 달의 Tau Rank 상관 계수를 계산 합니다. | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |Xtabs 개체의 열 및 열의 쌍 조합에 함수를 적용 합니다. | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |2-2 xtabs 개체에서 상대 위험을 계산 합니다. | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |2-2 xtabs 개체에 홀수 비율을 계산 합니다. | 

<sup>*</sup> 이 범주에서 가장 인기 있는 함수를 나타냅니다.

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5-예측 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |선형 모델을 데이터에 맞춥니다. | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |로지스틱 회귀 모델을 데이터에 맞춥니다. | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |일반화 된 선형 모델을 데이터에 맞춥니다. | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |공변성 (covariance), 상관 관계 또는 제곱합 / 교차곱을 계산 변수 집합에 대 한 행렬입니다. | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |분류 또는 회귀 트리를 데이터에 맞춥니다. | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |분류 또는 회귀 의사 결정 포리스트는 추계 그라데이션 승격 알고리즘을 사용 하 여 데이터에 맞춥니다. | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |데이터 분류 또는 회귀 의사 결정 포리스트를 적합합니다. | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |맞춤된 모델에 대 한 예측을 계산합니다. 출력에는 XDF 데이터 원본에 있어야 합니다. | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |K-means 클러스터링을 수행합니다. | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |Naive Bayes 분류를 수행합니다. | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |변수 집합에 대 한 공 분산 행렬을 계산 합니다. | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |변수 집합에 대 한 상관 관계 행렬을 계산 합니다. | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |제곱합 / 교차곱 합계를 계산할 변수의 집합에 대 한 행렬입니다. | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |이진 분류자 시스템에서 실제 및 예측 값을 사용 하 여 받는 사람 ROC (Operating Characteristic) 계산 합니다. | 

<sup>*</sup> 이 범주에서 가장 인기 있는 함수를 나타냅니다.


## <a name="how-to-work-with-revoscaler"></a>RevoScaleR을 사용 하는 방법

함수가 **RevoScaleR** 저장된 프로시저에서 캡슐화 하는 R 코드에서 호출할 수 있습니다. 대부분의 개발자는 빌드할 **RevoScaleR** 솔루션을 로컬로 다음 배포 연습으로 저장된 프로시저에 완성 된 R 코드를 마이그레이션합니다.

로컬로 실행할 때 일반적으로 R 개발 환경 또는 명령줄에서 R 스크립트를 실행 및 중 하나를 사용 하 여 SQL Server 계산 컨텍스트를 지정 합니다 **RevoScaleR** 함수입니다. 전체 코드의 경우 또는 개별 함수에 대 한 원격 계산 컨텍스트를 사용할 수 있습니다. 예를 들어 다음 모델 학습 최신 데이터를 사용 하 고 데이터 이동을 방지 하기 위해 서버를 오프 로드 하는 것이 좋습니다.

저장된 프로시저 내에서 R 스크립트를 캡슐화 할 준비가 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), 입력 및 출력에 명확 하 게 정의한 단일 함수로 코드를 다시 작성 하는 것이 좋습니다. 

## <a name="see-also"></a>참조

+ [R 자습서](../tutorials/sql-server-r-tutorials.md)
+ [계산 컨텍스트를 사용 하는 방법을 알아봅니다](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [SQL 개발자를 위한 R: 학습 및 모델 운영](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub의 Microsoft 제품 샘플](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 참조 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
