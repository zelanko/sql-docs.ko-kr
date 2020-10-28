---
title: 배포 구성
titleSuffix: SQL Server big data clusters
description: azdata 관리 도구에 기본 제공되는 구성 파일을 사용하여 빅 데이터 클러스터 배포를 사용자 지정하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cef348aee2b917b0a6afd61d30b5e4f7fa7da665
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257204"
---
# <a name="configure-deployment-settings-for-cluster-resources-and-services"></a>클러스터 리소스 및 서비스에 대한 배포 설정 구성

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] 관리 도구에 기본적으로 제공되는 미리 정의된 구성 프로필 세트에서 시작하여 BDC 워크로드 요구 사항에 더 잘 맞도록 기본 설정을 쉽게 수정할 수 있습니다. 구성 파일의 구조를 사용하면 리소스의 각 서비스에 대한 설정을 세부적으로 업데이트할 수 있습니다.

빅 데이터 클러스터 구성에 대한 개요는 13분 분량의 다음 동영상을 시청하세요.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Big-Data-Cluster-Configuration/player?WT.mc_id=dataexposed-c9-niner]

> [!TIP]
> 고가용성 서비스를 배포하는 방법에 대한 자세한 내용은 [SQL Server 마스터](deployment-high-availability.md) 또는 [HDFS 이름 노드](deployment-high-availability-hdfs-spark.md)와 같은 중요 업무용 구성 요소에 **고가용성** 을 구성하는 방법에 대한 문서를 참조하세요.

또한 리소스 수준 구성을 설정하거나 리소스의 모든 서비스에 대한 구성을 업데이트할 수도 있습니다. `bdc.json` 구조에 대한 요약은 다음과 같습니다.

```json
{
    "apiVersion": "v1",
    "metadata": {
        "kind": "BigDataCluster",
        "name": "mssql-cluster"
    },
    "spec": {
        "resources": {
            "nmnode-0": {...
            },
            "sparkhead": {...
            },
            "zookeeper": {...
            },
            "gateway": {...
            },
            "appproxy": {...
            },
            "master": {...
            },
            "compute-0": {...
            },
            "data-0": {...
            },
            "storage-0": {...
        },
        "services": {
            "sql": {
                "resources": [
                    "master",
                    "compute-0",
                    "data-0",
                    "storage-0"
                ]
            },
            "hdfs": {
                "resources": [
                    "nmnode-0",
                    "zookeeper",
                    "storage-0",
                    "sparkhead"
                ],
                "settings": {...
            },
            "spark": {
                "resources": [
                    "sparkhead",
                    "storage-0"
                ],
                "settings": {...
            }
        }
    }
}
```

풀의 인스턴스와 같은 리소스 수준 구성을 업데이트하는 경우 사양을 업데이트합니다. 예를 들어 컴퓨팅 풀의 인스턴스 수를 업데이트하려면 `bdc.json` 구성 파일에서 다음 섹션을 수정합니다.

```json
"resources": {
    ...
    "compute-0": {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Compute",
            "replicas": 4
        }
    }
    ...
}
``` 

특정 리소스 내에서 단일 서비스의 설정을 변경하는 경우에도 마찬가지입니다. 예를 들어 스토리지 풀의 Spark 구성 요소에 대해서만 Spark 메모리 설정을 변경하려면 `storage-0` 리소스를 `bdc.json` 구성 파일의 `spark` 서비스에 대한 `settings` 섹션으로 업데이트합니다.

```json
"resources":{
    ...
     "storage-0": {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Storage",
            "replicas": 2,
            "settings": {
                "spark": {
                    "spark-defaults-conf.spark.driver.memory": "2g",
                    "spark-defaults-conf.spark.driver.cores": "1",
                    "spark-defaults-conf.spark.executor.instances": "3",
                    "spark-defaults-conf.spark.executor.memory": "1536m",
                    "spark-defaults-conf.spark.executor.cores": "1",
                    "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
                    "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
                    "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
                    "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
                    "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
                }
            }
        }
    }
    ...
}
```

동일한 구성을 여러 리소스와 연결된 서비스에 적용하려면 `services` 섹션에서 해당 `settings`를 업데이트합니다. 예를 들어 스토리지 풀과 Spark 풀 모두에서 Spark에 대해 동일한 설정을 지정하려면 `bdc.json` 구성 파일의 `spark` 서비스 섹션에서 `settings` 섹션을 업데이트합니다.

