---
title: Active Directory 모드에서 배포
titleSuffix: SQL Server Big Data Cluster
description: Active Directory 도메인에서 SQL Server 빅 데이터 클러스터를 업그레이드하는 방법을 알아봅니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 48dde8000274ea74df1c6095714b54669c5becdd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257293"
---
# <a name="deploy-sql-server-big-data-cluster-in-active-directory-mode"></a>Active Directory 모드에서 SQL Server 빅 데이터 클러스터 배포

이 문서에서는 Active Directory 모드로 SQL Server 빅 데이터 클러스터를 배포하는 방법을 설명합니다. 이 문서의 단계를 수행하려면 Active Directory 도메인에 대한 액세스 권한이 있어야 합니다. 계속 진행하기 전에 [Active Directory 모드로 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포](active-directory-prerequisites.md)에 설명된 요구 사항을 완료해야 합니다.

## <a name="prepare-deployment"></a>배포 준비

AD 통합을 사용하여 BDC를 배포하는 경우 AD에서 BDC 관련 개체를 만들기 위해 제공해야 하는 몇 가지 추가 정보가 있습니다.

`kubeadm-prod` 프로필을 사용하면(또는 CU5 릴리스부터는 `openshift-prod`를 사용하면) AD 통합에 필요한 보안 관련 정보 및 엔드포인트 관련 정보에 대한 자리 표시자를 자동으로 갖게 됩니다.

또한 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]가 AD에서 필요한 개체를 만드는 데 사용할 자격 증명을 제공해야 합니다. 이러한 자격 증명은 환경 변수로 제공됩니다.

## <a name="set-security-environment-variables"></a>보안 환경 변수 설정

다음 환경 변수는 AD 통합을 설정하는 데 사용되는 BDC 도메인 서비스 계정의 자격 증명을 제공합니다. 이 계정은 BDC에서 BDC 관련 AD 개체를 유지하는 데도 사용합니다.

```bash
export DOMAIN_SERVICE_ACCOUNT_USERNAME=<AD principal account name>
export DOMAIN_SERVICE_ACCOUNT_PASSWORD=<AD principal password>
```

## <a name="provide-security-and-endpoint-parameters"></a>보안 및 엔드포인트 매개 변수 제공

