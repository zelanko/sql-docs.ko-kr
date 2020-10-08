---
title: Azure Red Hat OpenShift에 배포 python 스크립트
titleSuffix: SQL Server Big Data Clusters
description: 배포 스크립트를 사용하여 ARO(Azure Red Hat OpenShift)에 SQL Server 빅 데이터 클러스터를 배포하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f74a46d13c907bd81e3afe4af7ba8db38a515e00
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725783"
---
# <a name="use-a-python-script-to-deploy-a-sql-server-big-data-cluster-on-azure-red-hat-openshift-aro"></a>python 스크립트를 사용하여 ARO(Azure Red Hat OpenShift)에 SQL Server 빅 데이터 클러스터 배포

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 자습서에서는 샘플 python 배포 스크립트를 사용하여 [ARO(Azure Red Hat OpenShift)](/azure/virtual-machines/linux/openshift-get-started)에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]를 배포합니다. 이 배포 옵션은 SQL Server 2019 CU5부터 지원됩니다.

> [!TIP]
> ARO는 빅 데이터 클러스터를 위해 Kubernetes를 호스팅하는 옵션 중 하나일 뿐입니다. 다른 배포 옵션 및 배포 옵션을 사용자 지정하는 방법에 대한 자세한 내용은 [Kubernetes에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md)을 참조하세요.


