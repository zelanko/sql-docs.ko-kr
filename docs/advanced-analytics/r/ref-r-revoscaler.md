---
title: RevoScaleR R 함수 라이브러리
description: SQL Server 2016 R Services에서 RevoScaleR 함수 라이브러리를 소개 하 고 R을 사용 하 여 Machine Learning Services SQL Server 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b5dcd2f14d1a1d8e23a62be299b1ff6f41814041
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715062"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR (SQL Server의 R 라이브러리)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**RevoScaleR** 은 Microsoft의 고성능 데이터 과학 함수 라이브러리입니다. 함수는 데이터 가져오기, 데이터 변환, 요약, 시각화 및 분석을 지원 합니다.

기본 R 함수와 달리 매우 큰 데이터 집합, 병렬 및 분산 파일 시스템에 대해 RevoScaleR 작업을 수행할 수 있습니다. 함수는 청크를 사용 하 여 메모리에 맞지 않는 데이터 집합에 대해 작동 하 고 작업이 완료 되 면 결과를 reassembling 수 있습니다.

RevoScaleR 함수는 쉽게 식별할 수 있도록 **rx** 또는 **rx** 접두사로 표시 됩니다.

RevoScaleR는 분산 데이터 과학을 위한 플랫폼 역할을 합니다. 예를 들어 [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)의 최신 알고리즘을 사용 하 여 RevoScaleR 계산 컨텍스트 및 변환을 사용할 수 있습니다. [Rxexec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) 를 사용 하 여 기본 R 함수를 병렬로 실행할 수도 있습니다.

## <a name="full-reference-documentation"></a>전체 참조 설명서

