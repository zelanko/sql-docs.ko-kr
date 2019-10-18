---
title: 배포 구성
titleSuffix: SQL Server big data clusters
description: 구성 파일을 사용하여 빅 데이터 클러스터 배포를 사용자 지정하는 방법을 알아봅니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 31c745a585adf26b521054cbcd0234fd4087a114
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2019
ms.locfileid: "72542168"
---
# <a name="configure-deployment-settings-for-cluster-resources-and-services"></a>클러스터 리소스 및 서비스에 대 한 배포 설정 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Azdata 관리 도구에 기본 제공 되는 미리 정의 된 구성 프로필 집합에서 시작 하 여 BDC 워크 로드 요구 사항에 더 적합 하도록 기본 설정을 쉽게 수정할 수 있습니다. 릴리스 후보 릴리스부터 구성 파일의 구조가 업데이트 되어 리소스의 각 서비스 마다 업데이트 설정을 세부적으로 수 있습니다. 

리소스 수준 구성을 설정 하거나 리소스의 모든 서비스에 대 한 구성을 업데이트할 수도 있습니다. 다음은 bdc의 구조에 대 한 요약입니다 **.**

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

풀의 인스턴스와 같은 리소스 수준 구성을 업데이트 하는 경우 리소스 사양을 업데이트 합니다. 예를 들어, compute 풀의 인스턴스 수를 업데이트 하려면이 섹션을 **bdc. json** 구성 파일에서 수정 합니다.
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

마찬가지로 특정 리소스 내에서 단일 서비스의 설정을 변경 하는 경우에도 마찬가지입니다. 예를 들어 저장소 풀의 Spark 구성 요소에 대 한 Spark 메모리 설정을 변경 하려는 경우에는 **저장소-0** 리소스를 **bdc. json** 구성 파일의 **spark** 서비스에 대 한 **설정** 섹션으로 업데이트 합니다. .
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
                    "driverMemory": "2g",
                    "driverCores": "1",
                    "executorInstances": "3",
                    "executorMemory": "1536m",
                    "executorCores": "1"
                }
            }
        }
    }
    ...
}
```

여러 리소스와 연결 된 서비스에 동일한 구성을 적용 하려는 경우에는 **서비스** 섹션에서 해당 **설정을** 업데이트 합니다. 예를 들어, 저장소 풀과 Spark 풀 모두에서 Spark에 대해 동일한 설정을 설정 하려는 경우 **에는 해당** **설정** 섹션을 업데이트 **합니다.**

```json
"services": {
    ...
    "spark": {
        "resources": [
            "sparkhead",
            "storage-0"
        ],
        "settings": {
            "driverMemory": "2g",
            "driverCores": "1",
            "executorInstances": "3",
            "executorMemory": "1536m",
            "executorCores": "1"
        }
    }
    ...
}
```


클러스터 배포 구성 파일을 사용자 지정하려면 VSCode와 같은 JSON 형식 편집기를 사용할 수 있습니다. 자동화를 위해 이러한 편집 작업을 스크립팅하려면 **azdata bdc config** 명령을 사용합니다. 이 문서에서는 배포 구성 파일을 수정하여 빅 데이터 클러스터 배포를 구성하는 방법을 설명합니다. 각기 다른 시나리오에 맞게 구성을 변경하는 방법의 예제를 제공합니다. 배포에서 구성 파일을 사용하는 방법에 대한 자세한 내용은 [배포 지침](deployment-guidance.md#configfile)을 참조하세요.

## <a name="prerequisites"></a>Prerequisites

- [azdata 설치](deploy-install-azdata.md).

- 이 섹션의 각 예제에서는 표준 구성 중 하나의 복사본을 만들었다고 가정합니다. 자세한 내용은 [사용자 지정 구성 만들기](deployment-guidance.md#customconfig)를 참조하세요. 예를 들어 다음 명령은 기본 **aks** 구성에 **기반 하 여** 두 개의 json 배포 구성 파일인 및 **control**을 포함 하는 `custom` 라는 디렉터리를 만듭니다.

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> 클러스터 이름 변경

클러스터 이름은 빅 데이터 클러스터의 이름과 배포 시 생성되는 Kubernetes 네임스페이스로 구성됩니다. 이 파일은 다음과 같은 **bdc. json** 배포 구성 파일의 부분에 지정 되어 있습니다.

```json
"metadata": {
    "kind": "BigDataCluster",
    "name": "mssql-cluster"
},
```

다음 명령은 키-값 쌍을 **--json-values** 매개 변수로 보내 빅 데이터 클러스터 이름을 **test-cluster**로 변경합니다.

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> 빅 데이터 클러스터 이름은 소문자 영숫자여야 하고 공백을 포함하지 않아야 합니다. 클러스터의 모든 Kubernetes 아티팩트(컨테이너, Pod, 상태 저장 세트, 서비스)는 지정된 클러스터 이름과 동일한 이름의 네임스페이스에 생성됩니다.

## <a id="ports"></a> 엔드포인트 포트 업데이트

끝점은 **컨트롤. json** 의 컨트롤러에 대해 정의 되 고, 게이트웨이 및 SQL Server 마스터 인스턴스는 해당 섹션의 **bdc. json**에 정의 되어 있습니다. **control.json** 구성 파일의 다음 부분에는 컨트롤러의 엔드포인트 정의가 표시됩니다.

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

다음 예제에서는 인라인 JSON을 사용하여 **컨트롤러** 엔드포인트의 포트를 변경합니다.

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> 풀 복제본 구성

저장소 풀과 같은 각 리소스의 구성은 **bdc. json** 구성 파일에 정의 되어 있습니다. 예를 들어, 다음의 **bdc** 는 **저장소 0** 리소스 정의를 보여 줍니다.

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
                "driverMemory": "2g",
                "driverCores": "1",
                "executorInstances": "3",
                "executorMemory": "1536m",
                "executorCores": "1"
            }
        }
    }
}
```