> [!WARNING]
> 기본 제공 스토리지 클래스인 *managed-premium*을 사용하여 만든 영구 볼륨에는 삭제 회수 정책이 지정됩니다. 따라서 빅 데이터 클러스터 SQL Server를 삭제하는 경우 영구적 볼륨과 마찬가지로 영구적 볼륨 클레임이 삭제됩니다. [스토리지 개념](/azure/aks/concepts-storage/#storage-classes)에 설명된 대로 유지 회수 정책으로 azure-disk 프로비저닝 프로그램을 사용하여 사용자 지정 스토리지 클래스를 만들어야 합니다. 아래 스크립트는 *managed-premium* 스토리지 클래스를 사용합니다. 자세한 내용은 [데이터 지속성](concept-data-persistence.md) 항목을 참조하세요.

여기서 사용하는 기본 빅 데이터 클러스터 배포는 SQL 마스터 인스턴스 1개, 컴퓨팅 풀 인스턴스 1개, 데이터 풀 인스턴스 2개, 스토리지 풀 인스턴스 2개로 구성되어 있습니다. 데이터는 ARO 기본 스토리지 클래스를 사용하는 Kubernetes 영구적 볼륨을 사용하여 유지됩니다. 이 자습서에서 사용하는 기본 구성은 개발/테스트 환경에 적합합니다.

## <a name="prerequisites"></a>사전 요구 사항

- Azure 구독
- [oc](https://docs.openshift.com/container-platform/4.4/cli_reference/openshift_cli/getting-started-cli.html)
- [Python 최소 버전 3.0](https://www.python.org/downloads)
- [`az` CLI](/cli/azure/install-azure-cli/)
- [`azdata` CLI](../azdata/install/deploy-install-azdata.md)
- **Azure Data Studio**

## <a name="log-in-to-your-azure-account"></a>Azure 계정에 로그인

스크립트는 Azure CLI를 사용하여 ARO 클러스터 생성을 자동화합니다. 스크립트를 실행하기 전에 Azure CLI를 사용하여 Azure 계정에 한 번 이상 로그인해야 합니다. 명령 프롬프트에서 다음 명령을 실행합니다.

```terminal
az login
```

## <a name="instructions"></a>Instructions

1. Python 스크립트 `deploy-sql-big-data-aro.py` 및 yaml 파일 `bdc-scc.yaml`을 모두 다운로드합니다.

   >이러한 파일은 이 문서의 다음 위치에 있습니다.
   - [`deploy-sql-big-data-aro.py`](#deploy-sql-big-data-aropy)
   - [`bdc-scc.yaml`](#bdc-sccyaml)

1. 다음을 사용하여 스크립트를 실행합니다.

```terminal
python deploy-sql-big-data-aro.py
```

메시지가 표시되면 Azure 구독 ID 및 Azure 리소스 그룹에 대한 입력을 제공하여 리소스를 만듭니다. 필요에 따라 다른 구성에 대한 입력을 제공하거나 제공된 기본값을 사용할 수도 있습니다. 예를 들면 다음과 같습니다.

- `azure_region`
- `vm_size`(OpenShift 작업자 노드의 경우). 기본 시나리오의 유효성을 검사하는 동안 최적의 경험을 위해 클러스터의 모든 작업자 노드에서 최소 8개의 vCPU와 64GB 메모리를 권장합니다. 스크립트는 기본적으로 `Standard_D8s_v3` 및 3개의 작업자 노드를 사용합니다. 빅 데이터 클러스터의 기본 크기 구성은 모든 구성 요소에서 영구 볼륨 클레임에 약 24개의 디스크를 사용합니다.
- OpenShift 클러스터 배포용 네트워크 구성 - 각 매개 변수에 대한 자세한 내용은 [ARO 배포 문서](\azure\openshift\tutorial-create-cluster)를 참조하세요.
- `cluster_name` -이 값은 ARO 클러스터 및 ARO 위에 생성된 SQL Server 빅 데이터 클러스터에 모두 사용됩니다. SQL 빅 데이터 클러스터의 이름은 Kubernetes 네임스페이스가 됩니다.
- `username ` - 컨트롤러 관리자 계정, SQL Server 마스터 인스턴스 계정, 게이트웨이에 대한 배포 도중에 프로비저닝되는 계정의 사용자 이름입니다. 모범 사례로 `sa` SQL Server 계정이 사용하지 않도록 자동 설정됩니다.
- `password` - 모든 계정에 동일한 값이 사용됩니다.

SQL Server 빅 데이터 클러스터가 ARO에 배포되었습니다. 이제 Azure Data Studio를 사용하여 클러스터에 연결할 수 있습니다. 자세한 내용은 [Azure Data Studio를 사용하여 SQL Server 빅 데이터 클러스터에 연결](connect-to-big-data-cluster.md)을 참조하세요.

## <a name="clean-up"></a>정리

Azure에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 테스트하는 경우 예기치 않은 요금이 청구되지 않도록, 작업이 완료되면 ARO 클러스터를 삭제해야 합니다. 계속 사용하려는 경우에는 클러스터를 제거하지 않습니다.

> [!WARNING]
> 다음 단계에서는 ARO 클러스터를 삭제하며, 따라서 SQL Server 빅 데이터 클러스터도 제거됩니다. 유지하려는 데이터베이스 또는 HDFS 데이터가 있는 경우 클러스터를 삭제하기 전에 해당 데이터를 백업합니다.

다음 Azure CLI 명령을 실행하여 Azure에서 빅 데이터 클러스터 및 ARO 서비스를 제거합니다(`<resource group name>`을 배포 스크립트에서 지정한 **Azure 리소스 그룹**으로 바꿈).

```terminal
az group delete -n <resource group name>
```

## `deploy-sql-big-data-aro.py` 

이 섹션의 스크립트는 Azure Red Hat OpenShift에 SQL Server 빅 데이터 클러스터를 배포합니다. 배포를 시작하기 전에 스크립트를 워크스테이션에 복사하고 `deploy-sql-big-data-aro.py`로 저장합니다.

```python
#
# Prerequisites: 
# 
# Azure CLI (https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), azdata CLI (https://docs.microsoft.com/en-us/sql/big-data-cluster/deploy-install-azdata?view=sql-server-ver15), oc CLI (https://www.openshift.com/blog/installing-oc-tools-windows)
#
# Run `az login` at least once BEFORE running this script
#

from subprocess import check_output, CalledProcessError, STDOUT, Popen, PIPE, getoutput
from time import sleep
import os
import getpass
import json

def executeCmd (cmd):
    if os.name=="nt":
        process = Popen(cmd.split(),stdin=PIPE, shell=True)
    else:
        process = Popen(cmd.split(),stdin=PIPE)
    stdout, stderr = process.communicate()
    if (stderr is not None):
        raise Exception(stderr)

#
# MUST INPUT THESE VALUES!!!!!
#
SUBSCRIPTION_ID = input("Provide your Azure subscription ID:").strip()
GROUP_NAME = input("Provide Azure resource group name to be created:").strip()
#
# This password will be use for Controller user, Gateway user and SQL Server Master SA accounts
AZDATA_USERNAME=input("Provide username to be used for Controller, SQL Server and Gateway endpoints - Press ENTER for using  `admin`:").strip() or "admin"
AZDATA_PASSWORD = getpass.getpass("Provide password to be used for Controller user, Gateway user and SQL Server Master accounts:")
#
# Optionally change these configuration settings
#
AZURE_REGION=input("Provide Azure region - Press ENTER for using `westus2`:").strip() or "westus2"
# MASTER_VM_SIZE=input("Provide VM size for master nodes for the ARO cluster - Press ENTER for using  `Standard_D2s_v3`:").strip() or "Standard_D2s_v3"
WORKER_VM_SIZE=input("Provide VM size for the worker nodes for the ARO cluster - Press ENTER for using  `Standard_D8s_v3`:").strip() or "Standard_D8s_v3"
OC_NODE_COUNT=input("Provide number of worker nodes for ARO cluster - Press ENTER for using  `3`:").strip() or "3"
VNET_NAME=input("Provide name of Virtual Network for ARO cluster - Press ENTER for using  `aro-vnet`:").strip() or "aro-vnet"
VNET_ADDRESS_SPACE=input("Provide Virtual Network Address Space for ARO cluster - Press ENTER for using  `10.0.0.0/16`:").strip() or "10.0.0.0/16"
MASTER_SUBNET_NAME=input("Provide Master Subnet Name for ARO cluster - Press ENTER for using  `master-subnet`:").strip() or "master-subnet"
MASTER_SUBNET_IP_RANGE=input("Provide address range of Master Subnet for ARO cluster - Press ENTER for using  `10.0.0.0/23`:").strip() or "10.0.0.0/23"
WORKER_SUBNET_NAME=input("Provide Worker Subnet Name for ARO cluster - Press ENTER for using  `worker-subnet`:").strip() or "worker-subnet"
WORKER_SUBNET_IP_RANGE=input("Provide address range of Worker Subnet for ARO cluster - Press ENTER for using  `10.0.2.0/23`:").strip() or "10.0.2.0/23"
#
# This is both Kubernetes cluster name and SQL Big Data cluster name
CLUSTER_NAME=input("Provide name of OpenShift cluster and SQL big data cluster - Press ENTER for using  `sqlbigdata`:").strip() or "sqlbigdata"
#
# Deploy the ARO cluster
#  
print ("Set azure context to subscription: "+SUBSCRIPTION_ID)
command = "az account set -s "+ SUBSCRIPTION_ID
executeCmd (command)
print ("Creating azure resource group: "+GROUP_NAME)
command="az group create --name "+GROUP_NAME+" --location "+AZURE_REGION
executeCmd (command)
command = "az network vnet create --resource-group "+GROUP_NAME+" --name "+VNET_NAME+" --address-prefixes "+VNET_ADDRESS_SPACE
print("Creating Virtual Network: "+VNET_NAME)
executeCmd(command)
command = "az network vnet subnet create --resource-group "+GROUP_NAME+" --vnet-name "+VNET_NAME+" --name "+MASTER_SUBNET_NAME+" --address-prefixes "+MASTER_SUBNET_IP_RANGE+" --service-endpoints Microsoft.ContainerRegistry"
print("Creating Master Subnet: "+MASTER_SUBNET_NAME)
executeCmd(command)
command = "az network vnet subnet create --resource-group "+GROUP_NAME+" --vnet-name "+VNET_NAME+" --name "+WORKER_SUBNET_NAME+" --address-prefixes "+WORKER_SUBNET_IP_RANGE+" --service-endpoints Microsoft.ContainerRegistry"
print("Creating Worker Subnet: "+WORKER_SUBNET_NAME)
executeCmd(command)
command = "az network vnet subnet update --name "+MASTER_SUBNET_NAME+" --resource-group "+GROUP_NAME+" --vnet-name "+VNET_NAME+" --disable-private-link-service-network-policies true"
print("Updating Master Subnet by disabling Private Link Policies")
executeCmd(command)
command = "az aro create --resource-group "+GROUP_NAME+" --name "+CLUSTER_NAME+" --vnet "+VNET_NAME+" --master-subnet "+MASTER_SUBNET_NAME+" --worker-subnet "+WORKER_SUBNET_NAME+" --worker-count "+OC_NODE_COUNT+" --worker-vm-size "+WORKER_VM_SIZE +" --only-show-errors"
print("Creating OpenShift cluster: "+CLUSTER_NAME)
executeCmd (command)
#
# Login to oc console
#
command = "az aro list-credentials --name "+CLUSTER_NAME+" --resource-group "+GROUP_NAME +" --only-show-errors"
output=json.loads(getoutput(command))
OC_CLUSTER_USERNAME = str(output['kubeadminUsername'])
OC_CLUSTER_PASSWORD = str(output['kubeadminPassword'])
command = "az aro show --name "+CLUSTER_NAME+" --resource-group "+GROUP_NAME +" --only-show-errors"
output=json.loads(getoutput(command))
APISERVER = str(output['apiserverProfile']['url'])
command = "oc login "+ APISERVER+ " -u " + OC_CLUSTER_USERNAME + " -p "+ OC_CLUSTER_PASSWORD
executeCmd (command)
#
# Setup pre-requisites for deploying BDC on OpenShift
#
#
#Creating new project/namespace
command = "oc new-project "+ CLUSTER_NAME
executeCmd (command)
#
# create custom SCC for BDC
command = "oc apply -f bdc-scc.yaml"
executeCmd (command)
#
#Adding the custom scc to BDC namespace
command = "oc adm policy add-scc-to-group bdc-scc system:serviceaccounts:" + CLUSTER_NAME
executeCmd (command)
#
# Deploy big data cluster
#
print ('Set environment variables for credentials')
os.environ['AZDATA_PASSWORD'] = AZDATA_PASSWORD
os.environ['AZDATA_USERNAME'] = AZDATA_USERNAME
os.environ['ACCEPT_EULA']="Yes"
#
#Creating azdata configuration with aro-dev-test profile
command = "azdata bdc config init --source aro-dev-test --target custom --force"
executeCmd (command)
command="azdata bdc config replace -c custom/bdc.json -j ""metadata.name=" + CLUSTER_NAME + ""
executeCmd (command)
#
# Create BDC
command = "azdata bdc create --config-profile custom --accept-eula yes"
executeCmd(command)
#login into BDC cluster and list endpoints
command="azdata login -n " + CLUSTER_NAME
executeCmd (command)
print("")
print("SQL Server big data cluster endpoints: ")
command="azdata bdc endpoint list -o table"
executeCmd(command)
```

## `bdc-scc.yaml`

다음 .yaml 매니페스트는 빅 데이터 클러스터 배포를 위한 사용자 지정 SCC(보안 컨텍스트 제약 조건)를 정의합니다. `deploy-sql-big-data-aro.py`와 동일한 디렉터리에 복사합니다.

```yaml
allowHostDirVolumePlugin: false
allowHostIPC: false
allowHostNetwork: false
allowHostPID: false
allowHostPorts: false
allowPrivilegeEscalation: true
allowPrivilegedContainer: false
allowedCapabilities:
  - SETUID
  - SETGID
  - CHOWN
  - SYS_PTRACE
apiVersion: security.openshift.io/v1
defaultAddCapabilities: null
fsGroup:
  type: RunAsAny
kind: SecurityContextConstraints
metadata:
  annotations:
    kubernetes.io/description: SQL Server BDC custom scc is based on 'nonroot' scc plus additional capabilities required by BDC.
  generation: 2
  name: bdc-scc
readOnlyRootFilesystem: false
requiredDropCapabilities:
  - KILL
  - MKNOD
runAsUser:
  type: MustRunAsNonRoot
seLinuxContext:
  type: MustRunAs
supplementalGroups:
  type: RunAsAny
volumes:
  - configMap
  - downwardAPI
  - emptyDir
  - persistentVolumeClaim
  - projected
  - secret
```

## <a name="next-steps"></a>다음 단계

배포 스크립트는 Azure Kubernetes Service를 구성하고 SQL Server 2019 빅 데이터 클러스터도 배포했습니다. 수동 설치를 통해 이후 배포를 사용자 지정할 수도 있습니다. 빅 데이터 클러스터를 배포하는 방법 및 배포를 사용자 지정하는 방법에 대한 자세한 내용은 [Kubernetes에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md)을 참조하세요.

이제 SQL Server 빅 데이터 클러스터가 배포되었으므로 샘플 데이터를 로드하고 자습서를 살펴볼 수 있습니다.

> [!div class="nextstepaction"]
> [자습서: SQL Server 2019 빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)