---
title: 빅 데이터 클러스터 배포의 Active Directory 및 Kubernetes DNS 조정
description: Active Directory 모드에서 SQL Server 빅 데이터 클러스터에 대한 DNS 조정 구성
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 63a5c53e64ece7650e65414fd24ddd82d6da5324
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892463"
---
# <a name="active-directory-and-kubernetes-dns-reconciliation-in-big-data-clusters-deployments"></a>빅 데이터 클러스터 배포의 Active Directory 및 Kubernetes DNS 조정

이 문서에서는 BDC(빅 데이터 클러스터)를 배포할 때 몇 가지 문제와 Active Directory 통합을 수용하는 해결 방법에 대해 설명합니다.

## <a name="overview"></a>개요

빅 데이터 클러스터가 Active Directory 통합을 사용하여 배포되지 않은 경우 내부 DNS 확인을 위해 [Kubernetes CoreDNS](https://kubernetes.io/docs/tasks/administer-cluster/coredns/) 서비스를 사용합니다. Kubernetes는 `<namespace>.svc.cluster.local` 같은 내부 도메인을 사용합니다. 이 도메인에서 이름을 사용하여 DNS 서버에 A(정방향 조회) 레코드와 PTR(역방향 조회) 레코드를 만듭니다.

그러나 Active Directory 모드를 사용하는 경우에는 새 도메인 및 고유한 DNS 서버 세트가 사용됩니다. 이로 인해 내부 이름 확인 중에 DNS 정방향 조회 및 역방향 조회를 위해 사용할 서버 세트에 대한 혼동이 발생할 수 있습니다.

## <a name="challenges"></a>과제

* 새 Kubernetes Pod가 배포되면 두 DNS 서버 집합 모두에 DNS 항목을 추가해야 합니다. Kubernetes는 CoreDNS의 항목 기록을 처리하지만, Active Directory 도메인 컨트롤러 DNS 서버에 필요한 항목을 추가하는 일은 BDC 배포 워크플로에서 처리됩니다. 마찬가지로 BDC 클러스터가 삭제되면 워크플로는 이러한 항목이 제거되었는지 확인해야 합니다.
* Active Directory DNS 서버는 Kubernetes 클러스터 외부에 있습니다. 그러나 BDC는 Kubernetes 내부에 고유한 IP 공간을 가집니다. 이 IP 공간이 클러스터 경계 외부에 표시되지 않으므로 BDC는 외부에 배치된 DNS 서버에 이 IP 공간의 레코드를 만들 수 없습니다.
* Kubernetes 클러스터 내에서 장애 조치(failover) 이벤트가 발생하면 AD DNS 서버의 레코드도 업데이트해야 합니다.
* Pod 이름 외에 Kubernetes 서비스 이름도 AD 도메인 이름 조회를 통해 주소 지정이 가능해야 합니다. 여기서 Active Directory DNS에 추가 문제가 생깁니다. 하나의 서비스 이름이 여러 Pod IP 주소에 매핑될 수 있기 때문입니다.
* 조직의 Active Directory DNS 서버에서 레코드 업데이트 전파 및 복제 지연이 발생하면 BDC 관리 워크플로의 제어를 벗어나는 중대한 문제가 될 수 있습니다. 이 문제는 배포 및 장애 조치(failover) 시 즉시 BDC 기능에 영향을 줄 수 있습니다. 반면, Kubernetes CoreDNS는 그 위치로 인해 더 빠르고 효율적입니다.

## <a name="solution"></a>해결 방법

앞서 설명한 문제를 해결하기 위해 BDC에 구현된 솔루션에는 BDC 네임스페이스 내에서 관리되는 새로운 내부 CoreDNS 서비스가 포함됩니다. 이는 이름 확인을 위해 BDC 네임스페이스의 Pod가 연결되는 유일한 DNS 서비스입니다. 여러 도메인의 복잡성은 새 CoreDNS 서비스 뒤에 숨겨집니다.

예를 들어 다음 다이어그램에서 Pod는 BDC CoreDNS 서버를 사용하여 이름을 확인합니다. Pod는 Kubernetes CoreDNS server 또는 AD DNS 서버와 직접 상호 작용하지 않습니다. 

:::image type="content" source="media/active-directory-dns-reconciliation/bdc-ad-dns-reconciliation.png" alt-text="Pod가 자체 네임스페이스의 CoreDNS 서버에 연결됨":::

이 디자인이 BDC에서 작동하는 방식을 명확하게 보여 주는 구현 세부 정보입니다.

### <a name="centralized-management-of-multiple-domains"></a>여러 도메인에 대한 중앙 집중식 관리

이름 조회에서 이루어지는 작업의 복잡성은 중앙 집중식으로 내부 DNS 서비스 뒤에 숨겨진 상태로 유지됩니다. 이에 따라 여러 도메인을 개별 Pod에서 배치 및 관리하는 부담이 없고 디자인이 간소해집니다.

### <a name="no-records-for-internal-pods-in-external-dns-servers"></a>내부 Pod에 대한 레코드가 외부 DNS 서버에 없음

이 디자인 원칙에 따라, BDC는 외부 DNS 서버에서 Kubernetes IP 공간에 Pod에 대한 A 레코드 및 PTR 레코드를 만들고 관리할 필요가 없습니다.

### <a name="no-duplication-of-records"></a>레코드 중복 없음

여러 위치에 있는 내부 DNS 레코드. 이러한 레코드의 유일한 스토리지는 Kubernetes CoreDNS입니다. BDC 내부 CoreDNS는 계산을 재작성하고 DNS 쿼리를 Kubernetes CoreDNS에 전달합니다.

### <a name="computational-rewriting"></a>계산 재작성

BDC는 레코드를 저장하지 않으므로 들어오는 정방향 조회 쿼리를 AD 도메인이 있는 이름에서 Kubernetes 도메인이 있는 이름으로 변환하고 이 쿼리를 Kubernetes CoreDNS에 전달합니다.
예를 들어 `compute-0-0.contoso.local`의 들어오는 쿼리는 `compute-0-0.compute-0-svc.contoso.svc.cluster.local`로 재작성되고 이 요청은 Kubernetes CoreDNS에 전달됩니다.
역방향 조회의 경우 요청은 내부 IP를 사용하여 Kubernetes CoreDNS에 전달되며 클라이언트에 응답하기 전에 응답을 AD 도메인 이름으로 재작성합니다.

### <a name="simplicity-in-pod-configurations"></a>Pod 구성의 단순성

내부 BDC CoreDNS만 모든 BDC Pod의 /etc/resolv.conf에서 참조되므로 Pod에서 네트워크 보기가 간단해집니다. 대신 복잡성은 내부 CoreDNS에 숨겨집니다.

### <a name="static-and-reliable-ip-address-for-dns-service"></a>DNS 서비스에 대한 신뢰할 수 있는 정적 IP 주소

BDC가 배포하는 CoreDNS 서비스는 모든 Pod에서 액세스할 수 있는 정적 내부 IP를 등록합니다. 이렇게 하면 /etc/resolv.conf의 값을 업데이트할 필요가 없습니다.

### <a name="service-load-balance-management-is-retained-by-kubernetes"></a>Kubernetes에서 서비스 부하 분산 관리 보존

개별 Pod 아닌 서비스에 대해 조회가 발생하는 경우에도 여전히 Kubernetes CoreDNS에 전달되므로, BDC는 특히 AD 도메인에 대한 부하 분산을 구현하지 않습니다.

예를 들어 `compute-0-svc.contoso.local`에 대해 정방향 조회 요청이 발생하는 경우` compute-0-svc.contoso.svc.cluster`.local로 재작성됩니다. 이 요청은 Kubernetes CoreDNS에 전달되고 여기서 부하 분산이 이루어집니다. 응답은 여러 컴퓨팅 풀 인스턴스(Pod 복제본) 중 하나의 IP 주소입니다.

### <a name="scalability"></a>확장성

BDC는 레코드를 저장하지 않으므로, 여러 복제본에서 상태를 보존하고 레코드를 복제하지 않고도 내부 BDC CoreDNS를 스케일링할 수 있습니다. DNS 레코드가 BDC 내에 저장되는 경우 모든 Pod에서 상태를 복제하는 일도 BDC에서 처리해야 합니다.

### <a name="externally-visible-service-entries-stay-in-ad-dns"></a>외부에 표시되는 서비스 항목이 AD DNS에 유지됨

Kubernetes 클러스터 외부의 클라이언트에서 액세스해야 하는 서비스 엔드포인트의 경우 BDC가 배포되는 동안 AD DNS 서버에 DNS 항목이 생성됩니다. 사용자는 배포 구성 프로필을 통해 등록할 DNS 이름을 입력합니다.

### <a name="self-deprovisioning"></a>자동 프로비저닝 해제

BDC가 삭제된 후에는 클러스터의 프로비저닝을 해제할 때 DNS 항목을 삭제하는 추가 동적 작업이 없습니다. 정리해야 할 원격 Active Directory DNS 항목은 외부 서비스에 대한 항목뿐이며 그 숫자가 고정적입니다. 내부 DNS 항목은 클러스터와 함께 자동으로 제거됩니다.

## <a name="next-steps"></a>다음 단계

- [Active Directory 모드에서 SQL Server 빅 데이터 클러스터 배포](active-directory-deploy.md)
- [Active Directory 모드에서 빅 데이터 클러스터 액세스 관리](active-directory-objects.md)
- [Deploy multiple SQL Server Big Data Clusters in the same Active Directory domain](active-directory-deployment-background.md)(동일한 Active Directory 도메인에 여러 SQL Server 빅 데이터 클러스터 배포)
