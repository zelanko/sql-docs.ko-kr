---
title: SQL Server 컨테이너의 고가용성
description: SQL Server 컨테이너의 고가용성에 대해 알아봅니다. Kubernetes에서 SQL Server와 함께 컨테이너를 배포하는 방법에 대해서도 알아봅니다.
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: d7e15c070b17fd0a3682f5572c9b7cd3ce2c1dee
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115656"
---
# <a name="high-availability-for-sql-server-containers"></a>SQL Server 컨테이너의 고가용성

Kubernetes에서 기본적으로 SQL Server 인스턴스를 만들고 관리합니다.

[Kubernetes](https://kubernetes.io/)에서 관리하는 docker 컨테이너에 SQL Server를 배포합니다. Kubernetes에서 클러스터 노드가 실패하는 경우 SQL Server 인스턴스가 포함된 컨테이너가 자동으로 복구될 수 있습니다.

SQL Server 2017에는 Kubernetes에서 배포할 수 있는 Docker 이미지가 도입되었습니다. Kubernetes PVC(영구적 볼륨 클레임)를 사용하여 이미지를 구성할 수 있습니다. Kubernetes는 컨테이너의 SQL Server 프로세스를 모니터링합니다. 프로세스, Pod, 컨테이너 또는 노드가 실패하는 경우 Kubernetes는 자동으로 다른 인스턴스를 부트스트랩하고 스토리지에 다시 연결합니다.

## <a name="container-with-sql-server-instance-on-kubernetes"></a>Kubernetes의 SQL Server 인스턴스가 포함된 컨테이너

Kubernetes 1.6 이상에서는 [*스토리지 클래스*](https://kubernetes.io/docs/concepts/storage/storage-classes/), [*영구적 볼륨 클레임*](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims) 및 [*Azure 디스크 볼륨 유형*](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk)을 지원합니다. 

이 구성에서 Kubernetes는 컨테이너 오케스트레이터의 역할을 수행합니다. 

![Kubernetes SQL Server 클러스터의 다이어그램](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

위 다이어그램에서 `mssql-server`는 [*Pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod/)의 SQL Server 인스턴스(컨테이너)입니다. [복제본 세트](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)는 노드 실패 후에 Pod가 자동으로 복구되도록 합니다. 애플리케이션이 서비스에 연결됩니다. 이 경우 서비스는 `mssql-server` 실패 후에도 동일하게 유지되는 IP 주소를 호스트하는 부하 분산 장치를 나타냅니다.

Kubernetes는 클러스터의 리소스를 오케스트레이션합니다. SQL Server 인스턴스 컨테이너를 호스트하는 노드가 실패하면 SQL Server 인스턴스가 포함된 새 컨테이너를 부트스트랩하고 동일한 영구적 스토리지에 연결합니다.

SQL Server 2017 이상에서는 Kubernetes의 컨테이너를 지원합니다.

Kubernetes에서 컨테이너를 만들려면 [Kubernetes에 SQL Server 컨테이너 배포](tutorial-sql-server-containers-kubernetes.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

AKS(Azure Kubernetes Service)에 SQL Server 컨테이너를 배포하려면 다음 예제를 참조하세요.
* [Docker 컨테이너에 SQL Server 배포](./sql-server-linux-docker-container-deployment.md)
* [Kubernetes에 SQL Server 컨테이너 배포](tutorial-sql-server-containers-kubernetes.md)