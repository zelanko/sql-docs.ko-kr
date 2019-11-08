---
title: SQL Server 빅 데이터 클러스터 릴리스 정보
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)](미리 보기)의 최신 업데이트 및 알려진 문제를 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e868d5db99c3f0be141d28a881d8d8bc6f9c241e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531638"
---
# <a name="sql-server-big-data-clusters-release-notes"></a>SQL Server 빅 데이터 클러스터 릴리스 정보

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

기계 학습 및 AI 기능을 포함하여 대규모 데이터 세트를 사용하여 작업하기 위한 완전한 환경을 제공하는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]로 모든 데이터에서 거의 실시간으로 인사이트를 얻을 수 있습니다.

이 문서에는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)](BDC) 최신 릴리스의 업데이트 및 알려진 문제가 나와 있습니다.

## <a id="rtm"></a> SQL Server 2019

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]부터 SQL Server 빅 데이터 클러스터가 도입되었습니다.

SQL Server 빅 데이터 클러스터는 다음과 같은 용도로 사용할 수 있습니다.

- Kubernetes에서 실행되는 SQL Server, Spark 및 HDFS 컨테이너의 [확장성 있는 클러스터 배포](../big-data-cluster/deploy-get-started.md) 
- Transact-SQL 또는 Spark에서 빅 데이터 읽기, 쓰기 및 처리
- 대용량 빅 데이터를 사용하여 가치 높은 관계형 데이터를 쉽게 조합 및 분석
- 외부 데이터 원본 쿼리
- SQL Server에서 관리하는 HDFS에 빅 데이터 저장
- 클러스터를 통해 여러 외부 데이터 원본에서 데이터 쿼리
- AI, 기계 학습 및 기타 분석 작업에 데이터 사용
- [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]에서 [애플리케이션 배포 및 실행](../big-data-cluster/concept-application-deployment.md)
- [PolyBase](../relational-databases/polybase/polybase-guide.md)를 사용하여 데이터 가상화 외부 테이블을 사용하여 외부 SQL Server, Oracle, Teradata, MongoDB 및 ODBC 데이터 원본의 데이터 쿼리
- Always On 가용성 그룹 기술을 사용하여 SQL Server 마스터 인스턴스 및 모든 데이터베이스에 관해 고가용성 제공

## <a name="sql-server-version"></a>SQL Server 버전

SQL Server의 현재 버전은 `15.0.2070.34`입니다.

## <a name="image-tags"></a>이미지 태그

이 릴리스의 이미지 태그는 `2019-GDR1-ubuntu-16.04`입니다.

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="supportability"></a>지원 가능성

이 섹션에서는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)](BDC)에서 지원하는 플랫폼에 관해 설명합니다.

### <a name="kubernetes-platforms"></a>Kubernetes 플랫폼

