---
title: 배포 구성
titleSuffix: SQL Server big data clusters
description: 구성 파일을 사용 하 여 빅 데이터 클러스터 배포를 사용자 지정 하는 방법을 알아봅니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ed86e7d293ba72eb178c65b53865b62ca419a6d2
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993994"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>빅 데이터 클러스터에 대 한 배포 설정을 구성 합니다.

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

클러스터 배포 구성 파일을 사용자 지정 하려면 VSCode와 같은 json 형식 편집기를 사용할 수 있습니다. 에서는 자동화를 위한 이러한 편집 스크립팅를 **mssqlctl 클러스터 구성 섹션** 명령입니다. 이 문서에서는 배포 구성 파일을 수정 하 여 빅 데이터 클러스터 배포를 구성 하는 방법에 설명 합니다. 다양 한 시나리오에 대 한 구성을 변경 하는 방법에 대 한 예제를 제공 합니다. 배포에서 구성 파일은 사용 하는 방법에 대 한 자세한 내용은 참조는 [배포 가이드](deployment-guidance.md#configfile)합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [Mssqlctl 설치](deploy-install-mssqlctl.md)합니다.

- 이 섹션의 예에서는 각 가정 표준 구성 파일 중 하나의 복사본을 만들어야 합니다. 자세한 내용은 [사용자 지정 구성 파일을 만들어](deployment-guidance.md#customconfig)합니다. 예를 들어 다음 명령은 만듭니다는 **custom.json** 기본값에 따라 파일 **aks-dev-test.json** 구성:

   ```bash
   mssqlctl cluster config init --src aks-dev-test.json --target custom.json
   ```

## <a id="clustername"></a> 클러스터 이름 변경

클러스터 이름에는 빅 데이터 클러스터 및 배포에서 생성 되는 Kubernetes 네임 스페이스 이름이입니다. 배포 구성 파일의 다음 부분에 지정 되어 있습니다.

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

다음 명령을 전송 하는 키-값 쌍을 **--json 값** 빅 데이터 클러스터 이름을 변경 하려면 매개 변수 **테스트 클러스터**:

```bash
mssqlctl cluster config section set -c custom.json -j ".metadata.name=test-cluster"
```

> [!IMPORTANT]
> 클러스터의 이름에는 소문자 영숫자 문자만 공백 없이 이어야 합니다. 클러스터와 동일한 이름 가진 네임 스페이스의 클러스터에 대 한 모든 Kubernetes 아티팩트 (컨테이너, pod, 상태 집합, 서비스)를 만들 수는 지정 된 이름입니다.

## <a id="ports"></a> 끝점 포트를 업데이트 합니다.

끝점도 개별 풀의 경우와 제어 평면에 대 한 정의 됩니다. 구성 파일의 다음 부분에는 제어 평면에 대 한 끝점 정의 보여 줍니다.

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
    },
    {
        "name": "AppServiceProxy",
        "serviceType": "LoadBalancer",
        "port": 30778
    },
    {
        "name": "Knox",
        "serviceType": "LoadBalancer",
        "port": 30443
    }
]
```

다음 예제에서는 인라인 JSON을 사용 하 여에 대 한 포트를 변경 하는 **컨트롤러** 끝점:

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.controlPlane.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> 복제본 풀 구성

저장소 풀과 같은 각 풀의 특징은 구성 파일에서 정의 됩니다. 예를 들어, 다음 부분은 저장소 풀 정을 보여 줍니다.

```json
"pools": [
    {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Storage",
            "replicas": 2,
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
        }
    }
]
```

수정 하 여 풀의 인스턴스 수를 구성할 수 있습니다 합니다 **복제본** 각 풀에 대 한 값입니다. 다음 예제에서는 인라인 JSON을 사용 하 여 저장소 및 데이터 풀에 대 한 이러한 값을 변경 하려면 `10` 고 `4` 각각.

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4'
```

## <a id="storage"></a> 저장소 구성

또한 저장소 클래스와 각 풀에 사용 되는 특성을 변경할 수 있습니다. 다음 예제에서는 저장소 풀에 사용자 지정 저장소 클래스를 할당 및 100 gb 데이터를 저장 하는 데는 영구적 볼륨 클레임의 크기를 업데이트 합니다. 사용 하 여 설정을 업데이트 하려면 구성 파일에서이 섹션에서는 사용 해야 합니다 *mssqlctl 클러스터 구성 집합* 명령이 패치 파일을 사용 하 여이 섹션을 추가 하는 방법을 아래를 참조 하세요:

```bash
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.className=storage-pool-class"
mssqlctl cluster config section set -c custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.size=32Gi"
```

