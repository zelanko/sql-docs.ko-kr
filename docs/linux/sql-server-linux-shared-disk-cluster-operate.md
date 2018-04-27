---
title: 장애 조치 클러스터 인스턴스-Linux에서 SQL Server 작동 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.workload: Inactive
ms.openlocfilehash: 71b017533aab9f1baef0d7340b509e4478220368
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="operate-failover-cluster-instance---sql-server-on-linux"></a>장애 조치 클러스터 인스턴스에 SQL Server Linux에서 작동 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서는 Linux에서 SQL Server 장애 조치 클러스터 인스턴스 (FCI) 작동 하는 방법을 설명 합니다. Linux에서 SQL Server FCI를 만들지 않은 경우 참조 [구성 장애 조치 클러스터 인스턴스-Linux에서 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)합니다. 

## <a name="failover"></a>장애 조치

Fci에 대 한 장애 조치가 Windows Server 장애 조치 클러스터 (WSFC)와 비슷합니다. FCI를 호스팅하는 클러스터 노드의 어떤 종류의 오류 발생, 하는 경우 FCI 자동으로 장애 조치를 다른 노드로 합니다. WSFC에서와 달리 없습니다 방법이 Pacemaker에서 FCI에 대 한 새 호스트 될 노드를 선택 하도록 기본 설정된 소유자를 설정할 수 있습니다.

수동으로 다른 노드로 FCI를 장애 하려는 경우가 있습니다. 프로세스는 WSFC에 Fci와 마찬가지로 동일 합니다. Wsfc에서 역할 수준에서 리소스에 대해 실패 합니다. Pacemaker에서 리소스를 이동 하려면 선택한 모든 제약 조건을 올바른지 라고 가정할 경우 다른 모든 항목에 들어왔다도 합니다. 

장애 조치 하는 방법은 Linux 배포판에 따라 달라 집니다. Linux 배포판에 대 한 지침을 따릅니다.

- [RHEL 또는 Ubuntu](#rhelFailover)
- [SLES](#slesFailover)

## <a name = "#rhelFailover"></a> 수동 장애 조치 (RHEL 또는 Ubuntu)

Red Hat Enterprise Linux (RHEL) onn 또는 Ubuntu 서버는 수동 장애 조치를 수행 하려면 다음 단계를 실행 합니다.
1.  다음 명령을 실행 합니다. 

   ```bash
   sudo pcs resource move <FCIResourceName> <NewHostNode> 
   ```

   \<FCIResourceName > SQL Server FCI에 대 한 Pacemaker 리소스 이름입니다.

   \<NewHostNode > FCI를 호스팅할 클러스터 노드의 이름입니다. 

   승인이 가져올 수 없습니다.

2.  수동 장애 조치 하는 동안 Pacemaker 수동으로 이동 하도록 선택 된 리소스에 위치 제약 조건을 만듭니다. 이 제약 조건의 보려면 실행 `sudo pcs constraint`합니다.

3.  장애 조치 완료 된 후 실행 하 여 제약 조건을 제거 `sudo pcs resource clear <FCIResourceName>`합니다. 

\<FCIResourceName > FCI에 대 한 Pacemaker 리소스 이름입니다. 

## <a name = "#slesFailover"></a> 수동 장애 조치 (SLES)


Suse Linux Enterprise Server (SLES)를 사용 하 여는 `migrate` SQL Server FCI를 수동으로 장애 조치가 가능 하도록 명령 합니다. 예를 들어:

```bash
crm resource migrate <FCIResourceName> <NewHostNode>
```

\<FCIResourceName > 장애 조치 클러스터 인스턴스에 대 한 리소스 이름입니다. 

\<NewHostNode > 새 대상 호스트의 이름입니다. 


<!---
|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)
--->

## <a name="next-steps"></a>다음 단계

- [장애 조치 클러스터 인스턴스-Linux에서 SQL Server 구성](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
