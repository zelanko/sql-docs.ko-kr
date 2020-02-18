---
title: Active Directory 모드에서 SQL Server 빅 데이터 클러스터 배포
titleSuffix: Deploy SQL Server Big Data Cluster in Active Directory mode
description: Active Directory 도메인에서 SQL Server 빅 데이터 클러스터를 업그레이드하는 방법을 알아봅니다.
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 12/02/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e47af4ef20bc3dac6c61b9c5f851822348d36650
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253114"
---
# <a name="deploy-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-in-active-directory-mode"></a>Active Directory 모드에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 배포

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

이 문서에서는 기존 AD 도메인을 인증에 사용하는 Active Directory 인증 모드에서 SQL Server 2019 BDC(빅 데이터 클러스터)를 배포하는 방법에 대해 설명합니다.

## <a name="background"></a>배경

AD(Active Directory) 인증을 사용하도록 설정하려면 BDC에서 클러스터의 다양한 서비스에 필요한 사용자, 그룹, 머신 계정 및 SPN(서비스 사용자 이름)을 자동으로 만듭니다. 이러한 계정을 일부 포함하고 범위 지정 권한을 허용하려면 배포하는 동안 모든 BDC 관련 AD 개체가 만들어지는 OU(조직 구성 단위)를 지정합니다. 이 OU는 클러스터를 배포하기 전에 만듭니다.

Active Directory에 필요한 모든 개체를 자동으로 만들려면 배포하는 동안 BDC에 AD 계정이 필요합니다. 이 계정에는 제공된 OU 내에 사용자, 그룹 및 머신 계정을 만들 수 있는 권한이 있어야 합니다.

