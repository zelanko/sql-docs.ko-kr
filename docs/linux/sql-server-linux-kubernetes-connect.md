---
title: Kubernetes 클러스터의 SQL Server Always On 가용성 그룹에 연결
description: 이 문서에서는 Always On 가용성 그룹에 연결하는 방법을 설명합니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f05bc51f587723414d3b0a4090fe2b27ad5fb837
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952601"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>Kubernetes의 SQL Server Always On 가용성 그룹에 연결

Kubernetes 클러스터의 컨테이너에 있는 SQL Server 인스턴스에 연결하려면 [부하 분산 장치 서비스](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)를 만듭니다. 부하 분산 장치는 엔드포인트입니다. IP 주소가 있으며, IP 주소에 대한 요청을 SQL Server 인스턴스가 실행되는 Pod에 전달합니다.

가용성 그룹 복제본에 연결하려면 여러 복제본 유형의 서비스를 만듭니다. [sql-server-samples/ag-services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)에서 여러 복제본 유형의 서비스 예를 확인할 수 있습니다.

* `ag1-primary`는 주 복제본을 가리킵니다.
* `ag1-secondary`는 보조 복제본을 가리킵니다.

보조 복제본이 두 개 이상인 경우 Kubernetes는 라운드 로빈 방식으로 연결을 다른 복제본으로 라우팅합니다.

## <a name="create-a-load-balancer-service"></a>부하 분산 장치 서비스 만들기

주 복제본과 보조 복제본의 부하 분산 장치 서비스를 만들려면 [sql-server-samples](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-file)에서 [`ag1-services.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml)을 복사하고 해당 가용성 그룹에 맞게 업데이트합니다.

다음 명령은 `.yaml` 파일의 구성을 클러스터에 적용합니다.

```kubectl
kubectl apply -f ag1-services.yaml --namespace ag1
```

## <a name="get-the-ip-address-for-your-load-balancer-service"></a>부하 분산 장치 서비스의 IP 주소 가져오기

부하 분산 장치 서비스의 부하 분산 장치 IP 주소를 가져오려면 다음 명령을 실행합니다.

```kubectl
kubectl get services
```

연결하려는 서비스의 IP 주소를 확인합니다.

## <a name="connect-to-primary-replica"></a>주 복제본에 연결

SQL 인증을 사용하여 주 복제본에 연결하려면 `sa` 계정, 직접 만든 비밀의 `sapassword` 값, 이 IP 주소를 사용합니다.

예를 들어

```cmd
sqlcmd -S <0.0.0.0> -U sa -P "<MyC0m9l&xP@ssw0rd>"
```

## <a name="next-steps"></a>다음 단계

[Kubernetes 클러스터의 SQL Server 가용성 그룹 관리](sql-server-linux-kubernetes-manage.md)

[Kubernetes 클러스터의 SQL Server 가용성 그룹](sql-server-ag-kubernetes.md)
