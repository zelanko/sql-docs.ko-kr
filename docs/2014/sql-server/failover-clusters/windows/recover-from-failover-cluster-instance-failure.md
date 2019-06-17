---
title: 장애 조치(failover) 클러스터 인스턴스 오류 복구 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- clusters [SQL Server], recovery from failure
- failover clustering [SQL Server], recovery from failure
- hardware failures [SQL Server]
- recovering failover cluster failures [SQL Server]
ms.assetid: 3d151d0c-e841-4325-8606-c094de37d7d1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c4da45e57342288cc23a9783709666f4c02d0bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63050016"
---
# <a name="recover-from-failover-cluster-instance-failure"></a>장애 조치(failover) 클러스터 인스턴스 오류 복구
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 장애 조치(failover)가 발생한 후에 장애 조치(failover) 클러스터 관리자 스냅인을 사용하여 클러스터 오류를 복구하는 방법에 대해 설명합니다. 장애 조치 클러스터 관리자 스냅인은 WSFC(Windows Server 장애 조치(failover) 클러스터링) 서비스용 클러스터 관리 애플리케이션입니다.  
  
-   [복구 불가능 오류 복구](#Scenario1)  
  
-   [소프트웨어 오류 복구](#Scenario2)  
  
##  <a name="Scenario1"></a> 복구 불가능 오류 복구  
 복구 불가능 오류를 복구하려면 다음 단계를 따르세요. 예를 들어 디스크 컨트롤러 오류나 운영 체제 오류로 인해 이러한 오류가 발생할 수 있습니다. 이런 경우, 오류는 두 노드 클러스터의 노드 1의 하드웨어 오류로 인해 발생합니다.  
  
1.  노드 1에 오류가 발생한 후 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI에서 노드 2로 장애 조치됩니다.  
  
2.  FCI에서 노드 1을 제거합니다. 이렇게 하려면 노드 2에서 장애 조치(failover) 클러스터 관리자 스냅인을 열고 노드 1을 마우스 오른쪽 단추로 클릭하여 **이동 동작**을 클릭한 다음 **노드 제거**를 클릭합니다.  
  
3.  노드 1이 클러스터 정의에서 제거되었는지 확인합니다.  
  
4.  새 하드웨어를 설치하여 노드 1에서 장애가 발생한 하드웨어를 바꿉니다.  
  
5.  장애 조치(Failover) 클러스터 관리자 스냅인을 사용하여 기존 클러스터에 노드 1을 추가합니다. 자세한 내용은 [장애 조치(failover) 클러스터링을 설치하기 전에](../install/before-installing-failover-clustering.md)를 참조하세요.  
  
6.  관리자 계정이 모든 클러스터 노드에서 동일한지 확인합니다.  
  
7.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하여 FCI에 노드 1을 추가합니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)을 참조하세요.  
  
##  <a name="Scenario2"></a> 복구 가능 오류 복구  
 복구 가능 오류를 복구하려면 다음 단계를 따르세요. 이 단계에서 오류는 노드 1이 다운되거나 오프라인 상태가 되어 발생하지만 회복할 수 없는 상태는 아닙니다. 이는 운영 체제의 오류, 하드웨어 오류 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스 자체의 오류에 의해 발생할 수 있습니다.  
  
1.  노드 1에 오류가 발생한 후 FCI에서 노드 2로 장애 조치됩니다.  
  
2.  노드 1의 문제를 해결합니다.  
  
3.  WSFC 서비스가 작동하고 모든 노드가 온라인 상태인지 확인합니다.  
  
4.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 복구된 노드로 장애 조치합니다.  
  
  
