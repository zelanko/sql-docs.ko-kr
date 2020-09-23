---
title: SQL Server 빅 데이터 클러스터 릴리스 정보
titleSuffix: SQL Server big data clusters
description: 이 문서에서는 SQL Server 빅 데이터 클러스터의 최신 업데이트 및 알려진 문제를 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/02/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 32cfd85d1b07a315a196c2728c776297c4d85d9d
ms.sourcegitcommit: c5f0c59150c93575bb2bd6f1715b42716001126b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89392177"
---
# <a name="sql-server-2019-big-data-clusters-release-notes"></a>SQL Server 2019 빅 데이터 클러스터 릴리스 정보

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

다음 릴리스 정보는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]에 적용됩니다. 이 문서는 각 릴리스에 대한 섹션으로 나뉩니다. 각 릴리스에는 CU 변경 내용을 설명하는 지원 문서 링크와 Linux 패키지 다운로드용 링크가 있습니다. 이 문서에는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)](BDC) 최신 릴리스의 [알려진 문제](#known-issues)가 나와 있습니다.

## <a name="supported-platforms"></a>지원 플랫폼

이 섹션에서는 BDC에서 지원되는 플랫폼에 대해 설명합니다.

### <a name="kubernetes-platforms"></a>Kubernetes 플랫폼

|플랫폼|지원되는 버전|
|---------|---------|
|Vanilla(업스트림) Kubernetes|최소 1.13 버전의 Kubernetes 클러스터를 사용하여 온-프레미스에 BDC를 배포합니다. [Kubernetes version and version skew support policy](https://kubernetes.io/docs/setup/release/version-skew-policy/)(Kubernetes 버전 및 버전 기울이기 지원 정책)를 참조하세요.|
|Red Hat OpenShift|최소 4.3 버전의 OpenShift 클러스터를 사용하여 온-프레미스에 BDC를 배포합니다. [Red Hat OpenShift Container Platform Life Cycle Policy](https://access.redhat.com/support/policy/updates/openshift)(Red Hat OpenShift Container Platform 수명 주기 정책)를 참조하세요.<br><br> SQL Server 2019 CU5에서 지원이 도입되었습니다.|
|AKS(Azure Kubernetes Service)|최소 1.13 버전의 AKS 클러스터에 BDC를 배포합니다.<br/>버전 지원 정책은 [AKS에서 지원되는 Kubernetes 버전](/azure/aks/supported-kubernetes-versions)을 참조하세요.|
|ARO(Azure Red Hat OpenShift)|최소 4.3 버전의 ARO에 BDC를 배포합니다. [Azure Red Hat OpenShift](/azure/openshift/)를 참조하세요. <br><br> SQL Server 2019 CU5에서 지원이 도입되었습니다.|

### <a name="host-os-for-kubernetes"></a>Kubernetes용 호스트 OS

|플랫폼|호스트 OS|지원되는 버전|
|---------|---------|
|Kubernetes|Ubuntu|16.04|
|Kubernetes|Red Hat Enterprise Linux|7.3, 7.4, 7.5, 7.6|
|OpenShift|Red Hat Enterprise Linux/CoreOS |[OpenShift 릴리스 정보](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-about-this-release) 참조|

### <a name="sql-server-editions"></a>SQL Server 버전

|버전|메모|
|---------|---------|
|Enterprise<br/>Standard<br/>Developer| 빅 데이터 클러스터 버전은 SQL Server 마스터 인스턴스에 의해 결정됩니다. 배포 시점에는 기본적으로 개발자 버전이 배포됩니다. 배포 후에 버전을 변경할 수 있습니다. [SQL Server 마스터 인스턴스 구성](./configure-sql-server-master-instance.md)을 참조하세요. |

## <a name="tools"></a>도구

|플랫폼|지원되는 버전|
|---------|---------|
|`azdata`|사용 가능한 최신 버전을 사용하는 것이 가장 좋습니다. SQL Server 2019 CU5 릴리스부터 `azdata`에는 서버와 별개의 의미 체계 버전이 있습니다. <br/><br/>`azdata –-version`을 실행하여 버전을 확인하세요.<br/><br/>최신 버전은 [릴리스 기록](#release-history)을 참조하세요.|
|Azure Data Studio|[Azure Data Studio](https://aka.ms/getazuredatastudio)의 최신 빌드를 받으세요.|

전체 목록은 [필수 도구](deploy-big-data-tools.md#which-tools-are-required)를 참조하세요.

## <a name="release-history"></a>릴리스 기록

다음 표에는 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]의 릴리스 기록이 나와 있습니다.

| 해제          | BDC 버전    | `azdata` 버전| 릴리스 날짜 |
|------------------|----------------|-----------------|--------------|
| [CU6](#cu6)      | 15.0.4053.23   | 20.0.1          | 2020-08-04   |
| [CU5](#cu5)      | 15.0.4043.16   | 20.0.0          | 2020-06-22   |
| [CU4](#cu4)      | 15.0.4033.1    | 15.0.4033       | 2020-03-31   |
| [CU3](#cu3)      | 15.0.4023.6    | 15.0.4023       | 2020-03-12   |
| [CU2](#cu2)      | 15.0.4013.40   | 15.0.4013       | 2020-02-13   |
| [CU1](#cu1)      | 15.0.4003.23   | 15.0.4003       | 2020-01-07   |
| [GDR1](#rtm)     | 15.0.2070.34   | 15.0.2070       | 2019-11-04   |

> [!NOTE]
> CU7에는 SQL Server 2019 빅 데이터 클러스터 업데이트가 없습니다.

## <a name="how-to-install-updates"></a>업데이트 설치 방법

업데이트를 설치하려면 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 업그레이드하는 방법](deployment-upgrade.md)을 참조하세요.

## <a name="cu6-july-2020"></a><a id="cu6"></a> CU6(2020년 7월)

SQL Server 2019의 CU6(누적 업데이트 6) 릴리스입니다.

|패키지 버전 | 이미지 태그 |
|-----|-----|
|15.0.4053.23 |[2019-CU6-ubuntu-16.04]

이 릴리스에는 사소한 수정과 향상된 기능이 포함되어 있습니다. 다음 문서에는 이러한 업데이트와 관련된 정보가 포함되어 있습니다.

- [Active Directory 모드에서 빅 데이터 클러스터 액세스 관리](manage-user-access.md)
- [Active Directory 모드에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포](deploy-active-directory.md)
- [고가용성을 사용하여 SQL Server 빅 데이터 클러스터 배포](deployment-high-availability.md)
- [SQL Server 빅 데이터 클러스터 구성](configure-cluster.md)
- [빅 데이터 클러스터에서 Apache Spark 및 Apache Hadoop 구성](configure-spark-hdfs.md)
- [SQL Server 마스터 인스턴스 구성 속성](reference-config-master-instance.md)
- [Apache Spark 및 Apache Hadoop(HDFS) 구성 속성](reference-config-spark-hadoop.md)
- [Kubernetes RBAC 모델과 BDC를 관리하는 사용자 및 서비스 계정에 대한 영향](kubernetes-rbac.md)

## <a name="cu5-june-2020"></a><a id="cu5"></a> CU5(2020년 6월)

SQL Server 2019의 CU5(누적 업데이트 5) 릴리스입니다.

|패키지 버전 | 이미지 태그 |
|-----|-----|
|15.0.4043.16 |[2019-CU5-ubuntu-16.04]

### <a name="added-capabilities"></a>추가된 기능

- Red Hat OpenShift에서 빅 데이터 클러스터 배포를 지원합니다. 지원에는 온-프레미스 버전 4.3 이상 및 Azure Red Hat OpenShift에서 배포된 OpenShift 컨테이너 플랫폼이 포함됩니다. [Deploy SQL Server Big Data Clusters on OpenShift](deploy-openshift.md)(OpenShift에 SQL Server 빅 데이터 클러스터 배포)를 참조하세요.
- BDC의 일부로 배포된 권한 있는 컨테이너가 더 이상 ‘필요’하지 않도록 BDC 배포 보안 모델을 업데이트했습니다. 권한 없는 컨테이너 외에도, 컨테이너는 SQL Server 2019 CU5를 사용하는 모든 신규 배포에 대해 기본적으로 루트가 아닌 사용자로 실행됩니다. 
- Active Directory 도메인에 여러 개의 빅 데이터 클러스터를 배포하도록 지원을 추가했습니다.
- `azdata` CLI에는 서버와 별개인 고유한 의미 체계 버전이 있습니다. 클라이언트 버전과 서버 버전의 azdata 간에 모든 종속성이 제거되었습니다. 최신 향상 기능 및 수정 사항을 활용할 수 있도록 클라이언트와 서버 모두의 최신 버전을 사용하는 것이 좋습니다.
- 특정 외부 데이터 원본의 검사를 지원하기 위해 두 개의 새로운 저장 프로시저 sp_data_source_objects 및 sp_data_source_table_columns를 도입했습니다. 고객이 T-SQL을 통해 직접 이 저장 프로시저를 사용하여 스키마를 검색하고 가상화가 가능한 테이블을 확인할 수 있습니다. SQL Server, Oracle, MongoDB 및 Teradata에서 외부 테이블을 만들 수 있도록 이러한 변경 내용을 Azure Data Studio용 [데이터 가상화 확장](../azure-data-studio/data-virtualization-extension.md)의 외부 테이블 마법사에서 활용합니다.
- Grafana에서 수행되는 사용자 지정을 유지하도록 지원을 추가했습니다. CU5 이전에는 (Grafana 대시보드를 호스트하는) `metricsui` Pod가 다시 시작될 때 Grafana 구성의 편집 내용이 손실되었습니다. 이 문제를 해결하여 이제 모든 구성이 유지됩니다. 
- Telegraf(`metricsdc` Pod에서 호스팅)를 사용하여 Pod 및 노드 메트릭을 수집하는 데 사용되는 API와 관련된 보안 문제를 해결했습니다. 이 변경으로 인해 이제 Telegraf에서는 서비스 계정, 클러스터 역할 및 클러스터 바인딩에서 필수 권한이 있어야 Pod 및 노드 메트릭을 수집할 수 있습니다. 자세한 내용은 [Cluster role required for Pods and nodes metrics collection](kubernetes-rbac.md#cluster-role-required-for-pods-and-nodes-metrics-collection)(Pod 및 노드 메트릭 수집에 필요한 클러스터 역할)을 참조하세요.
- Pod 및 노드 메트릭의 수집을 제어하는 두 가지 기능 스위치를 추가했습니다. Kubernetes 인프라를 모니터링하기 위해 다른 솔루션을 사용하는 경우 control.json 배포 구성 파일에서 *allowNodeMetricsCollection* 및 *allowPodMetricsCollection*을 false로 설정하면 기본 제공되는 Pod 및 호스트 노드 메트릭 수집을 해제할 수 있습니다. OpenShift 환경의 경우 Pod 및 노드 메트릭을 수집하려면 권한 기능이 필요하므로 기본 제공 배포 프로필에서 이 설정은 기본적으로 false로 설정됩니다.

## <a name="cu4-april-2020"></a><a id="cu4"></a> CU4(2020년 4월)

SQL Server 2019의 CU4(누적 업데이트 4) 릴리스입니다. 이 릴리스의 SQL Server 데이터베이스 엔진 버전은 15.0.4033.1입니다.

|패키지 버전 | 이미지 태그 |
|-----|-----|
|15.0.4033.1 |[2019-CU4-ubuntu-16.04]

## <a name="cu3-march-2020"></a><a id="cu3"></a> CU3(2020년 3월)

SQL Server 2019의 CU3(누적 업데이트 3) 릴리스입니다. 이 릴리스의 SQL Server 데이터베이스 엔진 버전은 15.0.4023.6입니다.

|패키지 버전 | 이미지 태그 |
|-----|-----|
|15.0.4023.6 |[2019-CU3-ubuntu-16.04]

### <a name="resolved-issues"></a>해결된 문제

SQL Server 2019 CU3에서는 이전 릴리스의 다음 문제를 해결합니다.

- [프라이빗 리포지토리를 사용하여 배포](#deployment-with-private-repository)
- [시간 초과로 인해 업그레이드에 실패할 수 있음](#upgrade-may-fail-due-to-timeout)

## <a name="cu2-february-2020"></a><a id="cu2"></a> CU2(2020년 2월)

SQL Server 2019의 CU2(누적 업데이트 2) 릴리스입니다. 이 릴리스에 대한 SQL Server 데이터베이스 엔진 버전은 15.0.4013.40입니다.

|패키지 버전 | 이미지 태그 |
|-----|-----|
|15.0.4013.40 |[2019-CU2-ubuntu-16.04]

## <a name="cu1-january-2020"></a><a id="cu1"></a> CU1(2020년 1월)

SQL Server 2019의 CU1(누적 업데이트 1) 릴리스입니다. 이 릴리스에 대한 SQL Server 데이터베이스 엔진 버전은 15.0.4003.23입니다.

|패키지 버전 | 이미지 태그 |
|-----|-----|
|15.0.4003.23|[2019-CU1-ubuntu-16.04]

## <a name="gdr1-november-2019"></a><a id="rtm"></a> GDR1(2019년 11월)

SQL Server 2019 GDR1(일반 배포 릴리스 1) - [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-nover.md)]에 대한 일반 가용성이 도입되었습니다. 이 릴리스에 대한 SQL Server 데이터베이스 엔진 버전은 15.0.2070.34입니다.

|패키지 버전 | 이미지 태그 |
|-----|-----|
|15.0.2070.34|[2019-GDR1-ubuntu-16.04]

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="known-issues"></a>알려진 문제

### <a name="empty-livy-jobs-before-you-apply-cumulative-updates"></a>누적 업데이트를 적용하기 전의 빈 Livy 작업

- **영향을 받는 릴리스**: 현재 누적 업데이트를 통해

- **문제 및 고객에게 미치는 영향**: 업그레이드하는 동안 sparkhead에서 404 오류를 반환합니다.

- **해결 방법**: BDC를 업그레이드하기 전에 활성 Livy 세션 또는 일괄 처리 작업이 없는지 확인합니다. 이 문제를 방지하려면 [지원되는 릴리스에서 업그레이드](deployment-upgrade.md#upgrade-from-supported-release)의 지침을 따르세요. 

   업그레이드 프로세스 중에 Livy에서 404 오류를 반환하는 경우 두 sparkhead 노드 모두에서 Livy 서버를 다시 시작합니다. 예를 들어:

   ```console
   kubectl -n <clustername> exec -it sparkhead-0/sparkhead-1 -c hadoop-livy-sparkhistory -- exec supervisorctl restart livy
   ```

### <a name="big-data-cluster-generated-service-accounts-passwords-expiration"></a>빅 데이터 클러스터 생성 서비스 계정 암호 만료

- **영향을 받는 릴리스**: 릴리스에 관계없이 Active Directory 통합을 사용한 모든 빅 데이터 클러스터 배포

- **문제 및 고객에게 미치는 영향**: 빅 데이터 클러스터를 배포하는 동안 워크플로는 [서비스 계정](active-directory-objects.md) 집합을 생성합니다. 도메인 컨트롤러에 설정된 암호 만료 정책에 따라 이러한 계정의 암호는 만료될 수 있습니다(기본값은 42일). 지금은 BDC의 모든 계정에 대한 자격 증명을 회전하는 메커니즘이 없으므로 만료 기간이 경과하면 클러스터가 작동하지 않게 됩니다.

- **해결 방법**: 도메인 컨트롤러에서 BDC 서비스 계정의 만료 정책을 "암호 사용 기간 제한 없음"으로 업데이트합니다. 이러한 계정의 전체 목록은 [자동 생성 Active Directory 개체](active-directory-objects.md)를 참조하세요. 이 작업은 만료 이전 또는 이후에 수행할 수 있습니다. 후자의 경우 만료된 암호를 Active Directory가 다시 활성화합니다.

### <a name="credentials-for-accessing-services-through-gateway-endpoint"></a>게이트웨이 엔드포인트를 통해 서비스에 액세스하기 위한 자격 증명

- **영향을 받는 릴리스**: CU5부터 새 클러스터가 배포됩니다.

- **문제 및 고객에게 미치는 영향**: SQL Server 2019 CU5를 사용하여 배포된 새로운 빅 데이터 클러스터의 경우 게이트웨이 사용자 이름은 **루트**가 아닙니다. 게이트웨이 엔드포인트에 연결하는 데 사용된 애플리케이션에서 잘못된 자격 증명을 사용하는 경우 인증 오류가 표시됩니다. 이런 변경은 루트가 아닌 사용자로 빅 데이터 클러스터 내에서 애플리케이션을 실행한 결과입니다(SQL Server 2019 CU5 릴리스부터 새로운 기본 동작: CU5를 사용하여 새 빅 데이터 클러스터를 배포할 때 게이트웨이 엔드포인트의 사용자 이름은 **AZDATA_USERNAME** 환경 변수를 통해 전달된 값을 기반으로 함). 이때 사용자 이름은 컨트롤러 및 SQL Server 엔드포인트에 사용되는 것과 동일합니다. 이런 현상은 새 배포에만 영향을 미치며, 이전 릴리스를 사용하여 배포된 기존 빅 데이터 클러스터는 계속 **루트**를 사용합니다. Active Directory 인증을 사용하도록 클러스터를 배포하는 경우 자격 증명에는 영향이 없습니다. 

- **해결 방법**: Azure Data Studio는 게이트웨이 연결에 대해 자격 증명 변경을 투명하게 처리하여 ObjectExplorer에서 HDFS 검색 환경을 사용하도록 설정합니다. 이 사용 사례를 처리하는 데 필요한 변경 내용이 포함된 [최신 Azure Data Studio 릴리스](../azure-data-studio/download-azure-data-studio.md)를 설치해야 합니다.
게이트웨이를 통해 서비스에 액세스하기 위해 자격 증명을 제공해야 하는 다른 시나리오(예: `azdata`를 사용하여 로그인, Spark의 웹 대시보드에 액세스)의 경우 올바른 자격 증명이 사용되는지 확인해야 합니다. CU5 이전에 배포된 기존 클러스터를 대상으로 하는 경우 클러스터를 CU5로 업그레이드한 후에도 계속 **루트** 사용자 이름을 사용하여 게이트웨이에 연결합니다. CU5 빌드를 사용하여 새 클러스터를 배포하는 경우 **AZDATA_USERNAME** 환경 변수에 해당하는 사용자 이름을 제공하여 로그인합니다.

### <a name="pods-and-nodes-metrics-not-being-collected"></a>Pod 및 노드 메트릭이 수집되지 않음

- **영향을 받는 릴리스**: CU5 이미지를 사용하는 새 클러스터 및 기존 클러스터

- **문제 및 고객에게 미치는 영향**: `telegraf`에서 메트릭 Pod 및 호스트 노드 메트릭을 수집하는 데 사용한 API와 관련된 보안 수정의 결과, 고객은 메트릭이 수집되지 않는 것을 경험했을 수도 있습니다. 이런 현상은 (CU5로 업그레이드한 후) BDC의 새 배포와 기존 배포 모두에서 일어날 수 있습니다. 수정한 결과, 이제 Telegraf는 클러스터 전체 역할 권한을 가진 서비스 계정을 요구합니다. 배포에서 필요한 서비스 계정 및 클러스터 역할을 만들려고 시도하지만 클러스터를 배포하거나 업그레이드를 수행하는 사용자에게 충분한 권한이 없는 경우에는 배포/업그레이드가 진행되고 경고가 나타나며 성공하지만 Pod 및 노드 메트릭은 수집되지 않습니다.

- **해결 방법**: 배포/업그레이드 전이나 후에 관리자에게 해당 역할 및 서비스 계정을 만들도록 요청하면 됩니다. 그러면 BDC가 이 역할 및 서비스 계정을 사용합니다. [이 문서](kubernetes-rbac.md#cluster-role-required-for-pods-and-nodes-metrics-collection)에서는 필요한 아티팩트를 만드는 방법을 설명합니다.

### <a name="azdata-bdc-copy-logs-command-failure"></a>`azdata bdc copy-logs` 명령 실패

- **영향을 받는 릴리스**: `azdata` 버전 *20.0.0*

- **문제 및 고객에게 미치는 영향**: *copy-logs* 명령의 구현은 명령이 실행되는 클라이언트 머신에 `kubectl` 클라이언트 도구가 설치되어 있다고 가정합니다. `oc` 도구만 설치된 클라이언트에서 OpenShift에 설치된 BDC 클러스터에 대해 명령을 실행하는 경우 ‘로그를 수집하는 동안 오류가 발생했습니다. [WinError 2] 시스템에서 지정한 파일을 찾을 수 없습니다.’라는 오류가 발생합니다.

- **해결 방법**: 동일한 클라이언트 머신에 `kubectl` 도구를 설치하고 `azdata bdc copy-logs` 명령을 다시 실행합니다. `kubectl`을 설치하는 방법에 대한 지침은 [여기](deploy-big-data-tools.md)를 참조하세요.

### <a name="deployment-with-private-repository"></a>프라이빗 리포지토리를 사용하여 배포

- **영향을 받는 릴리스**: GDR1, CU1, CU2. CU3에서 문제가 해결되었습니다.

- **문제 및 고객에게 미치는 영향**: 프라이빗 리포지토리에서 업그레이드하는 경우 특정 요구 사항이 있습니다.

- **해결 방법**: 프라이빗 리포지토리를 사용하여 BDC를 배포하거나 업그레이드하기 위해 이미지를 미리 가져오는 경우 현재 빌드 이미지와 대상 빌드 이미지가 프라이빗 리포지토리에 있는지 확인합니다. 이렇게 하면 필요한 경우 성공적으로 롤백할 수 있습니다. 또한 원래 배포 이후 프라이빗 리포지토리의 자격 증명을 변경한 경우 업그레이드하기 전에 Kubernetes에서 해당 암호를 업데이트합니다. `azdata`는 `AZDATA_PASSWORD` 및 `AZDATA_USERNAME` 환경 변수를 통한 자격 증명 업데이트를 지원하지 않습니다. [`kubectl edit secrets`](https://kubernetes.io/docs/concepts/configuration/secret/#editing-a-secret)를 사용하여 암호를 업데이트합니다. 

현재 및 대상 빌드에 다른 리포지토리를 사용하여 업그레이드할 수 없습니다.

### <a name="upgrade-may-fail-due-to-timeout"></a>시간 초과로 인해 업그레이드가 실패할 수 있음

- **영향을 받는 릴리스**: GDR1, CU1, CU2. CU3에서 문제가 해결되었습니다.

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

   2. 다음 필드를 편집합니다.

       **`controllerUpgradeTimeoutInMinutes`** 컨트롤러 또는 컨트롤러 db의 업그레이드가 완료될 때까지 대기할 시간(분)을 지정합니다. 기본값은 5입니다. 20 이상으로 업데이트합니다.

       **`totalUpgradeTimeoutInMinutes`** : 컨트롤러와 컨트롤러 db 모두가 업그레이드(`controller` + `controllerdb` 업그레이드)를 완료하는 데 걸리는 시간을 합한 값을 지정합니다. 기본값은 10입니다. 40 이상으로 업데이트합니다.

       **`componentUpgradeTimeoutInMinutes`** : 업그레이드의 각 후속 단계를 완료해야 하는 기간을 지정합니다. 기본값은 30입니다. 45로 업데이트합니다.

   3. 저장한 후 종료합니다.

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