|플랫폼|지원되는 버전|
|---------|---------|
|Kubernetes|BDC에는 Kubernetes 버전 1.13 이상이 필요합니다. Kubernetes 버전 지원 정책은 [Kubernetes version and version skew support policy](https://kubernetes.io/docs/setup/release/version-skew-policy/)(Kubernetes 버전 및 버전 기울이기 지원 정책)를 참조하세요.|
|AKS(Azure Kubernetes Service)|BDC에는 AKS 버전 1.13 이상이 필요합니다.<br/>버전 지원 정책은 [AKS에서 지원되는 Kubernetes 버전](/azure/aks/supported-kubernetes-versions)을 참조하세요.|

### <a name="host-os-for-kubernetes"></a>Kubernetes용 호스트 OS

|플랫폼|지원되는 버전|
|---------|---------|
|Red Hat Enterprise Linux|7.3, 7.4, 7.5, 7.6|
|Ubuntu|16.04|

### <a name="tools"></a>도구

|플랫폼|지원되는 버전|
|---------|---------|
|`azdata`|서버와 동일한 부 버전이어야 합니다(SQL Server 마스터 인스턴스와 동일).<br/>`azdata –-version`을 실행하여 버전을 확인하세요. 현재 이 버전은 `15.0.2070`입니다.|
|Azure Data Studio|[Azure Data Studio](https://aka.ms/getazuredatastudio)의 최신 빌드를 받으세요.|

### <a name="sql-server-editions"></a>SQL Server 버전

|버전|참고|
|---------|---------|
|Enterprise<br/>Standard<br/>Developer| 빅 데이터 클러스터 버전은 SQL Server 마스터 인스턴스에 의해 결정됩니다. 배포 시점에는 기본적으로 개발자 버전이 배포됩니다. 배포 후에 버전을 변경할 수 있습니다. [SQL Server 마스터 인스턴스 구성](../big-data-cluster/configure-sql-server-master-instance.md)을 참조하세요. |

## <a name="known-issues"></a>알려진 문제

### <a name="livy-job-submission-from-azure-data-studio-ads-or-curl-fail-with-500-error"></a>ADS(Azure Data Studio) 또는 curl에서 Livy 작업 제출 시 500 오류가 발생하고 제출이 실패함

**문제 및 고객에게 미치는 영향**: HA 구성에서는 Spark 공유 리소스(sparkhead)가 여러 복제본으로 구성되어 있습니다. 이 경우 ADS(Azure Data Studio) 또는 `curl`에서 Livy 작업을 제출할 때 제출에 실패할 수 있습니다. 확인하려면 거부된 연결의 sparkjead pod 결과로 `curl`해 보세요. 예를 들어, `curl https://sparkhead-0:8998/`이나 `curl https://sparkhead-1:8998`은 500 오류를 반환합니다.

이 문제는 다음과 같은 경우에 발생합니다.

- Zookeeper po 또는 각 Zookeeper 인스턴스의 프로세스가 몇 차례 다시 시작된 경우
- Sparkhead pod과 Zookeeper pod 사이의 네트워크 연결이 불안정한 경우

**해결 방법**: 두 Livy 서버를 모두 다시 시작합니다.

```bash
kubectl -n <clustername> exec sparkhead-0 -c hadoop-livy-sparkhistory supervisorctl restart livy
```

```bash
kubectl -n <clustername> exec sparkhead-1 -c hadoop-livy-sparkhistory supervisorctl restart livy
```

### <a name="create-memory-optimized-table-when-master-instance-in-an-availability-group"></a>마스터 인스턴스가 가용성 그룹에 있을 때 메모리 최적화된 테이블 만들기

- **문제 및 고객에게 미치는 영향**: 가용성 그룹 데이터베이스(수신기) 연결을 위해 노출된 기본 엔드포인트를 사용하여 메모리 최적화된 테이블을 만들 수 없습니다.

- **해결 방법**: SQL Server 마스터 인스턴스가 가용성 그룹 구성 안에 있을 때 메모리 최적화된 테이블을 만들려면 [SQL Server 인스턴스에 연결](deployment-high-availability.md#instance-connect)하고, 엔드포인트를 노출시키고, SQL Server 데이터베이스에 연결하고, 새 연결로 만든 세션에서 메모리 최적화된 테이블을 만듭니다.

### <a name="insert-to-external-tables-active-directory-authentication-mode"></a>Active Directory 인증 모드에서 외부 테이블에 삽입

- **문제 및 고객에게 미치는 영향**: SQL Server 마스터 인스턴스가 Active Directory 인증 모드에 있을 때, 외부 테이블 중 적어도 하나 이상이 스토리지 풀에 있는 외부 테이블에서만 선택하여 다른 외부 테이블에 삽입하는 쿼리는 다음을 반환합니다.

   ```
   Msg 7320, Level 16, State 102, Line 1
   Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "SQLNCLI11". Only domain logins can be used to query Kerberized storage pool.
   ```

- **해결 방법**: 다음 방법을 사용하여 쿼리를 수정합니다. 스토리지 풀 테이블을 로컬 테이블에 조인하거나 먼저 로컬 테이블에 삽입한 다음 이 로컬 테이블에서 읽어서 데이터 풀에 삽입합니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
