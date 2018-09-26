---
title: Kubernetes 클러스터에서 SQL Server Always On 가용성 그룹에 연결
description: 이 문서에서는 Always On 가용성 그룹에 연결 하는 방법 설명
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d13f89a1297d21c882075821a681886dc95c4c76
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049593"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>SQL Server Always On 가용성 그룹에서 kubernetes에 연결

SQL Server의에서 인스턴스에 연결 하려면 Kubernetes 클러스터에 컨테이너를 만들려면를 [부하 분산 서비스](http://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)합니다. 부하 분산 장치 IP 주소를 SQL Server 인스턴스를 실행 하는 pod에 대 한 요청을 전달 합니다.

가용성 그룹 복제본에 연결 하려면 다른 복제본 형식에 대 한 서비스를 만듭니다. 서비스에 있는 복제본의 다른 형식에 대 한 예제를 확인할 수 있습니다 [sql server 샘플](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml)합니다.

* `ag1-primary` 주 복제본을 가리킵니다.
* `ag1-secondary-sync` 동기 보조 복제본을 가리킵니다.
* `ag1-secondary-async` 비동기 보조 복제본을 가리킵니다.

동일한 형식의 둘 이상의 보조 복제본이 있으면 Kubernetes 라운드 로빈 방식으로 서로 다른 복제본에 연결을 라우팅합니다.

## <a name="create-a-load-balancer-service"></a>부하 분산 장치 서비스 만들기

주 복제본에 대 한 부하 분산 장치 서비스를 만들려면 복사 `ag1-primary.yaml` 에서 [sql server 샘플]()및 가용성 그룹에 대 한 업데이트 합니다.

다음 명령은 클러스터.yaml 파일을 적용 대상:

```kubectl
kubectl apply -f ag1-primary.yaml
```

## <a name="get-the-ip-address-for-your-load-balancer-service"></a>부하 분산 장치 서비스에 대 한 IP 주소를 가져옵니다.

부하 분산 장치 서비스에 대 한 부하 분산 장치 IP 주소를 가져오려면 실행

```kubectl
kubectl get services
```

에 연결 하려는 서비스의 IP 주소를 식별 합니다.

## <a name="connect-to-primary-replica"></a>주 복제본에 연결

SQL 인증을 사용 하 여 주 복제본에 연결 하려면 사용 합니다 `sa` 계정, 값 `sapassword` , 만든 비밀 및이 IP 주소에서 합니다.

예를 들어:

```cmd
sqlcmd -S <0.0.0.0> -U sa -P "<MyC0m9l&xP@ssw0rd>"
```

## <a name="next-steps"></a>다음 단계

[Kubernetes 클러스터에서 SQL Server 가용성 그룹 관리](sql-server-linux-kubernetes-manage.md)

[Kubernetes 클러스터에서 SQL Server 가용성 그룹](sql-server-ag-kubernetes.md)