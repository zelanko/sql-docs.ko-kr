---
title: SQL Server 속성 (AlwaysOn 고가용성 탭) | Microsoft Docs
description: 2014 SQL Server에서 AlwaysOn 가용성 그룹 기능을 설정 하거나 해제 하는 방법에 대해 알아봅니다. 서버 인스턴스가이 기능에 대해 충족 해야 하는 필수 구성 요소를 확인 합니다.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: d8630923-a600-4f1c-aca1-027453a3ec82
author: mikeraymsft
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4e15cc28354d8dc77b579008feabbc6d13efb63d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939094"
---
# <a name="sql-server-properties-alwayson-high-availability-tab"></a>SQL Server 속성(AlwaysOn 고가용성 탭)
  **** 구성 관리자에서 **SQL Server 속성** 대화 상자의 AlwaysOn 고가용성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 탭을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 AlwaysOn 가용성 그룹 기능을 사용하거나 사용하지 않도록 설정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 고가용성 및 재해 복구 솔루션으로 가용성 그룹을 사용하려면 먼저 AlwaysOn 가용성 그룹을 사용하도록 설정해야 합니다.  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a> 전제 조건  
 AlwaysOn 가용성 그룹을 사용하도록 설정하려면 서버 인스턴스가 다음과 같은 사전 요구 사항을 충족해야 합니다.  
  
-   서버 인스턴스는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 노드에 있어야 합니다.  
  
-   동일한 가용성 그룹에 있으려면 인스턴스가 동일한 WSFC 클러스터에 있어야 합니다. 가용성 그룹은 여러 WSFC 클러스터에 걸쳐 있을 수 없습니다.  
  
-   서버 인스턴스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 지원하는 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]버전을 실행해야 합니다.  
  
-   한 번에 한 서버 인스턴스에 대해서만 AlwaysOn 가용성 그룹을 사용하도록 설정합니다. AlwaysOn 가용성 그룹을 사용하도록 설정한 후에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 다시 시작될 때까지 기다렸다가 다음 서버 인스턴스를 사용하도록 설정합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]에 대한 기능 지원과 추가 사전 요구 사항, 제한 사항 및 권장 사항에 대한 자세한 내용은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 온라인 설명서를 참조하세요.  
  
## <a name="dialog-options"></a>대화 상자 옵션  
 **Windows 장애 조치(failover) 클러스터 이름**  
 로컬 컴퓨터가 노드인 WSFC 클러스터의 이름을 표시합니다.  
  
 **AlwaysOn 가용성 그룹 사용**  
 다음과 같이 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 AlwaysOn 가용성 그룹을 사용하거나 사용하지 않도록 설정하려면 이 확인란을 사용합니다.  
  
-   이 확인란이 비어 있으면 현재 AlwaysOn 가용성 그룹을 사용하지 않도록 설정되어 있습니다. AlwaysOn 가용성 그룹을 사용하도록 설정하려면 이 확인란을 선택하고 **확인**을 클릭한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 수동으로 다시 시작합니다.  
  
-   이 확인란이 이미 선택되어 있으면 현재 AlwaysOn 가용성 그룹을 사용하도록 설정되어 있습니다. AlwaysOn 가용성 그룹을 사용하지 않도록 설정하려면 이 확인란의 선택을 취소하고 **확인**을 클릭합니다. 이렇게 하면 서버 인스턴스가 다시 시작됩니다.  
  
    > [!TIP]  
    >  AlwaysOn 가용성 그룹을 사용하지 않도록 설정한 후 서버 인스턴스에서 모든 로컬 가용성 복제본을 제거해야 합니다. 지정된 가용성 그룹의 마지막 복제본을 제거하는 경우 그룹도 제거해야 합니다.  
  
## <a name="ui-element-list"></a>UI 요소 목록  
  
> [!NOTE]  
>  AlwaysOn 가용성 그룹을 사용하지 않도록 설정한 후의 후속 작업과 가용성 그룹을 만들고 구성하는 방법에 대한 자세한 내용은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 온라인 설명서를 참조하십시오.  
  
  