**RevoScaleR** 라이브러리는 여러 Microsoft 제품에 배포 되지만, SQL Server 또는 다른 제품에 라이브러리를 가져올 때 사용 됩니다. 함수는 동일 하기 때문에 [개별 RevoScaleR 함수에 대 한 설명서](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 는 Microsoft Machine Learning Server에 대 한 [R 참조](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 의 한 위치에만 게시 됩니다. 제품별 동작이 있는 경우 함수 도움말 페이지에 차이점이 표시 됩니다.

## <a name="versions-and-platforms"></a>버전 및 플랫폼

**RevoScaleR** 라이브러리는 R 3.4.3를 기반으로 하며 다음 Microsoft 제품 또는 다운로드 중 하나를 설치 하는 경우에만 사용할 수 있습니다.

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 컴퓨터 학습 서비스](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 이상](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R 클라이언트](set-up-a-data-science-client.md)

> [!NOTE]
> 전체 제품 릴리스 버전은 SQL Server 2017부터 Windows 전용입니다. **RevoScaleR** 에 대 한 Linux 지원은 [SQL Server 2019 미리 보기](../../linux/sql-server-linux-setup-machine-learning.md)의 새로운 기능입니다.

## <a name="functions-by-category"></a>범주별 함수

이 섹션에서는 각 함수를 사용 하는 방법에 대 한 아이디어를 제공 하기 위해 범주별로 함수를 나열 합니다. [목차](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 를 사용 하 여 알파벳 순서로 함수를 찾을 수도 있습니다.

## <a name="1-data-source-and-compute"></a>1-데이터 원본 및 계산

**RevoScaleR** 에는 데이터 원본을 만들고 계산이 수행 되는 위치 또는 *계산 컨텍스트*를 설정 하는 함수가 포함 되어 있습니다. 데이터 원본 개체는 원하는 데이터 집합과 함께 연결 문자열을 지정하는 컨테이너로서, 테이블, 뷰 또는 쿼리로 정의됩니다. 저장 프로시저 호출은 지원되지 않습니다. SQL Server 시나리오와 관련 된 함수는 아래 표에 나와 있습니다.

경우에 따라 SQL Server와 R은 다른 데이터 형식을 사용 합니다. SQL 및 R 데이터 형식 간의 매핑 목록은 [R-sql 데이터 형식](r-libraries-and-data-types.md)을 참조 하세요.

| 함수| 설명|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  계산 컨텍스트 개체 SQL Server 만들어 원격 인스턴스에 계산을 푸시합니다. 여러 **RevoScaleR** 함수는 계산 컨텍스트를 인수로 사용 합니다. |
|[Rxget, Econtext/Rxset이상 컨텍스트](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | 활성 계산 컨텍스트를 가져오거나 설정 합니다. |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | SQL Server 쿼리나 테이블을 기반으로 데이터 개체를 만듭니다. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | ODBC 연결을 기반으로 데이터 원본을 만듭니다. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | 로컬 XDF 파일을 기반으로 데이터 원본을 만듭니다. XDF 파일은 종종 메모리 내 데이터를 디스크로 오프 로드 하는 데 사용 됩니다. XDF 파일은 한 일괄 처리의 데이터베이스에서 전송 될 수 있는 것 보다 더 많은 데이터를 사용 하거나 메모리에 포함할 수 있는 것 보다 많은 데이터를 사용할 때 유용할 수 있습니다. 예를 들어 데이터베이스를 각 R 작업에 대해 반복적으로 쿼리 하는 대신 데이터베이스에서 로컬 워크스테이션으로 데이터를 정기적으로 이동 하는 경우 XDF 파일을 일종의 캐시로 사용 하 여 데이터를 로컬로 저장 한 다음 R 작업 영역에서 사용할 수 있습니다.|

> [!TIP]
> 데이터 원본 또는 계산 컨텍스트의 아이디어를 처음 접하는 경우 Microsoft Machine Learning Server 설명서에서 [분산 컴퓨팅](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) 을 시작 하는 것이 좋습니다.

### <a name="perform-ddl-statements"></a>DDL 문 수행

인스턴스 및 데이터베이스에 대 한 필요한 권한이 있는 경우 R에서 DDL 문을 실행할 수 있습니다. 다음 함수는 ODBC 호출을 사용 하 여 DDL 문을 실행 하거나 데이터베이스 스키마를 검색 합니다.

| 함수| 설명|
| ------- | ---------- |
| [rxSqlServerTableExists 및 rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 테이블을 삭제 하거나 데이터베이스 테이블이 나 개체가 있는지 확인 합니다. |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | 데이터베이스 개체를 정의 하거나 조작 하는 DDL (데이터 정의 언어) 명령을 실행 합니다. 이 함수는 데이터를 반환할 수 없으며 개체 스키마 또는 메타 데이터를 검색 하거나 수정 하는 데만 사용 됩니다.|

## <a name="2-data-manipulation-etl"></a>2-데이터 조작 (ETL)

데이터 원본 개체를 만든 후 개체를 사용 하 여 데이터를 로드 하거나, 데이터를 변환 하거나, 지정 된 대상에 새 데이터를 쓸 수 있습니다. 원본의 데이터 크기에 따라 일괄 처리 크기를 데이터 원본의 일부로 정의하고 데이터를 청크로 이동할 수도 있습니다.

| 함수 | 설명 |
|----------|-------------|
| [rxOpen 메서드](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | 데이터 원본을 사용할 수 있는지 확인 하 고, 데이터 원본을 열거나 닫고, 원본에서 데이터를 읽고, 대상에 데이터를 쓰고, 데이터 원본을 닫습니다.|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | 데이터 원본에서 파일 저장소 또는 데이터 프레임으로 데이터를 이동 합니다.|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | 데이터를 데이터 원본 간에 이동 하는 동안 데이터를 변환 합니다.|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3-그래프 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |데이터에서 히스토그램을 만듭니다. | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |데이터에서 선 플롯을 만듭니다. | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |그릴 수 있는 로렌츠 곡선을 계산 합니다. | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |실제 데이터와 예측 데이터에서 ROC 곡선을 계산 하 고 플롯 합니다. | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4-설명 통계

| 함수 이름 | 설명 |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |는 정렬 하지 않고 .xdf 파일 및 데이터 프레임에 대 한 대략적인 변 위치 계산 합니다. | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |그룹별 계산을 포함 하 여 데이터의 기본 요약 통계입니다. .Xdf 파일에 대 한 그룹 계산으로 쓰기가 지원 되지 않습니다. | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |데이터의 수식 기반 교차 집계. | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |큐브 결과를 반환 하는 효율적인 표현 용으로 설계 된 대체 수식 기반 교차 집계. . Xdf 파일에 출력을 쓰는 것은 지원 되지 않습니다. | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |교차 tabulations의 한계 요약. | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |교차 집계 결과를 xtabs 개체로 변환 합니다. | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Xtabs 개체에 대해 카이 제곱 테스트를 수행 합니다. 작은 데이터 집합에 사용 되며 데이터를 청크 하지 않습니다. | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Xtabs 개체에 대해 피셔의 정확한 테스트를 수행 합니다. 작은 데이터 집합에 사용 되며 데이터를 청크 하지 않습니다. | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Xtabs 개체를 사용 하 여 Kendall의 타우 Rank 상관 계수를 계산 합니다. | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |Xtabs 개체의 행 및 열 쌍 조합에 함수를 적용 합니다. | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |두 개의 xtabs 개체에서 상대 위험을 계산 합니다. | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |두 개-두 개의 xtabs 개체에 대 한 비 확률 비율을 계산 합니다. | 

<sup>*</sup>이 범주에서 가장 인기 있는 함수를 나타냅니다.

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5-예측 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |선형 모델을 데이터에 맞춥니다. | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |로지스틱 회귀 모델을 데이터에 맞춥니다. | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |일반화 된 선형 모델을 데이터에 맞춥니다. | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |변수 집합에 대 한 제곱/교차곱 행렬의 공 분산, 상관 관계 또는 합계를 계산 합니다. | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |분류 또는 회귀 트리를 데이터에 맞춥니다. | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |추계 그라데이션 부스트 알고리즘을 사용 하 여 분류 또는 회귀 의사 결정 포리스트를 데이터에 맞춥니다. | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |분류 또는 회귀 의사 결정 포리스트를 데이터에 맞춥니다. | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |피팅 모델에 대 한 예측을 계산 합니다. 출력은 XDF 데이터 원본 이어야 합니다. | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |K를 의미 하는 클러스터링을 수행 합니다. | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |Naive Bayes 분류를 수행 합니다. | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |변수 집합에 대 한 공변성 행렬을 계산 합니다. | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |변수 집합에 대 한 상관 관계 행렬을 계산 합니다. | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |변수 집합에 대 한 제곱합/교차곱 행렬의 합계를 계산 합니다. | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |이진 분류자 시스템에서 실제 및 예측 값을 사용 하 여 ROC (Receiver 운영 특징) 계산 | 

<sup>*</sup>이 범주에서 가장 인기 있는 함수를 나타냅니다.


## <a name="how-to-work-with-revoscaler"></a>RevoScaleR로 작업 하는 방법

**RevoScaleR** 의 함수는 저장 프로시저에서 캡슐화 된 R 코드에서 호출할 수 있습니다. 대부분의 개발자는 **RevoScaleR** 솔루션을 로컬로 빌드한 다음 배포 연습으로 완료 된 R 코드를 저장 프로시저로 마이그레이션합니다.

로컬로 실행 하는 경우 일반적으로 명령줄 또는 R 개발 환경에서 R 스크립트를 실행 하 고 **RevoScaleR** 함수 중 하나를 사용 하 여 SQL Server 계산 컨텍스트를 지정 합니다. 전체 코드 또는 개별 함수에 대 한 원격 계산 컨텍스트를 사용할 수 있습니다. 예를 들어 최신 데이터를 사용 하 고 데이터 이동을 방지 하기 위해 모델 학습을 서버에 오프 로드할 수 있습니다.

[Sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)저장 프로시저 내에서 R 스크립트를 캡슐화 할 준비가 되 면 명확 하 게 정의 된 입력 및 출력을 포함 하는 단일 함수로 코드를 다시 작성 하는 것이 좋습니다. 

## <a name="see-also"></a>참조

+ [R 자습서](../tutorials/sql-server-r-tutorials.md)
+ [계산 컨텍스트 사용 방법 알아보기](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [SQL 개발자를 위한 R: 모델 학습 및 운영](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub의 Microsoft 제품 샘플](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 참조 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
