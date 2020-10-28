---
title: Jupyter Notebook 및 Azure Data Studio를 사용하여 BDC(빅 데이터 클러스터) 작업을 수행하는 일반적인 시나리오
titleSuffix: SQL Server Big Data Clusters
description: SQL Server 2019 빅 데이터 클러스터에서 Jupyter Notebook 및 Azure Data Studio를 사용하여 BDC 작업을 수행하는 일반적인 시나리오입니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 99e62be597e4ce08d38db199116f1bd4d5ab33f6
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378486"
---
# <a name="common-notebooks-for-sql-server-big-data-clusters"></a>SQL Server 빅 데이터 클러스터용 일반 Notebook

이 문서에는 SQL Server 빅 데이터 클러스터용 Notebook이 나열되어 있습니다. 이러한 실행 가능 Notebook(.ipynb)은 빅 데이터 클러스터에서 일반적인 시나리오를 표시하는 데 도움이 되도록 SQL Server 2019용으로 설계되었습니다.

각 Notebook은 자체 종속성을 확인하도록 설계되었습니다. **모든 셀 실행** 옵션은 성공적으로 완료되거나 예외가 발생하며 누락된 종속성을 해결하기 위한 다른 Notebook에 대한 하이퍼링크 힌트를 제공합니다. 후속 Notebook에 대한 힌트 하이퍼링크를 따라 이동하여 **모든 셀 실행** 을 누르고, 성공하면 원래 Notebook으로 돌아가서 **모든 셀 실행** 을 다시 누릅니다.

모든 종속성이 설치되었지만 **모든 셀 실행** 이 실패한 경우 각 Notebook은 결과를 분석하고 가능한 경우 다른 Notebook에 대한 하이퍼링크 힌트를 생성하여 문제 해결을 추가로 지원합니다.

## <a name="gathering-logs-from-big-data-cluster-bdc"></a>BDC(빅 데이터 클러스터)에서 로그 수집

이 섹션의 Notebook은 클러스터의 로그인 및 로그아웃처럼 다른 Notebook의 필수 구성 요소로 사용됩니다.

|Name |설명 |
|---|---|
|SOP005 - az login|az 명령줄 인터페이스를 사용하여 Azure에 로그인합니다. |
|SOP006 - az logout|az 명령줄 인터페이스를 사용하여 Azure에서 로그아웃합니다.|
|SOP007 - 버전 정보(azdata, bdc, kubernetes)|Notebook에서 버전 관리 정보에 사용되는 도우미 함수를 정의합니다.|
|SOP011 - kubernetes 구성 컨텍스트 설정|사용할 kubernetes 구성을 설정합니다. |
|SOP028 - azdata 로그인|azdata 명령줄 인터페이스를 사용하여 빅 데이터 클러스터에 로그인합니다. |
|SOP033 - azdata logout|azdata 명령줄 인터페이스를 사용하여 빅 데이터 클러스터에서 로그아웃합니다. |
|SOP034 - BDC가 정상 상태가 될 때까지 대기|빅 데이터 클러스터가 정상 상태이거나 지정된 제한 시간이 만료될 때까지 차단합니다. min_pod_count 매개 변수는 클러스터에 이 개수 이상의 Pod가 있을 때까지 상태 검사를 통과하지 않음을 나타냅니다. 기존 Pod가 이 제한을 초과하여 비정상 상태인 경우 클러스터는 정상 상태가 아닙니다.|
|OPR001 - App-Deploy 만들기|빅 데이터 클러스터에서 앱을 만들려면 이 Notebook을 사용합니다. |
|OPR002 - App-Deploy 실행|빅 데이터 클러스터에서 앱을 실행하려면 이 Notebook을 사용합니다. |
|OPR003 - CronJob 만들기|빅 데이터 클러스터에서 CronJob을 만들려면 이 Notebook을 사용합니다. |
|OPR004 - CronJob 일시 중단|빅 데이터 클러스터에서 CronJob을 일시 중단하려면 이 Notebook을 사용합니다. |
|OPR005 - CronJob 다시 시작|빅 데이터 클러스터에서 CronJob을 다시 시작하려면 이 Notebook을 사용합니다. |
|OPR006 - CronJob 삭제|빅 데이터 클러스터에서 CronJob을 삭제하려면 이 Notebook을 사용합니다. |
|OPR007 - App-Deploy 삭제|빅 데이터 클러스터에서 앱을 삭제하려면 이 Notebook을 사용합니다. |
|OPR100 - Notebook 배포 및 예약|App-Deploy Pod에 Notebook 목록을 배포하고, Kubernetes CronJob을 사용하여 일정에 따라 App-Deploy를 실행하고, 결과를 볼 Grafana 대시보드를 설치하려면 이 Notebook을 사용합니다.|
|OPR600 - 인프라 모니터링(Kubernetes)|인프라를 모니터링하려면 이 Notebook을 사용합니다.|
|OPR700 - App-Deploy 애플리케이션용 Grafana 대시보드 만들기|Grafana에 대시보드를 만들어 App-Deploy 결과를 모니터링하고 카나리아 또는 애플리케이션이 실패하는 경우 경고를 생성하려면 이 Notebook을 사용합니다.|
|OPR900 - App-Deploy 실행 문제 해결|kubectl 실행 파일을 사용하여 컨테이너에서 직접 App-Deploy 스크립트를 실행하려면 이 Notebook을 사용합니다. 그러면 문제 해결을 위해, 특히 스크립트 시작 단계의 문제와 관련하여 더 많은 디버깅 정보를 제공할 수 있습니다.|
|OPR901 - CronJob 문제 해결|kubectl 실행 파일을 사용하여 컨테이너에서 직접 CronJob 스크립트를 실행하려면 이 Notebook을 사용합니다. 그러면 문제 해결을 위해 보다 자세한 디버깅 정보를 제공할 수 있습니다.|