```json
"services": {
    ...
    "spark": {
        "resources": [
            "sparkhead",
            "storage-0"
        ],
        "settings": {
            "spark-defaults-conf.spark.driver.memory": "2g",
            "spark-defaults-conf.spark.driver.cores": "1",
            "spark-defaults-conf.spark.executor.instances": "3",
            "spark-defaults-conf.spark.executor.memory": "1536m",
            "spark-defaults-conf.spark.executor.cores": "1",
            "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
            "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
            "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
            "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
            "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
        }
    }
    ...
}
```

클러스터 배포 구성 파일을 사용자 지정하려면 VSCode와 같은 JSON 형식 편집기를 사용할 수 있습니다. 자동화를 위해 이러한 편집 작업을 스크립팅하려면 `azdata bdc config` 명령을 사용합니다. 이 문서에서는 배포 구성 파일을 수정하여 빅 데이터 클러스터 배포를 구성하는 방법을 설명합니다. 각기 다른 시나리오에 맞게 구성을 변경하는 방법의 예제를 제공합니다. 배포에서 구성 파일을 사용하는 방법에 대한 자세한 내용은 [배포 지침](deployment-guidance.md#configfile)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

- [azdata 설치](../azdata/install/deploy-install-azdata.md).

- 이 섹션의 각 예제에서는 표준 구성 중 하나의 복사본을 만들었다고 가정합니다. 자세한 내용은 [사용자 지정 구성 만들기](deployment-guidance.md#customconfig)를 참조하세요. 예를 들어 다음 명령은 기본 `aks-dev-test` 구성에 따라 두 개의 JSON 배포 구성 파일(`bdc.json` 및 `control.json`)을 포함하는 `custom-bdc`라는 디렉터리를 만듭니다.

   ```bash
   azdata bdc config init --source aks-dev-test --target custom-bdc
   ```

## <a name="change-default-docker-registry-repository-and-images-tag"></a><a id="docker"></a> 기본 Docker 레지스트리, 리포지토리 및 이미지 태그 변경

기본 제공 구성 파일, 특히 control.json에는 컨테이너 레지스트리, 리포지토리 및 이미지 태그가 미리 채워진 `docker` 섹션이 포함되어 있습니다. 기본적으로 빅 데이터 클러스터에 필요한 이미지는 `mssql/bdc` 리포지토리의 Microsoft Container Registry(`mcr.microsoft.com`)에 있습니다.

```json
{
    "apiVersion": "v1",
    "metadata": {
        "kind": "Cluster",
        "name": "mssql-cluster"
    },
    "spec": {
        "docker": {
            "registry": "mcr.microsoft.com",
            "repository": "mssql/bdc",
            "imageTag": "2019-GDR1-ubuntu-16.04",
            "imagePullPolicy": "Always"
        },
        ...
    }
}
```

배포하기 전에 `control.json` 구성 파일을 직접 편집하거나 `azdata bdc config` 명령을 사용하여 `docker` 설정을 사용자 지정할 수 있습니다. 예를 들어 다음 명령은 다른 `<registry>`, `<repository>` 및 `<image_tag>`를 사용하여 `custom-bdc` control.json 구성 파일을 업데이트합니다.

```bash
azdata bdc config replace -c custom-bdc/control.json -j "$.spec.docker.registry=<registry>"
azdata bdc config replace -c custom-bdc/control.json -j "$.spec.docker.repository=<repository>"
azdata bdc config replace -c custom-bdc/control.json -j "$.spec.docker.imageTag=<image_tag>"
```

> [!TIP]
> 버전별 이미지 태그는 사용하지만 `latest` 이미지 태그는 사용하지 않는 것이 좋습니다. 그렇지 않으면 이로 인해 클러스터 상태 문제가 발생하는 버전이 일치하지 않을 수 있습니다.

> [!TIP]
> 빅 데이터 클러스터 배포를 배포하는 경우 컨테이너 이미지를 가져올 컨테이너 레지스트리와 리포지토리에 액세스할 수 있어야 합니다. 환경에서 기본 Microsoft Container Registry에 액세스할 수 없는 경우 필요한 이미지가 먼저 프라이빗 Docker 리포지토리에 배치되는 오프라인 설치를 수행할 수 있습니다. 오프라인 설치에 대한 자세한 내용은[SQL Server 빅 데이터 클러스터의 오프라인 배포 수행](deploy-offline.md)을 참조하세요. 배포를 실행하기 전에 배포 워크플로에서 프라이빗 리포지토리에 액세스하여 이미지를 끌어오도록 `DOCKER_USERNAME` 및 `DOCKER_PASSWORD` [환경 변수](deployment-guidance.md#env)를 설정해야 합니다.

## <a name="change-cluster-name"></a><a id="clustername"></a> 클러스터 이름 변경

클러스터 이름은 빅 데이터 클러스터의 이름과 배포 시 생성되는 Kubernetes 네임스페이스로 구성됩니다. 이는 `bdc.json` 배포 구성 파일의 다음 부분에 지정되어 있습니다.

```json
"metadata": {
    "kind": "BigDataCluster",
    "name": "mssql-cluster"
},
```

다음 명령은 키-값 쌍을 `--json-values` 매개 변수에 보내서 빅 데이터 클러스터 이름을 `test-cluster`로 변경합니다.

```bash
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> 빅 데이터 클러스터 이름은 소문자 영숫자여야 하고 공백을 포함하지 않아야 합니다. 클러스터의 모든 Kubernetes 아티팩트(컨테이너, Pod, 상태 저장 세트, 서비스)는 지정된 클러스터 이름과 동일한 이름의 네임스페이스에 생성됩니다.

## <a name="update-endpoint-ports"></a><a id="ports"></a> 엔드포인트 포트 업데이트

엔드포인트는 컨트롤러의 경우 `control.json`에서 정의되고, 게이트웨이 및 SQL Server 마스터 인스턴스의 경우 `bdc.json`의 해당 섹션에서 정의됩니다. `control.json` 구성 파일의 다음 부분에서는 컨트롤러의 엔드포인트 정의를 보여 줍니다.

```json
{
  "endpoints": [
    {
      "name": "Controller",
      "serviceType": "LoadBalancer",
      "port": 30080
    },
    {
      "name": "ServiceProxy",
      "serviceType": "LoadBalancer",
      "port": 30777
    }
  ]
}
```

다음 예제에서는 인라인 JSON을 사용하여 `controller` 엔드포인트의 포트를 변경합니다.

```bash
azdata bdc config replace --config-file custom-bdc/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a name="configure-scale"></a><a id="replicas"></a> 크기 조정 구성

스토리지 풀과 같은 각 리소스의 구성은 `bdc.json` 구성 파일에 정의됩니다. 예를 들어 `bdc.json`의 다음 부분에서는 `storage-0` 리소스 정의를 보여 줍니다.

```json
"storage-0": {
    "metadata": {
        "kind": "Pool",
        "name": "default"
    },
    "spec": {
        "type": "Storage",
        "replicas": 2,
        "settings": {
            "spark": {
                "spark-defaults-conf.spark.driver.memory": "2g",
                "spark-defaults-conf.spark.driver.cores": "1",
                "spark-defaults-conf.spark.executor.instances": "3",
                "spark-defaults-conf.spark.executor.memory": "1536m",
                "spark-defaults-conf.spark.executor.cores": "1",
                "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
                "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
                "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
                "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
                "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
            }
        }
    }
}
```

각 풀의 `replicas` 값을 수정하여 스토리지, 컴퓨팅 및/또는 데이터 풀의 인스턴스 수를 구성할 수 있습니다. 다음 예제에서는 인라인 JSON을 사용하여 스토리지, 컴퓨팅 및 데이터 풀의 이러한 값을 각각 `10`, `4` 및 `4`로 변경합니다.

```bash
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.storage-0.spec.replicas=10"
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.compute-0.spec.replicas=4"
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.data-0.spec.replicas=4"
```

> [!NOTE]
> 컴퓨팅 및 데이터 풀의 유효성을 검사하는 인스턴스의 최대 수는 각각 `8`입니다. 배포 시에는 이 제한이 적용되지 않지만, 프로덕션 배포에는 더 큰 크기를 구성하지 않는 것이 좋습니다.

## <a name="configure-storage"></a><a id="storage"></a> 스토리지 구성

각 풀에 사용되는 특성 및 스토리지 클래스를 변경할 수도 있습니다. 다음 예제에서는 사용자 지정 스토리지 클래스를 스토리지와 데이터 풀에 할당하고, 데이터를 저장하기 위한 영구 볼륨 클레임의 크기를 HDFS(스토리지 풀)의 경우 500Gb, 마스터 및 데이터 풀의 경우 100Gb로 업데이트합니다. 

> [!TIP]
> 스토리지 구성에 대한 자세한 내용은 [Kubernetes의 SQL Server 빅 데이터 클러스터를 사용한 데이터 지속성](concept-data-persistence.md)을 참조하세요.

먼저 아래와 같이 스토리지 설정을 조정하는 patch.json 파일을 만듭니다.

```json
{
        "patch": [
                {
                        "op": "add",
                        "path": "spec.resources.storage-0.spec.storage",
                        "value": {
                                "data": {
                                        "size": "500Gi",
                                        "className": "default",
                                        "accessMode": "ReadWriteOnce"
                                },
                                "logs": {
                                        "size": "30Gi",
                                        "className": "default",
                                        "accessMode": "ReadWriteOnce"
                                }
                        }
                },
        {
                        "op": "add",
                        "path": "spec.resources.master.spec.storage",
                        "value": {
                                "data": {
                                        "size": "100Gi",
                                        "className": "default",
                                        "accessMode": "ReadWriteOnce"
                                },
                                "logs": {
                                        "size": "30Gi",
                                        "className": "default",
                                        "accessMode": "ReadWriteOnce"
                                }
                        }
                },
                {
                        "op": "add",
                        "path": "spec.resources.data-0.spec.storage",
                        "value": {
                                "data": {
                                        "size": "100Gi",
                                        "className": "default",
                                        "accessMode": "ReadWriteOnce"
                                },
                                "logs": {
                                        "size": "30Gi",
                                        "className": "default",
                                        "accessMode": "ReadWriteOnce"
                                }
                        }
                }
        ]
}

```

그런 다음, `azdata bdc config patch` 명령을 사용하여 `bdc.json` 구성 파일을 업데이트할 수 있습니다.
```bash
azdata bdc config patch --config-file custom-bdc/bdc.json --patch ./patch.json
```

> [!NOTE]
> `kubeadm-dev-test` 기반 구성 파일에는 각 풀에 대한 스토리지 정의가 없지만, 필요한 경우 위 프로세스를 사용하여 추가할 수 있습니다.

## <a name="configure-storage-pool-without-spark"></a><a id="sparkstorage"></a> Spark 없이 스토리지 풀 구성

Spark 없이 실행되도록 스토리지 풀을 구성하고 별도의 spark 풀을 만들 수도 있습니다. 이 구성을 사용하면 스토리지와 관계없이 Spark 컴퓨팅 기능의 크기를 조정할 수 있습니다. Spark 풀을 구성하는 방법에 대한 자세한 내용은 이 문서의 [Spark 풀 만들기](#sparkpool) 섹션을 참조하세요.

> [!NOTE]
> Spark 없이 빅 데이터 클러스터를 배포하는 것은 지원되지 않습니다. 따라서 `includeSpark`를 `true`로 설정하거나, 하나 이상의 인스턴스를 사용하여 별도의 [Spark 풀](#sparkpool)을 만들어야 합니다. 또한 스토리지 풀(`includeSpark`는 `true`임)에서 둘 모두를 실행하는 Spark를 사용하고, 별도의 Spark 풀을 사용할 수 있습니다.

기본적으로 스토리지 풀 리소스의 `includeSpark` 설정이 true로 설정되므로 이를 변경하려면 `includeSpark` 필드를 스토리지 구성으로 편집해야 합니다. 다음 명령은 인라인 json을 사용하여 이 값을 편집하는 방법을 보여 줍니다.

```bash
azdata bdc config replace --config-file custom-bdc/bdc.json --json-values "$.spec.resources.storage-0.spec.settings.spark.includeSpark=false"
```

## <a name="create-a-spark-pool"></a><a id="sparkpool"></a> Spark 풀 만들기

단지 덧셈에 Spark 인스턴스가 스토리지 풀에서 실행되는 대신 Spark 풀을 만들 수도 있습니다. 다음 예제에서는 `bdc.json` 구성 파일을 패치하여 두 개의 인스턴스를 사용하여 Spark 풀을 만드는 방법을 보여 줍니다. 

먼저 다음과 같이 `spark-pool-patch.json` 파일을 만듭니다.

```json
{
    "patch": [
        {
            "op": "add",
            "path": "spec.resources.spark-0",
            "value": {
                "metadata": {
                    "kind": "Pool",
                    "name": "default"
                },
                "spec": {
                    "type": "Spark",
                    "replicas": 2
                }
            }
        },
        {
            "op": "add",
            "path": "spec.services.spark.resources/-",
            "value": "spark-0"
        },
        {
            "op": "add",
            "path": "spec.services.hdfs.resources/-",
            "value": "spark-0"
        }
    ]
}
```

그런 다음, `azdata bdc config patch` 명령을 실행합니다.

```bash
azdata bdc config patch -c custom-bdc/bdc.json -p spark-pool-patch.json
```

## <a name="configure-pod-placement-using-kubernetes-labels"></a><a id="podplacement"></a> Kubernetes 레이블을 사용하여 Pod 배치 구성

다양한 유형의 워크로드 요구 사항에 맞게 특정 리소스가 있는 Kubernetes 노드의 Pod 배치를 제어할 수 있습니다. Kubernetes 레이블을 사용하면 빅 데이터 클러스터 리소스를 배포하는 데 사용되는 Kubernetes 클러스터의 노드를 사용자 지정할 수 있지만 특정 리소스에 사용되는 노드를 제한할 수도 있습니다.
예를 들어 더 많은 스토리지가 있는 노드에 스토리지 풀 리소스 Pod가 배치되고, 더 높은 CPU 및 메모리 리소스가 있는 노드에 SQL Server 마스터 인스턴스가 배치되도록 할 수 있습니다. 이 경우에는 먼저 다양한 유형의 하드웨어를 사용하여 다른 유형의 Kubernetes 클러스터를 빌드한 다음, 적절하게 [노드 레이블을 할당](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)합니다. 빅 데이터 클러스터를 배포할 때 클러스터 수준에서 동일한 레이블을 지정하여 `control.json` 파일의 `clusterLabel` 특성을 사용하여 빅 데이터 클러스터에 사용되는 노드를 나타낼 수 있습니다. 그런 다음, 다른 레이블이 풀 수준 배치에 사용됩니다. 이러한 레이블은 `nodeLabel` 특성을 사용하여 빅 데이터 클러스터 배포 구성 파일에서 지정할 수 있습니다. Kubernetes는 Pod를 지정된 레이블과 일치하는 노드에 할당합니다. Kubernetes 클러스터의 노드에 추가해야 하는 특정 레이블 키는 `mssql-cluster`(빅 데이터 클러스터에 사용되는 노드를 나타내는 경우) 및 `mssql-resource`(다양한 리소스에 대해 Pod가 배치되는 노드를 나타내는 경우)입니다. 이러한 레이블의 값은 선택한 문자열일 수 있습니다.

> [!NOTE]
> 노드 수준 메트릭을 수집하는 Pod의 특성으로 인해 `metricsdc` Pod는 `mssql-cluster` 레이블이 있는 모든 노드에 배포되고 `mssql-resource`는 이러한 Pod에 적용되지 않습니다.

다음 예제에서는 전체 빅 데이터 클러스터에 대한 `bdc` 노드 레이블, SQL Server 마스터 인스턴스 Pod를 특정 노드에 배치하기 위한 `bdc-master` 레이블, 스토리지 풀 리소스에 대한 `bdc-storage-pool`, 컴퓨팅 풀 및 데이터 풀 Pod에 대한 `bdc-compute-pool`, 나머지 리소스에 대한 `bdc-shared`를 포함하도록 사용자 지정 구성 파일을 편집하는 방법을 보여 줍니다. 

먼저 Kubernetes 노드의 레이블을 다음과 같이 지정합니다.

```bash
kubectl label node <kubernetesNodeName1> mssql-cluster=bdc mssql-resource=bdc-shared --overwrite=true
kubectl label node <kubernetesNodeName2> mssql-cluster=bdc mssql-resource=bdc-master --overwrite=true
kubectl label node <kubernetesNodeName3> mssql-cluster=bdc mssql-resource=bdc-compute-pool --overwrite=true
kubectl label node <kubernetesNodeName4> mssql-cluster=bdc mssql-resource=bdc-compute-pool --overwrite=true
kubectl label node <kubernetesNodeName5> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
kubectl label node <kubernetesNodeName6> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
kubectl label node <kubernetesNodeName7> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
kubectl label node <kubernetesNodeName8> mssql-cluster=bdc mssql-resource=bdc-storage-pool --overwrite=true
```

그런 다음, 레이블 값을 포함하도록 클러스터 배포 구성 파일을 업데이트합니다. 이 예제에서는 `custom-bdc` 프로필에서 구성 파일을 사용자 지정한다고 가정합니다. 기본적으로 기본 제공 구성에는 `nodeLabel` 및 `clusterLabel` 키가 없으므로 사용자 지정 구성 파일을 수동으로 편집하거나 `azdata bdc config add` 명령을 사용하여 필요한 편집 작업을 수행해야 합니다.

```bash
azdata bdc config add -c custom-bdc/control.json -j "$.spec.clusterLabel=bdc"
azdata bdc config add -c custom-bdc/control.json -j "$.spec.nodeLabel=bdc-shared"

azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.master.spec.nodeLabel=bdc-master"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.compute-0.spec.nodeLabel=bdc-compute-pool"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.data-0.spec.nodeLabel=bdc-compute-pool"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.storage-0.spec.nodeLabel=bdc-storage-pool"

# below can be omitted in which case we will take the node label default from the control.json
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.nmnode-0.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.sparkhead.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.zookeeper.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.gateway.spec.nodeLabel=bdc-shared"
azdata bdc config add -c custom-bdc/bdc.json -j "$.spec.resources.appproxy.spec.nodeLabel=bdc-shared"
```
>[!NOTE]
> 모범 사례는 위의 BDC 역할에 Kubernetes 마스터를 제공하지 않도록 방지합니다. Kubernetes 마스터 노드에 해당 역할을 할당할 계획인 경우 [``master:NoSchedule`` taint를 제거](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/)해야 합니다. 이 경우 마스터 노드를 오버로드되어 대규모 클러스터에서 Kubernetes 관리 임무를 수행할 수 없게 된다는 것에 유의하세요. 모든 배포의 마스터에 일부 Pod가 예약되어 있는 것이 일반적입니다. 이미 ``master:NoSchedule`` taint을 허용하며, 클러스터를 관리하는 데 주로 사용됩니다. 

## <a name="other-customizations-using-json-patch-files"></a><a id="jsonpatch"></a> JSON 패치 파일을 사용한 기타 사용자 지정

JSON 패치 파일은 한 번에 여러 설정을 구성합니다. JSON 패치에 대한 자세한 내용은 [Python의 JSON 패치](https://github.com/stefankoegl/python-json-patch) 및 [JSONPath Online Evaluator](https://jsonpath.com/)를 참조하세요.

다음 `patch.json` 파일에서 수행하는 변경 작업은 다음과 같습니다.

- `control.json`에서 단일 엔드포인트의 포트를 업데이트합니다.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.endpoints[?(@.name=='Controller')].port",
      "value": 30000
    }
  ]
}
```

- `control.json`에서 모든 엔드포인트(`port` 및 `serviceType`)를 업데이트합니다.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.endpoints",
      "value": [
        {
          "serviceType": "LoadBalancer",
          "port": 30001,
          "name": "Controller"
        },
        {
          "serviceType": "LoadBalancer",
          "port": 30778,
          "name": "ServiceProxy"
        }
      ]
    }
  ]
}
```

- `control.json`에서 컨트롤러 스토리지 설정을 업데이트합니다. 이 설정은 풀 수준에서 재정의하지 않을 경우 모든 클러스터 구성 요소에 적용됩니다.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.storage",
      "value": {
        "data": {
          "className": "managed-premium",
          "accessMode": "ReadWriteOnce",
          "size": "100Gi"
        },
        "logs": {
          "className": "managed-premium",
          "accessMode": "ReadWriteOnce",
          "size": "32Gi"
        }
      }
    }
  ]
}
```

- `control.json`에서 스토리지 클래스 이름을 업데이트합니다.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.storage.data.className",
      "value": "managed-premium"
    }
  ]
}
```