각 풀의 **replicas** 값을 수정하여 풀의 인스턴스 수를 구성할 수 있습니다. 다음 예제에서는 인라인 JSON을 사용하여 스토리지 풀과 데이터 풀의 해당 값을 각각 `10`과 `4`로 변경합니다.

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.storage-0.spec.replicas=10"
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.data-0.spec.replicas=4"
```

## <a id="storage"></a> 스토리지 구성

각 풀에 사용되는 특성 및 스토리지 클래스를 변경할 수도 있습니다. 다음 예제에서는 저장소 및 데이터 풀에 사용자 지정 저장소 클래스를 할당 하 고 데이터 풀의 HDFS (저장소 풀) 및 100 Gb에 대 한 데이터를 500으로 저장 하기 위한 영구 볼륨 클레임의 크기를 업데이트 합니다. 먼저 *type* 및 *replicas* 외에 새 *storage* 섹션을 포함하는 patch.json 파일을 아래와 같이 만듭니다.

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
            "size": "500Gi",
            "className": "myHDFSStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myHDFSStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.data-0.spec",
      "value": {
        "type": "Data",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myDataStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myDataStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

그런 다음 **azdata bdc 구성 패치** 명령을 사용 하 여 **bdc. json** 구성 파일을 업데이트할 수 있습니다.
```bash
azdata bdc config patch --config-file custom/bdc.json --patch ./patch.json
```

> [!NOTE]
> **kubeadm-dev-test**를 기반으로 하는 구성 파일에는 각 풀에 대한 스토리지 정의가 없지만, 필요한 경우 위 프로세스를 사용하여 추가할 수 있습니다.

스토리지 구성에 대한 자세한 내용은 [Kubernetes의 SQL Server 빅 데이터 클러스터를 사용한 데이터 지속성](concept-data-persistence.md)을 참조하세요.

## <a id="sparkstorage"></a> Spark 없이 스토리지 풀 구성

Spark 없이 실행되도록 스토리지 풀을 구성하고 별도의 spark 풀을 만들 수도 있습니다. 이렇게 하면 스토리지와 별도로 spark 컴퓨팅 기능을 확장할 수 있습니다. spark 풀을 구성하는 방법에 대한 자세한 내용은 이 문서의 끝에 있는 [JSON 패치 파일 예제](#jsonpatch)를 참조하세요.


기본적으로 저장소 풀 리소스에 대 한 **includespark** 설정은 true로 설정 되므로 변경 하기 위해 **includespark** 필드를 저장소 구성으로 편집 해야 합니다. 다음 명령은 인라인 json을 사용 하 여이 값을 편집 하는 방법을 보여 줍니다.

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.storage-0.spec.settings.spark.includeSpark=false"
```

## <a id="podplacement"></a> Kubernetes 레이블을 사용하여 Pod 배치 구성

다양한 유형의 워크로드 요구 사항에 맞게 특정 리소스가 있는 Kubernetes 노드의 Pod 배치를 제어할 수 있습니다. 예를 들어 저장소 풀 리소스 pod가 더 많은 저장소가 있는 노드에 배치 되도록 하거나, SQL Server 마스터 인스턴스가 더 높은 CPU 및 메모리 리소스가 있는 노드에 배치 되도록 할 수 있습니다. 이 경우에는 먼저 다양한 유형의 하드웨어를 사용하여 다른 유형의 Kubernetes 클러스터를 빌드한 다음, 적절하게 [노드 레이블을 할당](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)합니다. 빅 데이터 클러스터를 배포할 때 클러스터 배포 구성 파일의 풀 수준에서 동일한 레이블을 지정할 수 있습니다. 그러면 Kubernetes가 지정된 레이블과 일치하는 노드의 Pod에 선호도를 지정합니다. Kubernetes 클러스터의 노드에 추가 해야 하는 특정 레이블 키는 **mssql 클러스터 전체**에 해당 합니다. 이 레이블 자체의 값은 선택한 문자열일 수 있습니다.