## <a name="analyze-logs-from-big-data-clusters-bdc"></a>BDC(빅 데이터 클러스터)에서 로그 분석

SQL Server 빅 데이터 클러스터 시나리오를 보여 주는 예제 Notebook 세트입니다.

|Name |설명 |
|---|---|
|SAM001a - SQL Server 마스터 풀에서 스토리지 풀 쿼리(1/3) - 샘플 데이터 로드|이 3부 자습서에서는 azdata를 사용하여 스토리지 풀(HDFS)에 데이터를 로드하고, Spark를 사용하여 Parquet으로 변환합니다.세 번째 부분에서는 마스터 풀(SQL Server)을 사용하여 데이터를 쿼리합니다. |
|SAM001b - SQL Server 마스터 풀에서 스토리지 풀 쿼리(2/3) - 데이터를 parquet으로 변환|이 3부 자습서의 두 번째 부분에서 Spark를 사용하여 .csv 파일을 parquet 파일로 변환합니다.|
|SAM001c - SQL Server 마스터 풀에서 스토리지 풀 쿼리(3/3) - SQL Server에서 HDFS 쿼리|이 스토리지 풀 자습서의 세 번째 부분에서는 빅 데이터 클러스터에서 HDFS 데이터를 가리키는 외부 테이블을 만들고 이 데이터를 마스터 인스턴스의 고가치 데이터와 조인하는 방법을 알아봅니다.|
|SAM002 - 스토리지 풀(2/2) - HDFS 쿼리|이 스토리지 풀 자습서의 두 번째 부분에서는 빅 데이터 클러스터에서 HDFS 데이터를 가리키는 외부 테이블을 만들고 이 데이터를 마스터 인스턴스의 고가치 데이터와 조인하는 방법을 알아봅니다.|
|SAM003 - 데이터 풀 예제|이 자습서에서는 데이터 풀에서 데이터 풀 원본 및 외부 테이블을 만든 다음 데이터 풀 테이블에 데이터를 삽입하고 데이터 풀 테이블 간에 데이터를 로드하는 방법에 대해 알아봅니다. 데이터 풀 테이블의 데이터를 다른 데이터 풀 테이블과 조인하여 테이블 자르기 및 정리도 수행합니다. |
|SAM004 - MongoDB의 데이터 가상화|MongoDB 외부 데이터 원본의 데이터를 쿼리하려면 해당 외부 데이터를 참조하는 외부 테이블을 만들어야 합니다. 이 섹션에서는 이러한 외부 테이블을 만들기 위한 샘플 코드를 제공합니다.|
|SAM005 - Oracle의 데이터 가상화|Oracle 외부 데이터 원본의 데이터를 쿼리하려면 해당 외부 데이터를 참조하는 외부 테이블을 만들어야 합니다. 이 섹션에서는 이러한 외부 테이블을 만들기 위한 샘플 코드를 제공합니다.|
|SAM006 - SQL Server의 데이터 가상화|다른 SQL Server 데이터 원본의 데이터를 가상으로 쿼리하려면 외부 데이터를 참조하는 외부 테이블을 만들어야 합니다. 이 섹션에서는 이러한 외부 테이블을 만들기 위한 샘플 코드를 제공합니다.|
|SAM007 - Teradata의 데이터 가상화|Teradata 외부 데이터 원본의 데이터를 쿼리하려면 해당 외부 데이터를 참조하는 외부 테이블을 만들어야 합니다. 이 섹션에서는 이러한 외부 테이블을 만들기 위한 샘플 코드를 제공합니다.|
|SAM008 - azdata를 사용하는 Spark|azdata 및 kubectl 명령을 사용하여 Spark 세션 작업을 수행합니다.|
|SAM009 - azdata를 사용하는 HDFS|azdata 및 kubectl 명령을 사용하여 HDFS 작업을 수행합니다.|
|SAM010 - azdata를 사용하는 앱|azdata 및 kubectl 명령을 사용하여 App-Deploy 작업을 수행합니다. |

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