- `bdc.json`에서 스토리지 풀의 풀 스토리지 설정을 업데이트합니다.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

- `bdc.json`에서 스토리지 풀의 Spark 설정을 업데이트합니다.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.services.spark.settings",
      "value": {
            "spark-defaults-conf.spark.driver.memory": "2g",
            "spark-defaults-conf.spark.driver.cores": "1",
            "spark-defaults-conf.spark.executor.instances": "3",
            "spark-defaults-conf.spark.executor.memory": "1536m",
            "spark-defaults-conf.spark.executor.cores": "1",
            "yarn-site.yarn.nodemanager.resource.memory-mb": "18432",
            "yarn-site.yarn.nodemanager.resource.cpu-vcores": "6",
            "yarn-site.yarn.scheduler.maximum-allocation-mb": "18432",
            "yarn-site.yarn.scheduler.maximum-allocation-vcores": "6",
            "yarn-site.yarn.scheduler.capacity.maximum-am-resource-percent": "0.3"
      }
    }
  ]
}
```

> [!TIP]
> 배포 구성 파일을 변경하기 위한 구조 및 옵션에 대한 자세한 내용은 [빅 데이터 클러스터의 배포 구성 파일 참조](reference-deployment-config.md)를 참조하세요.

`azdata bdc config` 명령을 사용하여 JSON 패치 파일의 변경 내용을 적용합니다. 다음 예제에서는 `patch.json` 파일을 대상 배포 구성 파일 `custom-bdc/bdc.json`에 적용합니다.

```bash
azdata bdc config patch --config-file custom-bdc/bdc.json --patch-file ./patch.json
```

## <a name="disable-elasticsearch-to-run-in-privileged-mode"></a>특권 모드에서 실행되는 ElasticSearch 사용 안 함

ElasticSearch 컨테이너는 기본적으로 빅 데이터 클러스터에서 특권 모드로 실행됩니다. 이렇게 설정하면 컨테이너 초기화 시 ElasticSearch에서 더 많은 양의 로그를 처리할 때 필요한 호스트의 설정을 업데이트할 수 있을 만큼 충분한 권한이 컨테이너에 있습니다. 자세한 내용은 [이 문서](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)의 해당 항목에서 확인할 수 있습니다. 

ElasticSearch를 실행하는 컨테이너를 특권 모드에서 실행되지 않도록 설정하려면 `control.json`에서 `settings` 섹션을 업데이트하고 `vm.max_map_count`의 값을 `-1`로 지정해야 합니다. 이 섹션의 예제는 다음과 같습니다.

```json
{
    "apiVersion": "v1",
    "metadata": {...},
    "spec": {
        "docker": {...},
        "storage": {...},
        "endpoints": [...],
        "settings": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
            }
        }
    }
}
```

`control.json`을 수동으로 편집하고 위의 섹션을 `spec`에 추가하거나, 아래와 같이 `elasticsearch-patch.json` 패치 파일을 만들고 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]를 사용하여 `control.json` 파일을 패치할 수 있습니다.

```json
{
  "patch": [
    {
      "op": "add",
      "path": "spec.settings",
      "value": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
        }
      }
    }
  ]
}
```

다음 명령을 실행하여 구성 파일을 패치합니다.

```bash
azdata bdc config patch --config-file custom-bdc/control.json --patch-file elasticsearch-patch.json
```

> [!IMPORTANT]
> [이 문서](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)의 지침에 따라 Kubernetes 클러스터의 각 호스트에서 `max_map_count` 설정을 수동으로 업데이트하는 것이 좋습니다.

## <a name="turn-pods-and-nodes-metrics-collection-onoff"></a>Pod 및 노드 메트릭 수집 설정/해제

SQL Server 2019 CU5에서는 Pod 및 노드 메트릭의 수집을 제어하는 두 가지 기능 스위치를 사용하도록 설정했습니다. Kubernetes 인프라를 모니터링하기 위해 다른 솔루션을 사용하는 경우 *control.json* 배포 구성 파일에서 *allowNodeMetricsCollection* 및 *allowPodMetricsCollection* 을 *false* 로 설정하면 기본 제공되는 Pod 및 호스트 노드 메트릭 수집을 해제할 수 있습니다. OpenShift 환경의 경우 Pod 및 노드 메트릭을 수집하려면 권한 기능이 필요하므로 기본 제공 배포 프로필에서 이 설정은 기본적으로 *false* 로 설정됩니다.
*azdata* CLI를 사용하여 사용자 지정 구성 파일에서 이 설정의 값을 업데이트하려면 다음 명령을 실행합니다.

```bash
 azdata bdc config replace -c custom-bdc/control.json -j "$.security.allowNodeMetricsCollection=false"
 azdata bdc config replace -c custom-bdc/control.json -j "$.security.allowPodMetricsCollection=false"
 ```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 배포에서 구성 파일을 사용하는 방법에 대한 자세한 내용은 [Kubernetes에 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포하는 방법](deployment-guidance.md#configfile)을 참조하세요.