다음 예제에서는 SQL Server 마스터 인스턴스, 계산 풀, 데이터 풀 & 저장소 풀에 대 한 노드 레이블 설정을 포함 하도록 사용자 지정 구성 파일을 편집 하는 방법을 보여 줍니다. 기본 제공 구성에는 *nodeLabel* 키가 없으므로 사용자 지정 구성 파일을 수동으로 편집 하거나 패치 파일을 만들고 사용자 지정 구성 파일에 적용 해야 합니다. SQL Server 마스터 인스턴스 pod는 값이 **bdc-마스터**인 **mssql-클러스터 전체** 를 포함 하는 노드에 배포 됩니다. 계산 풀 및 데이터 풀 pod는 **mssql-클러스터 차원의** 값이 **bdc-sql**인 노드에 배포 됩니다. 저장소 풀 pod는 **mssql-클러스터 전체** **에 값이**포함 된 노드에 배포 됩니다.

다음 내용을 사용하여 현재 디렉터리에 **patch.json**이라는 파일을 만듭니다.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.master.spec",
      "value": {
        "type": "Master",
        "replicas": 1,
        "endpoints": [
          {
            "name": "Master",
            "serviceType": "NodePort",
            "port": 31433
          }
        ],
        "settings": {
          "sql": {
            "hadr.enabled": "false"
          }
        },
        "nodeLabel": "bdc-master"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.compute-0.spec",
      "value": {
        "type": "Compute",
        "replicas": 1,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.data-0.spec",
      "value": {
        "type": "Data",
        "replicas": 2,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 3,
        "nodeLabel": "bdc-storage",
        "settings": {
          "spark": {
            "includeSpark": "true"
          }
        }
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
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

- 는 **bdc. json**의 저장소 풀에 대 한 풀 저장소 설정을 업데이트 합니다.
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

- 는 **bdc. json**의 저장소 풀에 대 한 Spark 설정을 업데이트 합니다.
```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.services.spark.settings",
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

- 두 개의 인스턴스를 사용 하 여 두 개의 spark 풀을 **만듭니다.**
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
   }
  ]
}
```

> [!TIP]
> 배포 구성 파일을 변경하기 위한 구조 및 옵션에 대한 자세한 내용은 [빅 데이터 클러스터의 배포 구성 파일 참조](reference-deployment-config.md)를 참조하세요.

**azdata bdc config** 명령을 사용하여 JSON 패치 파일의 변경 내용을 적용합니다. 다음 예제에서는 **사용자 지정/** a s c. **json 파일을** 대상 배포 구성 파일에 적용 합니다.

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="disable-elasticsearch-to-run-in-privileged-mode"></a>특권 모드에서 실행 되는 ElasticSearch 사용 안 함
기본적으로 ElasticSearch 컨테이너는 빅 데이터 클러스터의 권한 모드로 실행 됩니다. 이는 컨테이너 초기화 시간에 ElasticSearch가 더 많은 양의 로그를 처리할 때 컨테이너에 호스트 키워드가 필수 설정을 업데이트할 수 있는 충분 한 권한이 있는지 확인 하기 위한 것입니다. 이 항목에 대 한 자세한 내용은 [이 문서](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)에서 찾을 수 있습니다. 

ElasticSearch를 실행 하는 컨테이너를 사용 하지 않도록 설정 하 여 특권 모드에서 실행 하려면 **컨트롤** 의 **settings** 섹션을 업데이트 하 고 vm의 값을 지정 해야 **합니다. 최대 _map_count** 는 **-1**입니다. 다음은이 섹션의 예입니다.
```json
"settings": {
    "ElasticSearch": {
        "vm.max_map_count": "-1"
      }
}
```

수동으로 **를 편집 하 고 위의** 섹션을 **사양**에 추가 하거나, 아래와 같이 패치 파일 **elasticsearch** 를 만들고 **azdata** CLI를 사용 하 여 컨트롤을 패치할 수 있습니다 **. json** 파일:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec",
      "value": {
        "docker": {
            "registry": "mcr.microsoft.com",
            "repository": "mssql/bdc",
            "imageTag": "2019-RC1-ubuntu",
            "imagePullPolicy": "Always"
        },
        "storage": {
            "data": {
                "className": "default",
                "accessMode": "ReadWriteOnce",
                "size": "15Gi"
            },
            "logs": {
                "className": "default",
                "accessMode": "ReadWriteOnce",
                "size": "10Gi"
            }
        },
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
        ],
        "settings": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
             }
        }
       }
    }
  ]
}
```

다음 명령을 실행 하 여 구성 파일을 패치 합니다.
```
azdata bdc config patch --config-file control.json --patch-file elasticsearch-patch.json
```

> [!IMPORTANT]
> [이 문서의](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)지침에 따라 Kubernetes 클러스터의 각 호스트에서 수동으로 **max_map_count** 설정을 수동으로 업데이트 하는 것이 좋습니다.
## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 배포에서 구성 파일을 사용 하는 방법에 대 한 자세한 내용은 [Kubernetes에서 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]를 배포 하는 방법](deployment-guidance.md#configfile)을 참조 하세요.
