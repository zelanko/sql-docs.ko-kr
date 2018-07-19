---
title: Linux의 SQL Server 장애 조치 클러스터 인스턴스-작동 | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: e48f0e7150fa24361c8b854ced6f90b22448a68b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38001686"
---
# <a name="operate-failover-cluster-instance---sql-server-on-linux"></a>Linux의 SQL Server 장애 조치 클러스터 인스턴스-작동

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux에서 SQL Server 장애 조치 클러스터 인스턴스 (FCI)를 운영 하는 방법을 설명 합니다. Linux의 SQL Server FCI를 만들지 않은 경우 [구성 장애 조치 클러스터 인스턴스-Linux의 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)합니다. 

## <a name="failover"></a>장애 조치 

Fci에 대 한 장애 조치는 Windows Server 장애 조치 클러스터 (WSFC)와 비슷합니다. 일종의 오류가 발생 하는 FCI를 호스팅하는 클러스터 노드의 하는 경우 FCI 자동으로 장애 조치를 다른 노드로 합니다. WSFC와 달리 Pacemaker FCI에 대 한 새 호스트 되는 노드를 선택 하도록 기본 설정된 소유자를 설정 하 방법이 있습니다.

수동으로 다른 노드로 FCI 장애 복구 하려는 경우가 있습니다. 프로세스와 동일 하 게 하는 WSFC의 Fci 아닙니다. Wsfc의 경우 역할 수준에서 리소스에 대 한 실패합니다. Pacemaker에서 리소스를 이동 하려면 선택한 모든 제약 조건을 올바른지 가정 하 고, 기타 등등 이동도 합니다. 

장애 조치 하는 방법은 Linux 배포판에 따라 달라 집니다. Linux 배포에 대 한 지침을 따릅니다.

- [RHEL 또는 Ubuntu](#rhelFailover)
- [SLES](#slesFailover)

## <a name = "#rhelFailover"></a> 수동 장애 조치 (RHEL 또는 Ubuntu)

Red Hat Enterprise Linux (RHEL) 제목을 또는 Ubuntu 서버는 수동 장애 조치를 수행 하려면 다음 단계를 실행 합니다.
1.  다음 명령을 사용 합니다. 

   ```bash
   sudo pcs resource move <FCIResourceName> <NewHostNode> 
   ```

   \<FCIResourceName > SQL Server FCI에 대 한 Pacemaker 리소스 이름입니다.

   \<NewHostNode > FCI를 호스팅할 클러스터 노드의 이름입니다. 

   모든 승인을 받지 못합니다.

2.  수동 장애 조치 하는 동안 Pacemaker 수동으로 이동 하도록 선택 된 된 리소스에 위치 제약 조건을 만듭니다. 이 제약 조건을 확인 하려면 실행 `sudo pcs constraint`합니다.

3.  장애 조치를 완료 한 후 실행 하 여 제약 조건을 제거 `sudo pcs resource clear <FCIResourceName>`합니다. 

\<FCIResourceName >은 FCI에 대 한 Pacemaker 리소스 이름입니다. 

## <a name = "#slesFailover"></a> 수동 장애 조치 (SLES)


Enterprise Server SLES (Suse Linux)를 사용 하 여는 `migrate` SQL Server FCI 수동 장애 조치 하는 명령입니다. 예를 들어:

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

- [장애 조치 클러스터 인스턴스-Linux의 SQL Server 구성](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
