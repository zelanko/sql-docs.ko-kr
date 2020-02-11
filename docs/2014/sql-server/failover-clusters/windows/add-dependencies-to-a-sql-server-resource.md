---
title: SQL Server 리소스에 종속성 추가 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- resource dependencies [SQL Server]
- failover clustering [SQL Server], dependencies
- clusters [SQL Server], dependencies
- dependencies [SQL Server], clustering
ms.assetid: 25dbb751-139b-4c8e-ac62-3ec23110611f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a29577d6027c43fd35a8b27db8b402123c89a4b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63035674"
---
# <a name="add-dependencies-to-a-sql-server-resource"></a>SQL Server 리소스에 종속성 추가
  이 항목에서는 장애 조치(Failover) 클러스터 관리자 스냅인을 사용하여 AlwaysOn 장애 조치(Failover) 클러스터 인스턴스(FCI) 리소스에 종속성을 추가하는 방법에 대해 설명합니다. 장애 조치 클러스터 관리자 스냅인은 WSFC(Windows Server 장애 조치(failover) 클러스터링) 서비스용 클러스터 관리 애플리케이션입니다.  
  
-   **시작 하기 전 주의 사항:**  [제한](#Restrictions)사항, [필수 구성 요소](#Prerequisites)  
  
-   : [Windows 장애 조치(Failover) 클러스터 관리자](#WinClusManager) 를 **사용 하 여 SQL Server 리소스에 종속성을 추가 하려면**  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 그룹에 다른 리소스를 추가할 경우 해당 리소스에는 항상 고유한 SQL 네트워크 이름 리소스 및 고유한 SQL IP 주소 리소스가 있어야 합니다.  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]이외에는 기존의 SQL 네트워크 이름 리소스와 SQL IP 주소 리소스를 사용하지 마세요. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스를 다른 리소스와 공유하는 경우 다음 문제가 발생할 수 있습니다.  
  
-   예기치 않은 중단이 발생할 수 있습니다.  
  
-   서비스 팩 설치가 실패할 수 있습니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램이 실패할 수 있습니다. 이러한 문제가 발생할 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 추가 인스턴스를 설치하거나 일상적인 유지 관리를 수행할 수 없습니다.  
  
 다음과 같은 추가적인 문제를 고려하세요.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제에 FTP 사용: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제에 FTP를 사용하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 경우 FTP 서비스를 사용하도록 설정된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치할 때와 동일한 물리적 디스크 중 하나를 FTP 서비스에 사용해야 합니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스 종속성: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 그룹에 리소스를 추가하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 사용할 수 있도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스에 대한 종속성을 설정한 경우 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 리소스에 대한 종속성을 추가할 것을 권장합니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스에 대한 종속성을 추가하지 마세요. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 실행 중인 컴퓨터의 가용성을 계속 높은 상태로 유지하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 리소스가 실패하더라도 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 그룹에 영향을 주지 않도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에이전트 리소스를 구성합니다.  
  
-   파일 공유 및 프린터 리소스: 파일 공유 리소스나 프린터 클러스터 리소스를 설치하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 실행되는 컴퓨터와 동일한 물리적 디스크 리소스에 이 리소스를 배치하지 말아야 합니다. 이러한 리소스가 동일한 물리적 디스크 리소스에 추가되면 성능이 저하되거나 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행 중인 컴퓨터에 대한 서비스가 손실될 수 있습니다  
  
-   MS DTC 고려 사항: 운영 체제를 설치하고 FCI를 구성한 후 장애 조치(failover) 클러스터 관리자 스냅인을 사용하여 MS DTC( [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Distributed Transaction Coordinator)가 클러스터에서 작동하도록 구성해야 합니다. MS DTC 클러스터링에 실패해도 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치에는 문제가 없지만 MS DTC가 올바로 구성되지 않으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 애플리케이션 기능에 영향을 줄 수 있습니다.  
  
     
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 그룹에 MS DTC를 설치하고 MS DTC에 종속된 다른 리소스가 있을 경우 이 그룹이 오프라인 상태가 되거나 장애 조치(failover) 중인 경우 MS DTC를 사용할 수 없습니다. 
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 가능하면 MS DTC를 자체의 실제 디스크 리소스가 있는 해당 그룹에 추가하는 것이 좋습니다.  
  
###  <a name="Prerequisites"></a> 필수 조건  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 여러 개의 디스크 드라이브가 있는 WSFC 리소스 그룹에 설치하고 여러 드라이브 중 하나의 드라이브에 데이터를 저장하도록 선택하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스는 그 드라이브에만 종속되도록 설정됩니다. 다른 디스크에 데이터나 로그를 저장하려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스에 추가 디스크에 대한 종속성을 추가해야 합니다.  
  
##  <a name="WinClusManager"></a>장애 조치(Failover) 클러스터 관리자 스냅인 사용  
 **SQL Server 리소스에 종속성을 추가 하려면**  
  
-   장애 조치(failover) 클러스터 관리자 스냅인을 엽니다.  
  
-   종속시킬 적용 가능한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스가 있는 그룹을 찾습니다.  
  
-   디스크 리소스가 이미 이 그룹에 있는 경우 4단계로 이동합니다. 그렇지 않은 경우 디스크가 있는 그룹을 찾습니다. 이 그룹과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 있는 그룹을 동일한 노드에서 소유하지 않으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 그룹을 소유하는 노드로 디스크 리소스를 포함하는 그룹을 이동합니다.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스를 선택한 다음 **속성** 대화 상자를 열고 **종속성** 탭을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 종속성 집합에 디스크를 추가합니다.  
  
  
