---
title: SQL Server 빅 데이터 클러스터 릴리스 정보
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 빅 데이터 클러스터의 최신 업데이트 및 알려진 문제를 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 38a1e2381bb3b7730a06af09b807886e18a50d13
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78925860"
---
# <a name="sql-server-2019-big-data-clusters-release-notes"></a>SQL Server 2019 빅 데이터 클러스터 릴리스 정보

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 릴리스 정보는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]에 적용됩니다. 이 문서는 각 릴리스에 대한 섹션으로 나뉩니다. 각 릴리스에는 CU 변경 내용을 설명하는 지원 문서 링크와 Linux 패키지 다운로드용 링크가 있습니다. 이 문서에는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)](BDC) 최신 릴리스의 [알려진 문제](#known-issues)가 나와 있습니다.

## <a name="supported-platforms"></a>지원 플랫폼

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

### <a name="sql-server-editions"></a>SQL Server 버전

|버전|메모|
|---------|---------|
|Enterprise<br/>Standard<br/>Developer| 빅 데이터 클러스터 버전은 SQL Server 마스터 인스턴스에 의해 결정됩니다. 배포 시점에는 기본적으로 개발자 버전이 배포됩니다. 배포 후에 버전을 변경할 수 있습니다. [SQL Server 마스터 인스턴스 구성](../big-data-cluster/configure-sql-server-master-instance.md)을 참조하세요. |

## <a name="tools"></a>도구

|플랫폼|지원되는 버전|
|---------|---------|
|`azdata`|서버와 동일한 부 버전이어야 합니다(SQL Server 마스터 인스턴스와 동일).<br/><br/>`azdata –-version`을 실행하여 버전을 확인하세요.<br/><br/>SQL Server 2019 CU2 기준으로 이 버전은 `15.0.4013`입니다.|
|Azure Data Studio|[Azure Data Studio](https://aka.ms/getazuredatastudio)의 최신 빌드를 받으세요.|

## <a name="release-history"></a>릴리스 기록

다음 표에는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 릴리스 기록이 나와 있습니다.

| 해제               | 버전       | 릴리스 날짜 |
|-----------------------|---------------|--------------|
| [CU2](#cu2)           | 15.0.4013.40    | 2020-02-13   |
| [CU1](#cu1)           | 15.0.4003.23   | 2020-01-07   |
| [GDR1](#rtm)            | 15.0.2070.34  | 2019-11-04   |

## <a name="how-to-install-updates"></a>업데이트 설치 방법

업데이트를 설치하려면 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 업그레이드하는 방법](deployment-upgrade.md)을 참조하세요.

## <a id="cu2"></a> CU2(2020년 2월)

SQL Server 2019의 CU2(누적 업데이트 2) 릴리스입니다. 이 릴리스에 대한 SQL Server 데이터베이스 엔진 버전은 15.0.4013.40입니다.

|패키지 버전 | 이미지 태그 |
|-----|-----|
|15.0.4013.40 |[2019-CU2-ubuntu-16.04]

## <a id="cu1"></a> CU1(2020년 1월)

SQL Server 2019의 CU1(누적 업데이트 1) 릴리스입니다. 이 릴리스에 대한 SQL Server 데이터베이스 엔진 버전은 15.0.4003.23입니다.

|패키지 버전 | 이미지 태그 |
|-----|-----|
|15.0.4003.23|[2019-CU1-ubuntu-16.04]

## <a id="rtm"></a> GDR1(2019년 11월)

SQL Server 2019 GDR1(일반 배포 릴리스 1) - [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-nover.md)]에 대한 일반 가용성이 도입되었습니다. 이 릴리스에 대한 SQL Server 데이터베이스 엔진 버전은 15.0.2070.34입니다.

|패키지 버전 | 이미지 태그 |
|-----|-----|
|15.0.2070.34|[2019-GDR1-ubuntu-16.04]

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="known-issues"></a>알려진 문제

### <a name="deployment-with-private-repository"></a>프라이빗 리포지토리를 사용하여 배포

- **문제 및 고객에게 미치는 영향**: 프라이빗 리포지토리에서 업그레이드하는 경우 특정 요구 사항이 있습니다.

- **해결 방법**: 프라이빗 리포지토리를 사용하여 BDC를 배포하거나 업그레이드하기 위해 이미지를 미리 가져오는 경우 현재 빌드 이미지와 대상 빌드 이미지가 프라이빗 리포지토리에 있는지 확인합니다. 이렇게 하면 필요한 경우 성공적으로 롤백할 수 있습니다. 또한 원래 배포 이후 프라이빗 리포지토리의 자격 증명을 변경한 경우 업그레이드하기 전에 Kubernetes에서 해당 암호를 업데이트합니다. `azdata`는 `AZDATA_PASSWORD` 및 `AZDATA_USERNAME` 환경 변수를 통한 자격 증명 업데이트를 지원하지 않습니다. [`kubectl edit secrets`](https://kubernetes.io/docs/concepts/configuration/secret/#editing-a-secret)를 사용하여 암호를 업데이트합니다. 

현재 및 대상 빌드에 다른 리포지토리를 사용하여 업그레이드할 수 없습니다.

### <a name="upgrade-may-fail-due-to-timeout"></a>시간 초과로 인해 업그레이드가 실패할 수 있음

- **문제 및 고객에게 미치는 영향**: 시간 초과로 인해 업그레이드가 실패할 수 있습니다.

   다음 코드는 오류가 어떻게 표시되는지 보여 줍니다.

   ```
   >azdata.EXE bdc upgrade --name <mssql-cluster>
   Upgrading cluster to version 15.0.4003

   NOTE: Cluster upgrade can take a significant amount of time depending on
   configuration, network speed, and the number of nodes in the cluster.

   Upgrading Control Plane.
   Control plane upgrade failed. Failed to upgrade controller.
   ```

   이 오류는 Azure Kubernetes Service(AKS)에서 BDC를 업그레이드할 때 발생할 가능성이 높습니다.

- **해결 방법**: 업그레이드 시간 제한을 늘립니다. 

   업그레이드에 대한 시간 제한을 늘리려면 업그레이드 구성 맵을 편집합니다. 업그레이드 구성 맵을 편집하려면 다음을 수행합니다.

   1. 다음 명령 실행:

      ```bash
      kubectl edit configmap controller-upgrade-configmap
      ```

   2.   다음 필드를 편집합니다.

       **`controllerUpgradeTimeoutInMinutes`** 컨트롤러 또는 컨트롤러 db의 업그레이드가 완료될 때까지 대기할 시간(분)을 지정합니다. 기본값은 5입니다. 20 이상으로 업데이트합니다.

       **`totalUpgradeTimeoutInMinutes`** : 컨트롤러와 컨트롤러 db 모두가 업그레이드를 완료하는 데 걸리는 시간을 합한 값을 지정합니다(컨트롤러 + 컨트롤러 db 업그레이드). 기본값은 10입니다. 40 이상으로 업데이트합니다.

       **`componentUpgradeTimeoutInMinutes`** : 업그레이드의 각 후속 단계를 완료해야 하는 기간을 지정합니다.  기본값은 30입니다. 45로 업데이트합니다.

   3.   저장한 후 종료합니다.

   아래의 python 스크립트는 시간 제한을 설정하는 또 다른 방법입니다.

   ```python
   from kubernetes import client, config
   import json

   def set_upgrade_timeouts(namespace, controller_timeout=20, controller_total_timeout=40, component_timeout=45):
       """ Set the timeouts for upgrades

       The timeout settings are as follows

       controllerUpgradeTimeoutInMinutes: sets the max amount of time for the controller
           or controllerdb to finish upgrading

       totalUpgradeTimeoutInMinutes: sets the max amount of time to wait for both the
           controller and controllerdb to complete their upgrade

       componentUpgradeTimeoutInMinutes: sets the max amount of time allowed for
           subsequent phases of the upgrade to complete
       """
       config.load_kube_config()

       upgrade_config_map = client.CoreV1Api().read_namespaced_config_map("controller-upgrade-configmap", namespace)

       upgrade_config = json.loads(upgrade_config_map.data["controller-upgrade"])

       upgrade_config["controllerUpgradeTimeoutInMinutes"] = controller_timeout

       upgrade_config["totalUpgradeTimeoutInMinutes"] = controller_total_timeout

       upgrade_config["componentUpgradeTimeoutInMinutes"] = component_timeout

       upgrade_config_map.data["controller-upgrade"] = json.dumps(upgrade_config)

       client.CoreV1Api().patch_namespaced_config_map("controller-upgrade-configmap", namespace, upgrade_config_map)
   ```

### <a name="livy-job-submission-from-azure-data-studio-ads-or-curl-fail-with-500-error"></a>ADS(Azure Data Studio) 또는 curl에서 Livy 작업 제출 시 500 오류가 발생하고 제출이 실패함

- **문제 및 고객에게 미치는 영향**: HA 구성에서는 Spark 공유 리소스 `sparkhead`가 여러 복제본으로 구성되어 있습니다. 이 경우 ADS(Azure Data Studio) 또는 `curl`에서 Livy 작업을 제출할 때 제출에 실패할 수 있습니다. 확인하려면 거부된 연결의 `sparkhead` pod 결과로 `curl`해 보세요. 예를 들어, `curl https://sparkhead-0:8998/`이나 `curl https://sparkhead-1:8998`은 500 오류를 반환합니다.

   이 문제는 다음과 같은 경우에 발생합니다.

   - Zookeeper pod 또는 각 Zookeeper 인스턴스의 프로세스가 몇 차례 다시 시작된 경우
   - `sparkhead` pod과 Zookeeper pod 사이의 네트워크 연결이 불안정한 경우

- **해결 방법**: 두 Livy 서버를 모두 다시 시작합니다.

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

### <a name="transparent-data-encryption-capabilities-can-not-be-used-with-databases-that-are-part-of-the-availability-group-in-the-sql-server-master-instance"></a>SQL Server 마스터 인스턴스에서 가용성 그룹의 일부인 데이터베이스에는 투명한 데이터 암호화 기능을 사용할 수 없음

- **문제 및 고객에게 미치는 영향**: HA 구성에서는 암호화에 사용되는 마스터 키가 각 복제본마다 다르기 때문에 암호화가 사용된 데이터베이스는 장애 조치(failover) 후에 사용할 수 없습니다. 

- **해결 방법**: 이 문제에 대한 해결 방법이 없습니다. 수정될 때까지 이 구성에서 암호화를 사용하지 않는 것이 좋습니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.
