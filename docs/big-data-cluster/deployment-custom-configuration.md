---
title: 배포 구성
titleSuffix: SQL Server big data clusters
description: 구성 파일을 사용하여 빅 데이터 클러스터 배포를 사용자 지정하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 02e922ca909cd863d496f9c49a60dd986df8bedb
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652399"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>빅 데이터 클러스터의 배포 설정 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

클러스터 배포 구성 파일을 사용자 지정하려면 VSCode와 같은 JSON 형식 편집기를 사용할 수 있습니다. 자동화를 위해 이러한 편집 작업을 스크립팅하려면 **azdata bdc config** 명령을 사용합니다. 이 문서에서는 배포 구성 파일을 수정하여 빅 데이터 클러스터 배포를 구성하는 방법을 설명합니다. 각기 다른 시나리오에 맞게 구성을 변경하는 방법의 예제를 제공합니다. 배포에서 구성 파일을 사용하는 방법에 대한 자세한 내용은 [배포 지침](deployment-guidance.md#configfile)을 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

- [azdata 설치](deploy-install-azdata.md).

- 이 섹션의 각 예제에서는 표준 구성 중 하나의 복사본을 만들었다고 가정합니다. 자세한 내용은 [사용자 지정 구성 만들기](deployment-guidance.md#customconfig)를 참조하세요. 예를 들어 다음 명령은 기본 **aks-dev-test** 구성에 따라 두 개의 JSON 배포 구성 파일(**cluster.json** 및 **control.json**)이 포함되는 `custom` 디렉터리를 만듭니다.

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> 클러스터 이름 변경

클러스터 이름은 빅 데이터 클러스터의 이름과 배포 시 생성되는 Kubernetes 네임스페이스로 구성됩니다. **cluster.json** 배포 구성 파일의 다음 부분에 지정되어 있습니다.

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

다음 명령은 키-값 쌍을 **--json-values** 매개 변수로 보내 빅 데이터 클러스터 이름을 **test-cluster**로 변경합니다.

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> 빅 데이터 클러스터 이름은 소문자 영숫자여야 하고 공백을 포함하지 않아야 합니다. 클러스터의 모든 Kubernetes 아티팩트(컨테이너, Pod, 상태 저장 세트, 서비스)는 지정된 클러스터 이름과 동일한 이름의 네임스페이스에 생성됩니다.

## <a id="ports"></a> 엔드포인트 포트 업데이트

엔드포인트는 컨트롤러의 경우 **control.json**에 정의되어 있고, 게이트웨이 및 SQL Server 마스터 인스턴스의 경우 **cluster.json**의 해당 섹션에 정의되어 있습니다. **control.json** 구성 파일의 다음 부분에는 컨트롤러의 엔드포인트 정의가 표시됩니다.

```json
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
```

다음 예제에서는 인라인 JSON을 사용하여 **컨트롤러** 엔드포인트의 포트를 변경합니다.

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> 풀 복제본 구성

스토리지 풀과 같은 각 풀의 특성은 **cluster.json** 구성 파일에 정의되어 있습니다. 예를 들어 **cluster.json**의 다음 부분에는 스토리지 풀 정의가 표시됩니다.

```json
"pools": [
   {
       "metadata": {
           "kind": "Pool",
           "name": "default"
       },
       "spec": {
           "type": "Storage",
           "replicas": 2
       }
   }
]
```

각 풀의 **replicas** 값을 수정하여 풀의 인스턴스 수를 구성할 수 있습니다. 다음 예제에서는 인라인 JSON을 사용하여 스토리지 풀과 데이터 풀의 해당 값을 각각 `10`과 `4`로 변경합니다.

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a> 스토리지 구성

각 풀에 사용되는 특성 및 스토리지 클래스를 변경할 수도 있습니다. 다음 예제에서는 스토리지 풀에 사용자 지정 스토리지 클래스를 할당하고 데이터를 저장하기 위한 영구적 볼륨 클레임 크기를 100Gb로 업데이트합니다. 먼저 *type* 및 *replicas* 외에 새 *storage* 섹션을 포함하는 patch.json 파일을 아래와 같이 만듭니다.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
        "storage":{
        "data":{
                "size": "100Gi",
                "className": "myStorageClass",
                "accessMode":"ReadWriteOnce"
                },
        "logs":{
                "size":"32Gi",
                "className":"myStorageClass",
                "accessMode":"ReadWriteOnce"
                }
                },
        "type":"Storage",
        "replicas":2
      }
    }
  ]
}
```

그런 다음, **azdata bdc config patch** 명령을 사용하여 **cluster.json** 구성 파일을 업데이트할 수 있습니다.
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

> [!NOTE]
> **kubeadm-dev-test**를 기반으로 하는 구성 파일에는 각 풀에 대한 스토리지 정의가 없지만, 필요한 경우 위 프로세스를 사용하여 추가할 수 있습니다.

스토리지 구성에 대한 자세한 내용은 [Kubernetes의 SQL Server 빅 데이터 클러스터를 사용한 데이터 지속성](concept-data-persistence.md)을 참조하세요.

## <a id="sparkstorage"></a> Spark 없이 스토리지 풀 구성

Spark 없이 실행되도록 스토리지 풀을 구성하고 별도의 spark 풀을 만들 수도 있습니다. 이렇게 하면 스토리지와 별도로 spark 컴퓨팅 기능을 확장할 수 있습니다. spark 풀을 구성하는 방법에 대한 자세한 내용은 이 문서의 끝에 있는 [JSON 패치 파일 예제](#jsonpatch)를 참조하세요.



기본적으로 스토리지 풀의 **includeSpark** 설정은 true로 설정되어 있으므로 **includespark** 필드를 스토리지 구성에 추가해야 내용을 변경할 수 있습니다. 다음 JSON 패치 파일은 이 필드를 추가하는 방법을 보여 줍니다.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
       "type":"Storage",
       "replicas":2,
       "includeSpark":false
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

## <a id="podplacement"></a> Kubernetes 레이블을 사용하여 Pod 배치 구성

다양한 유형의 워크로드 요구 사항에 맞게 특정 리소스가 있는 Kubernetes 노드의 Pod 배치를 제어할 수 있습니다. 예를 들어 스토리지가 더 많은 노드에 스토리지 풀 Pod가 배치되도록 하거나, CPU 및 메모리 리소스가 더 많은 노드에 SQL Server 마스터 인스턴스가 배치되도록 할 수 있습니다. 이 경우에는 먼저 다양한 유형의 하드웨어를 사용하여 다른 유형의 Kubernetes 클러스터를 빌드한 다음, 적절하게 [노드 레이블을 할당](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)합니다. 빅 데이터 클러스터를 배포할 때 클러스터 배포 구성 파일의 풀 수준에서 동일한 레이블을 지정할 수 있습니다. 그러면 Kubernetes가 지정된 레이블과 일치하는 노드의 Pod에 선호도를 지정합니다. Kubernetes 클러스터의 노드에 추가 해야 하는 특정 레이블 키는 **mssql 클러스터 전체**에 해당 합니다. 이 레이블 자체의 값은 선택한 문자열일 수 있습니다.

다음 예제에서는 SQL Server 마스터 인스턴스, 계산 풀, 데이터 풀 & 저장소 풀에 대 한 노드 레이블 설정을 포함 하도록 사용자 지정 구성 파일을 편집 하는 방법을 보여 줍니다. 기본 제공 구성에는 *nodeLabel* 키가 없으므로 사용자 지정 구성 파일을 수동으로 편집하거나 패치 파일을 만들어 사용자 지정 구성 파일에 적용해야 합니다. SQL Server 마스터 인스턴스 pod는 값이 **bdc-마스터**인 **mssql-클러스터 차원의** 레이블을 포함 하는 노드에 배포 됩니다. 계산 풀 및 데이터 풀 pod는 **mssql-클러스터 차원의** 값이 **bdc-sql**인 노드에 배포 됩니다. 저장소 풀 pod는 **mssql-클러스터 전체** 에 값이 포함 된 노드에 배포 됩니다.

다음 내용을 사용하여 현재 디렉터리에 **patch.json**이라는 파일을 만듭니다.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Master')].spec",
      "value": {
    "type": "Master",
        "replicas": 1,
        "hadrEnabled": false,
        "endpoints": [
            {
             "name": "Master",
             "serviceType": "NodePort",
             "port": 31433
            }
          ],
        "nodeLabel": "bdc-master"
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Compute')].spec",
      "value": {
    "type": "Compute",
        "replicas": 1,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Data')].spec",
      "value": {
    "type": "Data",
        "replicas": 2,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
    "type": "Storage",
        "replicas": 3,
        "nodeLabel": "bdc-storage"
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a id="jsonpatch"></a> JSON 패치 파일

JSON 패치 파일은 한 번에 여러 설정을 구성합니다. JSON 패치에 대한 자세한 내용은 [Python의 JSON 패치](https://github.com/stefankoegl/python-json-patch) 및 [JSONPath Online Evaluator](https://jsonpath.com/)를 참조하세요.

아래 **patch.json** 파일은 다음과 같은 변경 작업을 수행합니다.

- **control.json**에서 단일 엔드포인트의 포트를 업데이트합니다.
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

- **control.json**에서 모든 엔드포인트(**port** 및 **serviceType**)를 업데이트합니다.
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

- **control.json**에서 컨트롤러 스토리지 설정을 업데이트합니다. 이 설정은 풀 수준에서 재정의하지 않을 경우 모든 클러스터 구성 요소에 적용됩니다.
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

- **control.json**에서 스토리지 클래스 이름을 업데이트합니다.
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

- **cluster.json**에서 스토리지 풀의 풀 스토리지 설정을 업데이트합니다.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
          "value": {
        "type":"Storage",
        "replicas":2,
        "storage":{
        "data":{
            "size": "100Gi",
            "className": "myStorageClass",
            "accessMode":"ReadWriteOnce"
            },
        "logs":{
            "size":"32Gi",
            "className":"myStorageClass",
            "accessMode":"ReadWriteOnce"
            }
            }
         }
        }
      ]
    }
    ```

