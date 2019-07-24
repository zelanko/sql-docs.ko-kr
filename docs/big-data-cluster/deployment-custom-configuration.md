---
title: 배포 구성
titleSuffix: SQL Server big data clusters
description: 구성 파일을 사용 하 여 빅 데이터 클러스터 배포를 사용자 지정 하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7559ecf9c7b17ca21c088ed531a347f88e89ee2
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419439"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>빅 데이터 클러스터에 대 한 배포 설정 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

클러스터 배포 구성 파일을 사용자 지정 하려면 VSCode와 같은 JSON 형식 편집기를 사용할 수 있습니다. 자동화를 위해 이러한 편집을 스크립팅 하려면 **azdata bdc config** 명령을 사용 합니다. 이 문서에서는 배포 구성 파일을 수정 하 여 빅 데이터 클러스터 배포를 구성 하는 방법을 설명 합니다. 다양 한 시나리오에 대 한 구성을 변경 하는 방법에 대 한 예제를 제공 합니다. 배포에서 구성 파일을 사용 하는 방법에 대 한 자세한 내용은 [배포 지침](deployment-guidance.md#configfile)을 참조 하세요.

## <a name="prerequisites"></a>사전 요구 사항

- [Azdata를 설치](deploy-install-azdata.md)합니다.

- 이 섹션의 각 예제에서는 표준 구성 중 하나의 복사본을 만들었다고 가정 합니다. 자세한 내용은 [사용자 지정 구성 만들기](deployment-guidance.md#customconfig)를 참조 하세요. 예를 들어 다음 명령은 기본 **aks** 구성에 따라 `custom` 두 개의 JSON 배포 구성 파일, cluster.exe **및** **컨트롤**을 포함 하는 라는 디렉터리를 만듭니다.

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a>클러스터 이름 변경

클러스터 이름은 빅 데이터 클러스터의 이름과 배포 시 생성 되는 Kubernetes 네임 스페이스입니다. 이 파일은 클러스터의 다음 부분인 **json** 배포 구성 파일에 지정 되어 있습니다.

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

다음 명령은 키-값 쌍을 **--json 값** 매개 변수로 전송 하 여 빅 데이터 클러스터 이름을 **테스트-클러스터**로 변경 합니다.

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> 빅 데이터 클러스터의 이름은 소문자 여야 하 고 공백이 없어야 합니다. 클러스터에 대 한 모든 Kubernetes 아티팩트 (컨테이너, pod, 상태 저장 집합, 서비스)는 지정 된 클러스터 이름과 이름이 같은 네임 스페이스에 만들어집니다.

## <a id="ports"></a>끝점 포트 업데이트

끝점은 **control. json** 의 컨트롤러에 대해 정의 되 고, 게이트웨이 및 SQL Server 마스터 인스턴스는 **cluster.exe의 해당**섹션에 정의 되어 있습니다. 다음의 **컨트롤 json** 구성 파일 부분은 컨트롤러에 대 한 끝점 정의를 보여 줍니다.

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

다음 예제에서는 인라인 JSON을 사용 하 여 **컨트롤러** 끝점의 포트를 변경 합니다.

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a>풀 복제본 구성

저장소 풀과 같은 각 풀의 특징은 **cluster. json** 구성 파일에 정의 되어 있습니다. 예를 들어, **클러스터** 의 다음 부분에서는 저장소 풀 정의를 보여 줍니다.

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

각 풀의 **복제본** 값을 수정 하 여 풀의 인스턴스 수를 구성할 수 있습니다. 다음 예제에서는 인라인 JSON을 사용 하 여 저장소 및 데이터 풀의 이러한 값을 `10` 각각 `4` 및로 변경 합니다.

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a>저장소 구성

각 풀에 사용 되는 특성 및 저장소 클래스를 변경할 수도 있습니다. 다음 예제에서는 저장소 풀에 사용자 지정 저장소 클래스를 할당 하 고 100Gb에 데이터를 저장 하기 위한 영구 볼륨 클레임의 크기를 업데이트 합니다. 먼저 *형식* 및 *복제본* 외에도 새 *저장소* 섹션을 포함 하는 아래와 같은 패치나 json 파일을 만듭니다.

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

그런 다음 **azdata bdc 구성 패치** 명령을 사용 하 여 **클러스터. json** 구성 파일을 업데이트할 수 있습니다.
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

> [!NOTE]
> **Kubeadm** 을 기반으로 하는 구성 파일에는 각 풀에 대 한 저장소 정의가 없지만 필요한 경우 위의 프로세스를 사용 하 여 추가할 수 있습니다.

저장소 구성에 대 한 자세한 내용은 [Kubernetes의 SQL Server 빅 데이터 클러스터를 사용 하는 데이터 지 속성](concept-data-persistence.md)을 참조 하세요.

## <a id="sparkstorage"></a>Spark를 사용 하지 않고 저장소 풀 구성

Spark 없이 실행 되도록 저장소 풀을 구성 하 고 별도의 spark 풀을 만들 수도 있습니다. 이렇게 하면 저장소와 무관 하 게 spark 계산 기능을 확장할 수 있습니다. Spark 풀을 구성 하는 방법에 대 한 자세한 내용은이 문서의 끝에 있는 [JSON 패치 파일 예제](#jsonpatch) 를 참조 하세요.



기본적으로 저장소 풀에 대 한 **includespark** 설정은 true로 설정 되므로 변경 하기 위해 **includespark** 필드를 저장소 구성에 추가 해야 합니다. 다음 JSON 패치 파일은이를 추가 하는 방법을 보여 줍니다.

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

## <a id="podplacement"></a>Kubernetes 레이블을 사용 하 여 pod 배치 구성

다양 한 종류의 작업 요구 사항에 맞게 특정 리소스가 있는 Kubernetes 노드의 pod 배치를 제어할 수 있습니다. 예를 들어 저장소 풀 pod가 더 많은 저장소가 있는 노드에 배치 되도록 하거나, SQL Server 마스터 인스턴스가 더 높은 CPU 및 메모리 리소스가 있는 노드에 배치 되도록 할 수 있습니다. 이 경우에는 먼저 다른 유형의 하드웨어를 사용 하 여 다른 유형의 Kubernetes 클러스터를 빌드한 다음 그에 따라 [노드 레이블을 할당](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) 합니다. 빅 데이터 클러스터를 배포할 때 클러스터 배포 구성 파일의 풀 수준에서 동일한 레이블을 지정할 수 있습니다. 그러면 Kubernetes는 지정 된 레이블과 일치 하는 노드의 pod를 한 합니다.

다음 예에서는 SQL Server 마스터 인스턴스에 대해 노드 레이블 설정을 포함 하도록 사용자 지정 구성 파일을 편집 하는 방법을 보여 줍니다. 기본 제공 구성에는 *nodeLabel* 키가 없으므로 사용자 지정 구성 파일을 수동으로 편집 하거나 패치 파일을 만들고 사용자 지정 구성 파일에 적용 해야 합니다.

다음 내용을 사용 하 여 현재 디렉터리에 **patch. json** 이라는 파일을 만듭니다.

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
         "nodeLabel": "<yourNodeLabel>"
       }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a id="jsonpatch"></a>JSON 패치 파일

JSON 패치 파일은 한 번에 여러 설정을 구성 합니다. JSON 패치에 대 한 자세한 내용은 [Python의 Json 패치와](https://github.com/stefankoegl/python-json-patch) [JSONPath Online 계산기](https://jsonpath.com/)를 참조 하세요.

다음 **패치나 json** 파일은 다음과 같이 변경 됩니다.

- **컨트롤 json**에서 단일 끝점의 포트를 업데이트 합니다.
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

- **컨트롤. json**의 모든 끝점 (**포트** 및 **serviceType**)을 업데이트 합니다.
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

- **컨트롤. json**의 컨트롤러 저장소 설정을 업데이트 합니다. 이러한 설정은 풀 수준에서 재정의 되지 않는 한 모든 클러스터 구성 요소에 적용할 수 있습니다.
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

- 는 **json**의 저장소 클래스 이름을 업데이트 합니다.
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

- **클러스터 json**의 저장소 풀에 대 한 풀 저장소 설정을 업데이트 합니다.
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

- **클러스터 json**의 저장소 풀에 대 한 Spark 설정을 업데이트 합니다.
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

- 두 개의 인스턴스를 사용 하 여 **클러스터 json**에 spark 풀을 만듭니다.
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
> 배포 구성 파일을 변경 하기 위한 구조 및 옵션에 대 한 자세한 내용은 [빅 데이터 클러스터에 대 한 배포 구성 파일 참조](reference-deployment-config.md)를 참조 하세요.

**Azdata bdc config** 명령을 사용 하 여 JSON 패치 파일의 변경 내용을 적용 합니다. 다음 예제에서는 **사용자 지정/** a p i. **json 파일을** 대상 배포 구성 파일에 적용 합니다.

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 배포에서 구성 파일을 사용 하는 방법에 대 한 자세한 내용은 [Kubernetes에서 빅 데이터 클러스터 SQL Server 배포 하는 방법](deployment-guidance.md#configfile)을 참조 하세요.
