---
title: SQL Server Always On 가용성 그룹 관리 Kubernetes
description: 이 문서는 SQL Server Always On 가용성 그룹에서 Kubernetes 관리 하는 방법에 설명 합니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8ad318c0f0967f26f5cfdf2c5ad9af2d94323bf0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622841"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>SQL Server 가용성 그룹 Kubernetes Always On 관리

Always On 가용성 그룹에서 kubernetes를 관리 하려면 매니페스트를 만들고 클러스터에 적용 합니다. 매니페스트는는 `.yaml` 파일입니다.  

이 문서의 예제에서는 모든 Kubernetes 클러스터에 적용 됩니다. 이 예제 시나리오는 Azure Kubernetes Service에서 클러스터에 대해 적용 됩니다.

예를 보려면는 종단 간 배포의 [이 자습서](tutorial-sql-server-ag-kubernetes.md)합니다.

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>장애 조치-Kubernetes에서 SQL Server 가용성 그룹

가용성 그룹 주 복제본은 Kubernetes에서 다른 노드로 장애 조치할, 작업을 사용 합니다. 이 문서에서는이 작업에 대 한 환경 변수를 식별합니다.

매니페스트 파일의 다음 예제에서는 작업을 수동으로 장애 조치 Kubernetes 복제본에서 가용성 그룹에 대 한 작업을 설명 합니다. 예제에서는 새 파일의 내용을 복사 `failover.yaml`합니다.

[failover.yaml](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/templates/failover.yaml)

작업을 배포 하려면 사용 하 여 `Kubectl`입니다.

```azurecli
kubectl apply -f failover.yaml
```

매니페스트 파일에 적용할 때 Kubernetes 작업을 실행 합니다. 작업 실행 시 감독자 새 리더를 선택 하 고 프로덕션에서는 리더의 SQL Server 인스턴스를 주 복제본 이동 합니다.

작업을 실행 한 후 삭제 합니다. Kubernetes에서 작업 개체의 상태를 볼 수 있도록 완료 된 후 남아 있습니다. 해당 상태를 확인 한 후 이전 작업을 수동으로 삭제 해야 합니다. Kubernetes 로그 삭제 작업을 삭제 하면 됩니다. 작업을 삭제 하면 작업의 이름 및 pod 선택기를 변경 하지 않는 한 이후 장애 조치 작업이 실패 합니다. 자세한 내용은 [-작업 실행을 완료 하려면](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)합니다.

## <a name="rotate-credentials"></a>자격 증명 회전

SA 및 마스터 키를 업데이트 하는 자격 증명을 회전 합니다.

복사 합니다 [회전 creds.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script) 로컬에서 사용할 `kubectl` 클러스터에 적용 합니다.

```azurecli
kubectl apply -f rotate-creds.yaml
```

## <a name="next-steps"></a>다음 단계

[Azure Kubernetes Service (AKS)를 사용 하 여 Kubernetes 대시보드에 액세스](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Kubernetes 클러스터에서 SQL Server 가용성 그룹](sql-server-ag-kubernetes.md)