자격 증명에 대한 환경 변수 외에도 AD 통합이 작동하기 위한 보안 및 엔드포인트 정보를 제공해야 합니다. 필요한 매개 변수는 `kubeadm-prod`/`openshift-prod` [배포 프로필](deployment-guidance.md#configfile)에 자동으로 포함됩니다.

AD 통합에 필요한 매개 변수는 다음과 같습니다. 이 문서의 아래 부분에 나오는 `config replace` 명령을 사용하여 이러한 매개 변수를 `control.json` 및 `bdc.json` 파일에 추가합니다. 아래의 모든 예제에서는 `contoso.local` 도메인 예제를 사용합니다.

- `security.activeDirectory.ouDistinguishedName`: 클러스터 배포에서 만든 모든 AD 계정이 추가될 OU(조직 구성 단위)의 고유 이름입니다. 도메인을 `contoso.local`이라고 하는 경우 OU의 고유 이름은 `OU=BDC,DC=contoso,DC=local`입니다.

- `security.activeDirectory.dnsIpAddresses`: 도메인의 DNS 서버 IP 주소 목록을 포함합니다. 

- `security.activeDirectory.domainControllerFullyQualifiedDns`: 도메인 컨트롤러의 FQDN 목록입니다. FQDN에는 도메인 컨트롤러의 머신/호스트 이름이 포함됩니다. 여러 도메인 컨트롤러가 있는 경우 여기에 목록을 제공할 수 있습니다. 예: `HOSTNAME.CONTOSO.LOCAL`.

  > [!IMPORTANT]
  > 여러 도메인 컨트롤러가 하나의 도메인에 서비스를 제공하는 경우, 보안 구성의 `domainControllerFullyQualifiedDns` 목록에 있는 첫 번째 항목을 PDC(주 도메인 컨트롤러)로 사용합니다. PDC 이름을 가져오려면 명령 프롬프트에서 `netdom query fsmo`를 입력하고 **Enter** 키를 누릅니다.

- `security.activeDirectory.realm` **선택적 매개 변수** : 대부분의 경우 영역은 도메인 이름과 동일합니다. 동일하지 않은 경우 이 매개 변수를 사용하여 영역 이름(예: `CONTOSO.LOCAL`)을 정의합니다. 이 매개 변수에 제공된 값은 정규화된 값이어야 합니다.

  > [!IMPORTANT]
  > 지금은 BDC가 Active Directory 도메인 이름이 Active Directory 도메인의 **NETBIOS** 이름과 다른 구성을 지원하지 않습니다.

- `security.activeDirectory.domainDnsName`: 클러스터에 사용될 DNS 도메인의 이름입니다(예: `contoso.local`).

- `security.activeDirectory.clusterAdmins`: 이 매개 변수는 하나의 AD 그룹을 사용합니다. AD 그룹 범위는 유니버설 또는 글로벌이어야 합니다. 이 그룹의 멤버는 클러스터에서 관리자 권한을 부여하는 `bdcAdmin` 클러스터 역할을 갖습니다. 즉, 컨트롤러 엔드포인트에 연결된 경우 [SQL Server의 `sysadmin` 권한](../relational-databases/security/authentication-access/server-level-roles.md#fixed-server-level-roles), [HDFS의 `superuser` 권한](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#The_Super-User) 및 관리자 권한을 얻습니다.

  >[!IMPORTANT]
  >배포를 시작하기 전에 AD에서 이 그룹을 만듭니다. 이 AD 그룹의 범위가 도메인이면 로컬 배포에 실패합니다.

- `security.activeDirectory.clusterUsers`: 빅 데이터 클러스터에서 일반 사용자(관리자 권한 없음)인 AD 그룹의 목록입니다. 이 목록에는 유니버설 또는 글로벌 그룹으로 범위가 지정된 AD 그룹이 포함될 수 있습니다. 도메인 로컬 그룹이 될 수는 없습니다.

이 목록에 있는 AD 그룹은 `bdcUser` 빅 데이터 클러스터 역할에 매핑되며, SQL Server([SQL Server 사용 권한](../relational-databases/security/permissions-hierarchy-database-engine.md) 참조) 또는 HDFS([HDFS 사용 권한 가이드](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#:~:text=Permission%20Checks%20%20%20%20Operation%20%20,%20%20N%2FA%20%2029%20more%20rows%20) 참조)에 대한 액세스 권한이 부여되어야 합니다. 컨트롤러 엔드포인트에 연결된 경우 이러한 사용자는 `azdata bdc endpoint list` 명령을 사용하여 클러스터에서 사용할 수 있는 엔드포인트만 나열할 수 있습니다.

이 설정에 대해 AD 그룹을 업데이트하는 방법에 대한 자세한 내용은 [Active Directory 모드에서 빅 데이터 클러스터 액세스 관리](manage-user-access.md)를 참조하세요.

  >[!TIP]
  >Azure Data Studio에서 SQL Server 마스터에 연결된 HDFS 검색 환경을 사용하도록 설정하려면 bdcUser 역할을 가진 사용자에게 VIEW SERVER STATE 권한을 부여해야 합니다. Azure Data Studio에서는 `sys.dm_cluster_endpoints` DMV를 사용하여 HDFS에 연결하는 데 필요한 Knox 게이트웨이 엔드포인트를 가져오기 때문입니다.

  >[!IMPORTANT]
  >배포를 시작하기 전에 AD에서 이 그룹을 만듭니다. 이 AD 그룹의 범위가 도메인이면 로컬 배포에 실패합니다.

  >[!IMPORTANT]
  >도메인 사용자에게 많은 수의 그룹 멤버 자격이 있는 경우, 사용자 지정 *bdc.json* 배포 구성 파일을 사용하여 게이트웨이 설정 `httpserver.requestHeaderBuffer`(기본값: `8192`) 및 HDFS 설정 `hadoop.security.group.mapping.ldap.search.group.hierarchy.levels`(기본값: `10`)의 값을 조정해야 합니다. 이는 431(‘요청 헤더 필드가 너무 큼’) 상태 코드와 함께 게이트웨이 및/또는 HTTP 응답에 대한 연결 시간 초과를 방지하기 위한 모범 사례입니다. 다음은 해당 설정 값을 정의하는 방법과 다수의 그룹 멤버 자격에 권장되는 값을 보여 주는 구성 파일의 한 섹션입니다.

```json
{
    ...
    "spec": {
        "resources": {
            ...
            "gateway": {
                "spec": {
                    "replicas": 1,
                    "endpoints": [{...}],
                    "settings": {
                        "gateway-site.gateway.httpserver.requestHeaderBuffer": "65536"
                    }
                }
            },
            ...
        },
        "services": {
            ...
            "hdfs": {
                "resources": [...],
                "settings": {
                  "core-site.hadoop.security.group.mapping.ldap.search.group.hierarchy.levels": "4"
                }
            },
            ...
        }
    }
}
```

  >[!IMPORTANT]
  >배포가 시작되기 전에, AD에서 아래의 설정에 대해 제공된 그룹을 만듭니다. 이 AD 그룹의 범위가 도메인이면 로컬 배포에 실패합니다.

- `security.activeDirectory.appOwners` **선택적 매개 변수** : 애플리케이션을 만들고, 삭제하고, 실행할 수 있는 권한이 있는 AD 그룹의 목록입니다. 이 목록에는 유니버설 또는 글로벌 그룹으로 범위가 지정된 AD 그룹이 포함될 수 있습니다. 도메인 로컬 그룹이 될 수는 없습니다.

- `security.activeDirectory.appReaders` **선택적 매개 변수** : 애플리케이션을 실행할 수 있는 권한이 있는 AD 그룹의 목록입니다. 이 목록에는 유니버설 또는 글로벌 그룹으로 범위가 지정된 AD 그룹이 포함될 수 있습니다. 도메인 로컬 그룹이 될 수는 없습니다.

아래 표에서는 애플리케이션 관리를 위한 권한 부여 모델을 보여 줍니다.

|   권한 있는 역할   |   [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 명령   |
|----------------------|--------------------|
|   appOwner           | azdata app create  |
|   appOwner           | azdata app update  |
|   appOwner, appReader| azdata app list    |
|   appOwner, appReader| azdata app describe|
|   appOwner           | azdata app delete  |
|   appOwner, appReader| azdata app run     |

- `security.activeDirectory.subdomain`: **선택적 매개 변수** 이 매개 변수는 동일한 도메인에 대해 여러 개의 빅 데이터 클러스터를 배포하는 것을 지원하기 위해 SQL Server 2019 CU5 릴리스에서 도입되었습니다. 이 설정을 사용하여, 배포된 각 빅 데이터 클러스터에 대해 여러 DNS 이름을 지정할 수 있습니다. 이 매개 변수의 값이 `control.json` 파일의 Active Directory 섹션에 지정되지 않은 경우, 기본적으로 하위 도메인 설정 값을 계산하는 데 빅 데이터 클러스터 이름(Kubernetes 네임스페이스 이름과 동일)이 사용됩니다. 

  >[!NOTE]
  >하위 도메인 설정을 통해 전달된 값은 새 AD 도메인이 아니라 BDC 클러스터에서 내부적으로 사용하는 DNS 도메인입니다.

  >[!IMPORTANT]
  >이러한 새로운 기능을 활용하고 동일한 도메인에 여러 개의 빅 데이터 클러스터를 배포하려면 SQL Server 2019 CU5 릴리스부터 최신 버전의 **[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]** 를 설치하거나 업그레이드해야 합니다.

  동일한 Active Directory 도메인에 여러 개의 빅 데이터 클러스터를 배포하는 방법에 대한 자세한 내용은 [개념: Active Directory 모드에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포](active-directory-deployment-background.md)를 참조하세요.

- `security.activeDirectory.accountPrefix`: **선택적 매개 변수** 이 매개 변수는 동일한 도메인에 대해 여러 개의 빅 데이터 클러스터를 배포하는 것을 지원하기 위해 SQL Server 2019 CU5 릴리스에서 도입되었습니다. 이 설정은 여러 빅 데이터 클러스터 서비스에 대한 계정 이름의 고유성을 보장합니다. 계정 이름은 두 클러스터 간에 서로 달라야 합니다. 계정 접두사 이름을 사용자 지정하는 것은 선택 사항이며, 기본적으로 하위 도메인 이름이 계정 접두사로 사용됩니다. 하위 도메인 이름이 12자보다 길면 하위 도메인 이름의 처음 12자가 계정 접두사로 사용됩니다.  

  >[!NOTE]
  >Active Directory에서는 계정 이름을 20자로 제한합니다. BDC 클러스터는 Pod 및 StatefulSets를 구별하기 위해 8자를 사용해야 합니다. 따라서 계정 접두사로 사용할 12자가 남습니다.

[AD 그룹 범위를 확인](/powershell/module/addsadministration/get-adgroup)하여 DomainLocal인지 확인합니다.

배포 구성 파일을 아직 초기화하지 않은 경우 다음 명령을 실행하여 구성의 복사본을 가져올 수 있습니다. 아래 예에서는 `kubeadm-prod` 프로필을 사용하며 `openshift-prod`에도 동일하게 적용됩니다.

```bash
azdata bdc config init --source kubeadm-prod  --target custom-prod-kubeadm
```

`control.json` 파일에서 위의 매개 변수를 설정하려면 다음 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 명령을 사용합니다. 이러한 명령은 구성을 바꾸고, 배포하기 전에 사용자 고유의 값을 제공합니다.

> [!IMPORTANT]
> SQL Server 2019 CU2 릴리스에서는 배포 프로필의 보안 구성 섹션 구조가 약간 변경되었고 Active Directory와 관련된 모든 설정이 `control.json` 파일의 `security` 아래에 있는 json 트리의 새로운 `activeDirectory`에 있습니다.

>[!NOTE]
> 이 섹션에 설명된 대로 하위 도메인에 대해 다른 값을 제공하는 것 외에도, 동일한 Kubernetes 클러스터에서 여러 BDC를 배포할 때 BDC 엔드포인트에 대해 서로 다른 포트 번호를 사용해야 합니다. 이러한 포트 번호는 배포 시점에 [배포 구성](deployment-custom-configuration.md) 프로필을 통해 구성할 수 있습니다.

아래 예제는 SQL Server 2019 CU2 사용을 기반으로 합니다. 배포 구성에서 AD 관련 매개 변수 값을 대체하는 방법을 보여 줍니다. 아래의 도메인 세부 정보는 예제 값입니다.

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

필요에 따라 SQL Server 2019 CU5 릴리스부터 `subdomain` 및 `accountPrefix` 설정의 기본값을 재정의할 수 있습니다.

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.subdomain=[\"bdctest\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.accountPrefix=[\"bdctest\"]"
```

마찬가지로 SQL Server 2019 CU2 이전 릴리스에서는 다음을 실행할 수 있습니다.

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

위의 정보 외에도 다른 클러스터 엔드포인트에 대한 DNS 이름을 제공해야 합니다. 제공된 DNS 이름을 사용하는 DNS 항목은 배포 시 DNS 서버에 자동으로 만들어집니다. 이러한 이름은 다른 클러스터 엔드포인트에 연결할 때 사용됩니다. 예를 들어 SQL 마스터 인스턴스의 DNS 이름이 `mastersql`이고 하위 도메인이 `control.json`에서 클러스터 이름의 기본값을 사용한다는 사실을 고려하면 `mastersql.contoso.local,31433` 또는 `mastersql.mssql-cluster.contoso.local,31433`(엔드포인트 DNS 이름에 대한 배포 구성 파일에 제공한 값에 따라)을 사용하여 도구에서 마스터 인스턴스에 연결합니다. 

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[1].dnsName=<monitoring services DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=<SQL Master Primary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=<SQL Master Secondary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=<Gateway (Knox) DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=<app proxy DNS name>.<Domain name. e.g. contoso.local>"
```

> [!IMPORTANT]
> 원하는 엔드포인트 DNS 이름(정규화된 이름인 경우)을 사용할 수 있으며, 동일한 도메인에 배포된 두 개의 빅 데이터 클러스터 간에 이름이 충돌하지 않습니다. 필요에 따라 `subdomain` 매개 변수 값을 사용하여 여러 클러스터에서 DNS 이름이 서로 다른지 확인할 수 있습니다. 예를 들면 다음과 같습니다.

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.<subdomain e.g. mssql-cluster>.contoso.local"
```

여기서 [AD 통합을 사용하여 SQL Server 빅 데이터 클러스터를 단일 노드 Kubernetes 클러스터(kubeadm)에 배포](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm-ad)하는 스크립트 예제를 찾을 수 있습니다.

> [!Note]
> 새로 도입된 `subdomain` 매개 변수를 수용할 수 없는 시나리오가 있을 수도 있습니다. 이미 **[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]** 로 업그레이드했으며 CU5 이전 릴리스를 배포해야 하는 경우를 예로 들어 보겠습니다. 이런 경우는 매우 드물지만, CU5 이전 동작으로 되돌려야 하는 경우 `control.json`의 Active Directory 섹션에서 `false` 매개 변수를 `useSubdomain`로 설정하면 됩니다.  이 작업을 수행하는 명령은 다음과 같습니다.

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.useSubdomain=false"
```

이제 Active Directory 통합을 사용하여 BDC를 배포하는 데 필요한 모든 매개 변수를 설정해야 합니다.

이제 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 명령과 kubeadm-prod 배포 프로필을 사용하여 Active Directory와 통합된 BDC 클러스터를 배포할 수 있습니다. [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]를 배포하는 방법에 대한 전체 설명서는 [Kubernetes에 SQL Server 빅 데이터 클러스터를 배포하는 방법](deployment-guidance.md)을 참조하세요.

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>도메인 컨트롤러에 대한 역방향 DNS 항목 확인

DNS 서버에 등록된 도메인 컨트롤러 자체에 대한 역방향 DNS 항목(PTR 레코드)이 있는지 확인합니다. 도메인 컨트롤러에서 도메인 이름의 `nslookup`을 실행하여 도메인 컨트롤러 IP 주소로 확인할 수 있는지 알아볼 수 있습니다.

## <a name="known-issues-and-limitations"></a>알려진 문제 및 제한 사항

**SQL Server 2019 CU5에서 알아야 할 제한 사항**

- 현재 로그 검색 대시보드 및 메트릭 대시보드는 AD 인증을 지원하지 않습니다. 배포 시 설정된 기본 사용자 이름과 암호를 사용하여 이러한 대시보드를 인증할 수 있습니다. 다른 모든 클러스터 엔드포인트는 AD 인증을 지원합니다.

- 보안 AD 모드는 현재 `kubeadm` 및 `openshift` 배포 환경에서만 작동하며, AKS 또는 ARO에서는 작동하지 않습니다. `kubeadm-prod` 및 `openshift-prod` 배포 프로필에는 기본적으로 보안 섹션이 포함됩니다.

- SQL Server 2019 CU5 릴리스 전까지는 도메인(Active Directory)당 하나의 BDC만 허용됩니다. 도메인당 여러 BDC를 사용하도록 설정하는 것은 CU5 릴리스부터 지원됩니다.

- 보안 구성에 지정된 AD 그룹은 DomainLocal 범위를 지정할 수 없습니다. [이러한 지침](/powershell/module/addsadministration/get-adgroup)에 따라 AD 그룹의 범위를 확인할 수 있습니다.

- BDC에 대해 구성된 도메인의 AD 계정을 사용하여 BDC에 로그인할 수 있습니다. 다른 트러스트된 도메인의 로그인을 사용하는 것은 지원되지 않습니다.

## <a name="next-steps"></a>다음 단계

[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 연결: Active Directory 모드](active-directory-connect.md)

[SQL Server 빅 데이터 클러스터 Active Directory 통합 문제 해결](troubleshoot-active-directory.md)

[개념: Active Directory 모드에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포](active-directory-deployment-background.md)