> [!NOTE]
> 구성 파일을 기반으로 **kubeadm-dev-test.json** 각 풀에 있지만 수동으로 추가할 수 있습니다 필요한 경우에 대 한 저장소 정의가 없습니다.

저장소 구성에 대 한 자세한 내용은 참조 하세요. [빅 데이터에서 kubernetes 클러스터는 SQL Server를 사용 하 여 데이터 지 속성](concept-data-persistence.md)합니다.

## <a id="podplacement"></a> Kubernetes 레이블을 사용 하 여 pod 배치 구성

다양 한 유형의 워크 로드 요구 사항에 맞게 특정 리소스가 있는 Kubernetes 노드에서 pod 배치를 제어할 수 있습니다. 예를 들어, 다음 저장소 풀 pod 더 많은 저장소를 사용 하 여 노드에 배치 됩니다 또는 SQL Server 마스터 인스턴스에 더 높은 CPU 및 메모리 리소스가 있는 노드에 배치 되는지 확인 하는 것이 좋습니다. 이 경우 먼저 만들어야 다양 한 유형의 하드웨어를 사용 하 여 다른 유형의 Kubernetes 클러스터 차례로 [노드 레이블을 할당할](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) 적절 하 게 합니다. 빅 데이터 클러스터를 배포 하는 동시에 동일한 레이블 풀 수준에서 클러스터 배포 구성 파일에서 지정할 수 있습니다. Kubernetes 지정한 레이블과 일치 하는 노드에 pod를 해 다음 처리 됩니다.

다음 예제에서는 SQL Server 마스터 인스턴스에 대 한 노드 레이블 설정을 포함 하도록 사용자 지정 구성 파일을 편집 하는 방법을 보여 줍니다. 없습니다 *nodeLabel* 사용자 지정 구성 파일을 수동으로 편집 하거나 패치 파일을 만들고 및 사용자 지정 구성 파일에 적용 해야 하므로 기본 제공된 구성의 키입니다.

이라는 파일을 만듭니다 **patch.json** 다음 콘텐츠를 사용 하 여 현재 디렉터리에 있습니다.

```json
{
  "patch": [
     {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Master')].spec",
      "value": {
      "nodeLabel": "<yourNodeLabel>"
       }
    }
  ]
}
```

```bash
mssqlctl cluster config section set -c custom.json -p ./patch.json
```

## <a id="jsonpatch"></a> JSON 패치 파일

JSON 패치 파일이 한 번에 여러 설정을 구성합니다. JSON 패치에 대 한 자세한 내용은 참조 하세요. [Python에 대 한 JSON 패치](https://github.com/stefankoegl/python-json-patch) 하며 [JSONPath 온라인 계산기](https://jsonpath.com/)합니다.

다음 **patch.json** 파일 다음 변경 작업을 수행 합니다.

- 단일 끝점의 포트를 업데이트합니다.
- 모든 끝점을 업데이트 (**포트** 하 고 **serviceType**).
- 제어 평면 저장소를 업데이트합니다. 이러한 설정은 풀 수준에서 재정의 되지 않은 경우 모든 클러스터 구성 요소에 적용할 수 있습니다.
- 제어 평면 저장소의 저장소 클래스 이름을 업데이트합니다.
- 저장소 풀에 대 한 풀 저장소 설정을 업데이트합니다.
- 저장소 풀에 대 한 Spark 설정을 업데이트합니다.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.controlPlane.spec.endpoints[?(@.name=='Controller')].port",
      "value": 30000
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.endpoints",
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
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30778,
            "name": "AppServiceProxy"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30443,
            "name": "Knox"
        }
      ]
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.controlPlane",
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
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.storage.data.className",
      "value": "managed-premium"
    },
    {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage",
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
    },
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

> [!TIP]
> 구조 및 배포 구성 파일을 변경 하는 것에 대 한 옵션에 대 한 자세한 내용은 참조 하세요. [빅 데이터 클러스터에 대 한 배포 구성 파일 참조](reference-deployment-config.md)합니다.

사용 하 여 **mssqlctl 클러스터 구성 섹션 집합** JSON 패치 파일에 변경 내용을 적용 합니다. 다음 예제에서는 적용 합니다 **patch.json** 대상 배포 구성 파일에 파일 **custom.json**합니다.

```bash
mssqlctl cluster config section set -c custom.json -p ./patch.json
```

## <a name="next-steps"></a>다음 단계

빅 데이터 클러스터 배포에서 구성 파일을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [빅 데이터를 SQL Server를 배포 하는 방법에서 kubernetes 클러스터](deployment-guidance.md#configfile)합니다.