아래 단계에서는 Active Directory 도메인 컨트롤러가 이미 있다고 가정합니다. 도메인 컨트롤러가 없는 경우 도움이 될 수 있는 단계는 이 [가이드](https://social.technet.microsoft.com/wiki/contents/articles/37528.create-and-configure-active-directory-domain-controller-in-azure-windows-server.aspx)에 포함되어 있습니다.

## <a name="create-ad-objects"></a>AD 개체 만들기

AD 통합을 사용하여 BDC를 배포하기 전에 다음 작업을 수행합니다.

1. 모든 BDC AD 개체가 저장되는 OU(조직 구성 단위)를 만듭니다. 배포 시 기존 OU를 지정하도록 선택할 수도 있습니다.
1. BDC에 대한 AD 계정을 만들거나, 기존 BDC AD 계정을 사용하여 올바른 권한을 이 계정에 제공합니다.

### <a name="create-a-user-in-ad-for-bdc-domain-service-account"></a>AD에서 BDC 도메인 서비스 계정에 대한 사용자 만들기

빅 데이터 클러스터에는 특정 권한이 있는 계정이 필요합니다. 계속하기 전에 기존 AD 계정이 있는지 확인하거나 빅 데이터 클러스터에서 필요한 개체를 설정하는 데 사용할 수 있는 새 계정을 만들어야 합니다.

AD에서 새 사용자를 만들려면 마우스 오른쪽 단추로 도메인 또는 OU를 클릭하고, **새로 만들기** > **사용자**를 차례로 선택하면 됩니다.

![image12](./media/deploy-active-directory/image12.png)

이 문서에서는 이 사용자를 *BDC 도메인 서비스 계정*이라고 합니다.

### <a name="creating-an-ou"></a>OU 만들기

도메인 컨트롤러에서 **Active Directory 사용자 및 컴퓨터**를 엽니다. 왼쪽 패널에서 마우스 오른쪽 단추로 OU를 만들려는 디렉터리를 클릭하고, 새로 만들기 -\> **조직 구성 단위**를 차례로 선택한 다음, 마법사의 안내에 따라 OU를 만듭니다. 또는 PowerShell을 사용하여 OU를 만들 수 있습니다.

```powershell
New-ADOrganizationalUnit -Name "<name>" -Path "<Distinguished name of the directory you wish to create the OU in>"
```

이 문서의 예제에서는 OU 이름을 `bdc`로 지정합니다.

![image13](./media/deploy-active-directory/image13.png)

![image14](./media/deploy-active-directory/image14.png)

### <a name="setting-permissions-the-bdc-ad-account"></a>BDC AD 계정에 대한 권한 설정

새 AD 사용자를 만들었는지, 아니면 기존 AD 사용자를 사용하는지에 관계없이 사용자에게 필요한 특정 권한이 있습니다. 이 계정은 BDC 컨트롤러에서 클러스터를 AD에 조인할 때 사용하는 사용자 계정입니다.

BDC DSA(도메인 서비스 계정)는 OU에서 사용자, 그룹 및 컴퓨터 계정을 만들 수 있어야 합니다. 다음 단계에서는 BDC 도메인 서비스 계정의 이름을 `bdcDSA`로 지정했습니다. 이 계정의 이름은 임의로 선택할 수 있습니다.

1. 도메인 컨트롤러에서 **Active Directory 사용자 및 컴퓨터**를 엽니다.

1. 왼쪽 패널에서 도메인, `bdc`에서 사용할 OU로 차례로 이동합니다.

1. 마우스 오른쪽 단추로 OU를 클릭하고 **속성**을 선택합니다.

1. [보안] 탭으로 이동합니다(마우스 오른쪽 단추로 OU를 클릭하고 **보기**를 선택하여 **고급 기능**을 선택했는지 확인).

    ![image15](./media/deploy-active-directory/image15.png)

1. **추가...** 를 클릭하고, **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA** 사용자를 추가 합니다.

    ![image16](./media/deploy-active-directory/image16.png)

    ![image17](./media/deploy-active-directory/image17.png)

1. **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA** 사용자를 선택하고, 모든 권한을 지운 다음, **고급**을 클릭합니다.

1. **추가**를 클릭합니다.

    ![image18](./media/deploy-active-directory/image18.png)

    - **보안 주체 선택**을 클릭하고, **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA**를 삽입한 다음, [확인]을 클릭합니다.

    - **형식**을 **허용**으로 설정합니다.

    - **적용 대상**을 **이 개체 및 모든 하위 개체**로 설정합니다.

        ![image19](./media/deploy-active-directory/image19.png)

    - 아래쪽으로 스크롤하여 **모두 지우기**를 클릭합니다.

    - 위쪽으로 다시 스크롤하여 다음을 선택합니다.
       - **모든 속성 읽기**
       - **모든 속성 쓰기**
       - **컴퓨터 개체 만들기**
       - **컴퓨터 개체 삭제**
       - **그룹 개체 만들기**
       - **그룹 개체 삭제**
       - **사용자 개체 만들기**
       - **사용자 개체 삭제**

    - **확인**을 클릭합니다.

- **추가**를 클릭합니다.

    - **보안 주체 선택**을 클릭하고, **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA**를 삽입한 다음, [확인]을 클릭합니다.

    - **형식**을 **허용**으로 설정합니다.

    - **적용 대상**을 **하위 컴퓨터 개체**로 설정합니다.

    - 아래쪽으로 스크롤하여 **모두 지우기**를 클릭합니다.

    - 위쪽으로 다시 스크롤하여 **암호 재설정**을 선택합니다.

    - **확인**을 클릭합니다.

- **추가**를 클릭합니다.

    - **보안 주체 선택**을 클릭하고, **[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA**를 삽입한 다음, [확인]을 클릭합니다.

    - **형식**을 **허용**으로 설정합니다.

    - **적용 대상**을 **하위 사용자 개체**로 설정합니다.

    - 아래쪽으로 스크롤하여 **모두 지우기**를 클릭합니다.

    - 위쪽으로 다시 스크롤하여 **암호 재설정**을 선택합니다.

    - **확인**을 클릭합니다.

- **확인**을 두 번 더 클릭하여 열려 있는 대화 상자를 닫습니다.

## <a name="prepare-deployment"></a>배포 준비

AD 통합을 사용하여 BDC를 배포하는 경우 AD에서 BDC 관련 개체를 만들기 위해 제공해야 하는 몇 가지 추가 정보가 있습니다.

`kubeadm-prod` 프로필을 사용하면 AD 통합에 필요한 보안 관련 정보 및 엔드포인트 관련 정보에 대한 자리 표시자를 자동으로 갖게 됩니다.

또한 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]가 AD에서 필요한 개체를 만드는 데 사용할 자격 증명을 제공해야 합니다. 이러한 자격 증명은 환경 변수로 제공됩니다.

## <a name="set-security-environment-variables"></a>보안 환경 변수 설정

다음 환경 변수는 AD 통합을 설정하는 데 사용되는 BDC 도메인 서비스 계정의 자격 증명을 제공합니다. 이 계정은 BDC에서 BDC 관련 AD 개체를 유지하는 데도 사용합니다.

```bash
export DOMAIN_SERVICE_ACCOUNT_USERNAME=<AD principal account name>
export DOMAIN_SERVICE_ACCOUNT_PASSWORD=<AD principal password>
```

## <a name="provide-security-and-endpoint-parameters"></a>보안 및 엔드포인트 매개 변수 제공

자격 증명에 대한 환경 변수 외에도 AD 통합이 작동하기 위한 보안 및 엔드포인트 정보를 제공해야 합니다. 필요한 매개 변수는 `kubeadm-prod` [배포 프로필](deployment-guidance.md#configfile)에 자동으로 포함됩니다.

AD 통합에 필요한 매개 변수는 다음과 같습니다. 이 문서의 아래 부분에 나오는 `config replace` 명령을 사용하여 이러한 매개 변수를 `control.json` 및 `bdc.json` 파일에 추가합니다. 아래의 모든 예제에서는 `contoso.local` 도메인 예제를 사용합니다.

- `security.ouDistinguishedName`: 클러스터 배포에서 만든 모든 AD 계정이 추가될 OU(조직 구성 단위)의 고유 이름입니다. 도메인을 `contoso.local`이라고 하는 경우 OU의 고유 이름은 `OU=BDC,DC=contoso,DC=local`입니다.

- `security.dnsIpAddresses`: 도메인 컨트롤러의 IP 주소 목록입니다.

- `security.domainControllerFullyQualifiedDns`: 도메인 컨트롤러의 FQDN 목록입니다. FQDN에는 도메인 컨트롤러의 머신/호스트 이름이 포함됩니다. 여러 도메인 컨트롤러가 있는 경우 여기에 목록을 제공할 수 있습니다. 예: `HOSTNAME.CONTOSO.LOCAL`

- `security.realm` **선택적 매개 변수**: 대부분의 경우 영역은 도메인 이름과 동일합니다. 동일하지 않은 경우 이 매개 변수를 사용하여 영역 이름(예: `CONTOSO.LOCAL`)을 정의합니다.

- `security.domainDnsName`: 도메인 이름입니다(예: `contoso.local`).

- `security.clusterAdmins`: 이 매개 변수는 **one- AD 그룹**을 사용합니다. 이 그룹의 멤버는 클러스터에서 관리자 권한을 얻게 됩니다. 즉 SQL Server에 대한 sysadmin 권한, HDFS에 대한 슈퍼 사용자 권한 및 컨트롤러에 대한 관리자 권한을 갖습니다. **배포를 시작하기 전에 이 그룹이 AD에 있어야 합니다. 또한 이 그룹은 Active Directory에서 DomainLocal로 범위가 지정될 수 없습니다. 도메인 로컬 범위 그룹으로 인해 배포가 실패합니다.**

- `security.clusterUsers`: 빅 데이터 클러스터에서 일반 사용자(관리자 권한 없음)인 AD 그룹의 목록입니다. **배포를 시작하기 전에 이러한 그룹이 AD에 있어야 합니다. 또한 이러한 그룹은 Active Directory에서 DomainLocal로 범위가 지정될 수 없습니다. 도메인 로컬 범위 그룹으로 인해 배포가 실패합니다.**

- `security.appOwners` **선택적 매개 변수**: 애플리케이션을 만들고, 삭제하고, 실행할 수 있는 권한이 있는 AD 그룹의 목록입니다. **배포를 시작하기 전에 이러한 그룹이 AD에 있어야 합니다. 또한 이러한 그룹은 Active Directory에서 DomainLocal로 범위가 지정될 수 없습니다. 도메인 로컬 범위 그룹으로 인해 배포가 실패합니다.**

- `security.appReaders`**선택적 매개 변수**: 애플리케이션을 실행할 수 있는 권한이 있는 AD 그룹의 목록입니다. **배포를 시작하기 전에 이러한 그룹이 AD에 있어야 합니다. 또한 이러한 그룹은 Active Directory에서 DomainLocal로 범위가 지정될 수 없습니다. 도메인 로컬 범위 그룹으로 인해 배포가 실패합니다.**

**AD 그룹 범위를 확인하는 방법:** 
AD 그룹의 범위를 확인하여 DomainLocal인지 살펴보기 위한 지침을 보려면 [여기를 클릭](https://docs.microsoft.com/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps)하세요.

배포 구성 파일을 아직 초기화하지 않은 경우 다음 명령을 실행하여 구성의 복사본을 가져올 수 있습니다.

```bash
azdata bdc config init --source kubeadm-prod  --target custom-prod-kubeadm
```

`control.json` 파일에서 위의 매개 변수를 설정하려면 다음 `azdata` 명령을 사용합니다. 이러한 명령은 구성을 바꾸고, 배포하기 전에 사용자 고유의 값을 제공합니다.

아래 예제에서는 배포 구성의 AD 관련 매개 변수 값을 바꿉니다. 아래의 도메인 세부 정보는 예제 값입니다.

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

위의 정보 외에도 다른 클러스터 엔드포인트에 대한 DNS 이름을 제공해야 합니다. 제공된 DNS 이름을 사용하는 DNS 항목은 배포 시 DNS 서버에 자동으로 만들어집니다. 이러한 이름은 다른 클러스터 엔드포인트에 연결할 때 사용됩니다. 예를 들어 SQL 마스터 인스턴스의 DNS 이름이 `mastersql`이면 `mastersql.contoso.local,31433`을 사용하여 도구에서 마스터 인스턴스에 연결합니다.

> [!NOTE]
> DNS 항목을 아래에서 정의하는 이름으로 DNS 서버에 만들어야 합니다. 예를 들어 `kubeadm` 배포의 경우 DNS 항목을 만들 때 Kubernetes 마스터 노드의 IP 주소를 사용할 수 있습니다.

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[1].dnsName=<monitoring services DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=<SQL Master Primary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=<SQL Master Secondary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=<Gateway (Knox) DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=<app proxy DNS name>.<Domain name. e.g. contoso.local>"
```

여기서 [AD 통합을 사용하여 SQL Server 빅 데이터 클러스터를 단일 노드 Kubernetes 클러스터(kubeadm)에 배포](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm-ad)하는 스크립트 예제를 찾을 수 있습니다.

이제 Active Directory 통합을 사용하여 BDC를 배포하는 데 필요한 모든 매개 변수를 설정해야 합니다.

[!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]를 배포하는 방법에 대한 전체 설명서는 [공식 설명서](deployment-guidance.md)를 참조하세요.

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>도메인 컨트롤러에 대한 역방향 DNS 항목 확인

DNS 서버에 등록된 도메인 컨트롤러 자체에 대한 역방향 DNS 항목(PTR 레코드)이 있는지 확인합니다. 도메인 컨트롤러에서 도메인 이름의 `nslookup`을 실행하여 도메인 컨트롤러 IP 주소로 확인할 수 있는지 알아볼 수 있습니다.

## <a name="connect-to-cluster-endpoints-in-ad-mode"></a>AD 모드에서 클러스터 엔드포인트에 연결

AD 인증을 사용하여 SQL Server 마스터 인스턴스에 로그인합니다.

SQL Server 인스턴스에 대한 AD 연결을 확인하려면 `sqlcmd`를 사용하여 SQL 마스터 인스턴스에 연결합니다. 배포 시 제공된 그룹(`clusterUsers` 및 `clusterAdmins`)에 대한 로그인이 자동으로 만들어집니다.

Linux를 사용하는 경우 먼저 `kinit`를 AD 사용자 권한으로 실행한 다음, `sqlcmd`를 실행합니다. Windows를 사용하는 경우 **도메인 조인 클라이언트 머신**에서 원하는 사용자 권한으로 로그인하면 됩니다.

### <a name="connect-to-master-instance-from-linuxmac"></a>Linux/Mac에서 마스터 인스턴스에 연결

```bash
kinit <username>@<domain name>
sqlcmd -S <DNS name for master instance>,31433 -E
```

### <a name="connect-to-master-instance-from-windows"></a>Windows에서 마스터 인스턴스에 연결

```cmd
sqlcmd -S <DNS name for master instance>,31433 -E
```

### <a name="log-in-to-sql-server-master-instance-using-azure-data-studio-or-ssms"></a>Azure Data Studio 또는 SSMS를 사용하여 SQL Server 마스터 인스턴스에 로그인

도메인 조인 클라이언트에서 SSMS 또는 Azure Data Studio를 열어 마스터 인스턴스에 연결할 수 있습니다. 이는 AD 인증을 사용하여 SQL Server 인스턴스에 연결하는 것과 동일한 환경입니다.

SSMS에서:

![image23](./media/deploy-active-directory/image23.png)

Azure Data Studio에서:

![image24](./media/deploy-active-directory/image24.png)}

### <a name="log-in-to-controller-with-ad-authentication"></a>AD 인증을 사용하여 컨트롤러에 로그인

#### <a name="connect-to-controller-with-ad-authentication-from-linuxmac"></a>Linux/Mac에서 AD 인증을 사용하여 컨트롤러에 연결

`azdata` 및 AD 인증을 사용하여 컨트롤러 엔드포인트에 연결할 수 있습니다.

```bash
kinit <username>@<domain name>
azdata login -e https://<controller DNS name>:30080 --auth ad
```

#### <a name="connect-to-controller-with-ad-authentication-from-windows"></a>Windows에서 AD 인증을 사용하여 컨트롤러에 연결

```cmd
azdata login -e https://<controller DNS name>:30080 --auth ad
```

### <a name="use-ad-authentication-to-knox-gateway-webhdfs"></a>Knox 게이트웨이에 AD 인증 사용(webHDFS)

Knox 게이트웨이 엔드포인트를 통해 curl을 사용하여 HDFS 명령을 실행할 수도 있습니다. 이 경우 Knox에 대한 AD 인증이 필요합니다. 아래 curl 명령은 Knox 게이트웨이를 통해 webHDFS REST 호출을 실행하여 `products`라는 디렉터리를 만듭니다.

```bash
curl -k -v --negotiate -u : https://<Gateway DNS name>:30443/gateway/default/webhdfs/v1/products?op=MKDIRS -X PUT
```

## <a name="known-issues-and-limitations"></a>알려진 문제 및 제한 사항

**이 릴리스에서 알아야 할 제한 사항:**

- 현재 로그 검색 대시보드 및 메트릭 대시보드는 AD 인증을 지원하지 않습니다. 이 엔드포인트에 대한 AD 지원은 향후 릴리스에 예정되어 있습니다. 배포 시 설정된 기본 사용자 이름과 암호를 사용하여 이러한 대시보드를 인증할 수 있습니다. 다른 모든 클러스터 엔드포인트는 AD 인증을 지원합니다.

- 보안 AD 모드는 현재 `kubeadm` 배포 환경에서만 작동하며, AKS에서는 작동하지 않습니다. `kubeadm-prod` 배포 프로필에는 기본적으로 보안 섹션이 포함됩니다.

- 현재 도메인당 하나의 BDC만 허용됩니다. 도메인당 여러 BDC를 사용하도록 설정하는 것은 향후 릴리스에 예정되어 있습니다.

- 보안 구성에 지정된 AD 그룹은 DomainLocal 범위를 지정할 수 없습니다. [이러한 지침](https://docs.microsoft.com/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps)에 따라 AD 그룹의 범위를 확인할 수 있습니다.
