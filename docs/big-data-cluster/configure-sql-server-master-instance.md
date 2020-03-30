---
title: SQL Server 마스터 인스턴스 구성
titleSuffix: Configure SQL Server master instance of Big Data Cluster
description: SQL Server 빅 데이터 클러스터의 마스터 인스턴스 구성
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a124b3a82c75f3da5f7abbdec3b519c86ec7c1c5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79090519"
---
# <a name="configure-master-instance-of-big-data-clusters-2019"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]의 마스터 인스턴스 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]의 마스터 인스턴스 구성

배포 시 SQL Server 마스터 인스턴스에 대해 서버 구성 설정을 구성할 수 없습니다. 이 문서에서는 SQL Server 버전, SQL Server 에이전트 사용 또는 사용 안 함, 특정 추적 플래그 사용 또는 사용 안 함, 고객 의견 사용/사용 안 함 등의 설정을 구성하는 방법에 대한 임시 해결 방안을 설명합니다.

이러한 설정을 변경하려면 다음 단계를 수행합니다.

1. 대상 설정을 포함하는 사용자 지정 `mssql-custom.conf` 파일을 만듭니다. 다음 예제는 SQL 에이전트, 원격 분석을 사용하도록 설정하고, Enterprise Edition의 PID를 설정하고, 추적 플래그 1204를 사용하도록 설정합니다.

   ```
   [sqlagent]
   enabled=true
   
   [telemetry]
   customerfeedback=true
   userRequestedLocalAuditDirectory = /tmp/audit

   [DEFAULT]
   pid = Enterprise

   [traceflag]
   traceflag0 = 1204
   ```

1. `mssql-custom.conf` 파일을 `/var/opt/mssql` Pod의 `mssql-server` 컨테이너에 있는 `master-0`에 복사합니다. `<namespaceName>`을 빅 데이터 클러스터 이름으로 바꿉니다.

   ```bash
   kubectl cp mssql-custom.conf master-0:/var/opt/mssql/mssql-custom.conf -c mssql-server -n <namespaceName>
   ```

1. SQL Server 인스턴스를 다시 시작합니다.  `<namespaceName>`을 빅 데이터 클러스터 이름으로 바꿉니다.

   ```bash
   kubectl exec -it master-0  -c mssql-server -n <namespaceName> -- /bin/bash
   supervisorctl restart mssql-server
   exit
   ```

> [!IMPORTANT]
> SQL Server 마스터 인스턴스가 가용성 그룹 구성에 있는 경우 모든 `mssql-custom.conf` Pod의 `master` 파일을 복사합니다. 다시 시작할 때마다 장애 조치(failover)가 발생하므로, 가동 중지 시간 동안 이 작업의 타이밍을 지정해야 합니다.

## <a name="known-limitations"></a>알려진 제한 사항

- 위의 단계를 수행하려면 Kubernetes cluster 관리자 권한이 필요합니다.
- 배포 후 빅 데이터 클러스터의 SQL Server 마스터 인스턴스에 대한 서버 데이터 정렬을 변경할 수 없습니다.

## <a name="next-steps"></a>다음 단계

SQL Server 빅 데이터 클러스터 배포에 대한 자세한 내용은 [SQL Server 빅 데이터 클러스터 시작](deploy-get-started.md)을 참조하세요.