- **cluster.json**에서 스토리지 풀의 Spark 설정을 업데이트합니다.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "$.spec.pools[?(@.spec.type == 'Storage')].hadoop.spark",
          "value": {
        "driverMemory": "2g",
        "driverCores": 1,
        "executorInstances": 3,
        "executorCores": 1,
        "executorMemory": "1536m"
          }
        }   
      ]
    }
    ```

- **cluster.json**에서 두 개의 인스턴스로 spark 풀을 만듭니다.
    ```json
    {
      "patch": [
        {
          "op": "add",
          "path": "spec.pools/-",
          "value":
          {
        "metadata": {
          "kind": "Pool",
          "name": "default"
        },
        "spec": {
          "type": "Spark",
          "replicas": 2
        },
        "hadoop": {
          "yarn": {
            "nodeManager": {
              "memory": 12288,
              "vcores": 6
            },
            "schedulerMax": {
              "memory": 12288,
              "vcores": 6
            },
            "capacityScheduler": {
              "maxAmPercent": 0.3
            }
          },
          "spark": {
            "driverMemory": "2g",
            "driverCores": 1,
            "executorInstances": 2,
            "executorMemory": "2g",
            "executorCores": 1
          }
        }
          }
        } 
      ]
    }
    ```



> [!TIP]
> 배포 구성 파일을 변경하기 위한 구조 및 옵션에 대한 자세한 내용은 [빅 데이터 클러스터의 배포 구성 파일 참조](reference-deployment-config.md)를 참조하세요.

**azdata bdc config** 명령을 사용하여 JSON 패치 파일의 변경 내용을 적용합니다. 다음 예제에서는 **patch.json** 파일을 대상 배포 구성 파일 **custom/cluster.json**에 적용합니다.

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 배포에서 구성 파일을 사용 하는 방법에 대 한 자세한 내용은 [Kubernetes에서 배포 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 하는 방법](deployment-guidance.md#configfile)을 참조 하세요.
