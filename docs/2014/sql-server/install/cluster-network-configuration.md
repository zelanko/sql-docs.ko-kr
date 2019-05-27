---
title: 클러스터 네트워크 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- cluster network selection, Setup
- cluster network selection
ms.assetid: 579482ef-a023-45b2-9176-b4a4188adf9d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 48dca8e9ce522f2520521441b2e7eea349ff099b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096442"
---
# <a name="cluster-network-configuration"></a>클러스터 네트워크 구성
  **클러스터 네트워크 선택** 페이지를 사용하여 장애 조치(Failover) 클러스터 인스턴스에 대한 네트워크 리소스를 지정할 수 있습니다.  
  
## <a name="options"></a>변수  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터 네트워크 이름** - 네트워크에서 장애 조치(Failover) 클러스터 인스턴스를 식별하는 데 사용되는 이름입니다.  
  
 **네트워크 설정** – 장애 조치(Failover) 클러스터 인스턴스의 IP 유형과 IP 주소를 지정합니다.  
  
 노드 추가 및 노드 제거 작업 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 대한 기존 IP 주소의 읽기 전용 목록이 표시됩니다.  
  
-   통합 설치:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터의 기존 노드에서 지원하는 것과 동일한 네트워크 서브넷 집합을 지원하는 노드를 추가하는 경우 IP 주소를 더 이상 추가할 수 없습니다. 종속성 설정은 변경되지 않고 그대로 유지됩니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터의 기존 노드에서 지원되는 서브넷의 하위 집합을 지원하는 노드를 추가하는 경우 IP 주소 리소스를 더 이상 추가할 수 없습니다. 지정된 모든 IP 주소가 모든 클러스터 노드에서 유효하지 않음을 나타내려면 IP 주소 리소스 종속성을 OR로 설정합니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터의 기존 노드에서 이미 지원되는 서브넷 이외의 서브넷을 지원하는 노드를 추가하는 경우 새로운 유효 IP 주소를 추가할 수 있습니다. 새 IP 주소를 지정하는 경우 지정된 모든 IP 주소가 모든 클러스터 노드에서 유효하지 않음을 나타내려면 IP 주소 리소스 종속성을 OR로 설정합니다.  
  
    -   추가 네트워크 서브넷은 지원하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터의 기존 노드에서 지원하는 서브넷은 지원하지 않는 노드를 추가하는 경우 IP 주소를 추가해야 합니다. 지정된 모든 IP 주소가 모든 클러스터 노드에서 유효하지 않음을 나타내려면 IP 주소 리소스 종속성을 OR로 설정합니다.  
  
-   고급 설치: 설치 완료 단계 중 모든 노드에 대 한 IP 주소 및 장애 조치 클러스터 인스턴스에 대 한 서브넷을 지정 합니다. 다중 서브넷 장애 조치(Failover) 클러스터에 대해 여러 IP 주소를 지정할 수 있지만 IP 주소는 서브넷별로 하나씩만 지원됩니다. 모든 준비된 노드는 하나 이상의 IP 주소에 대한 소유자여야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(Failover) 클러스터에 여러 서브넷이 있는 경우 IP 주소 리소스 종속성을 OR로 설정하라는 메시지가 표시됩니다. 노드 제거:  
  
    -   나머지 IP 주소가 모든 나머지 노드에서 지원되는 경우 IP 주소 리소스 종속성을 AND로 설정하라는 메시지가 표시됩니다.  
  
    -   나머지 IP 주소가 모든 나머지 노드에서 지원되지 않는 경우 IP 주소 리소스 종속성은 OR로 유지됩니다.  
  
  
