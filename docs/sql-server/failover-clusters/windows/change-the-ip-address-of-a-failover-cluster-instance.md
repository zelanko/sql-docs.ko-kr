---
title: "장애 조치(failover) 클러스터 인스턴스의 IP 주소 변경 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: failover-clusters
ms.prod_service: sql-non-specified
ms.service: database-engine
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying IP addresses
- failover clustering [SQL Server], IP addresses
- IP addresses [SQL Server]
- clusters [SQL Server], IP addresses
ms.assetid: b685f400-cbfe-4c5d-a070-227a1123dae4
caps.latest.revision: "33"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: afe88cc13f4edb8b32644946c60f844101797f06
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="change-the-ip-address-of-a-failover-cluster-instance"></a>장애 조치(failover) 클러스터 인스턴스의 IP 주소 변경
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 장애 조치(failover) 클러스터 관리자 스냅인을 사용하여 Always On 장애 조치(failover) 클러스터 인스턴스(FCI)에 IP 주소 리소스를 변경하는 방법에 대해 설명합니다. 장애 조치 클러스터 관리자 스냅인은 WSFC(Windows Server 장애 조치(failover) 클러스터링) 서비스용 클러스터 관리 응용 프로그램입니다.  
  
-   **시작하기 전 주의 사항:**  [보안](#Security)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 시작하기 전에 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 [장애 조치(failover) 클러스터링을 설치하기 전에](../../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)항목을 검토하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 FCI를 유지 관리 또는 업데이트하려면 FCI의 모든 노드 서비스로 로그온할 수 있는 권한을 가진 로컬 관리자여야 합니다.  
  
##  <a name="WSFC"></a> 장애 조치(Failover) 클러스터 관리자 스냅인 사용  
 **FCI용 IP 주소 리소스를 변경하려면**  
  
1.  장애 조치(failover) 클러스터 관리자 스냅인을 엽니다.  
  
2.  왼쪽 창에서 **서비스 및 응용 프로그램** 노드를 확장하고 FCI를 클릭합니다.  
  
3.  **서버 이름** 범주 아래의 오른쪽 창에서 SQL Server 인스턴스를 마우스 오른쪽 단추로 클릭하고 **속성** 옵션을 선택하여 **속성** 대화 상자를 엽니다.  
  
4.  **일반** 탭에서 IP 주소 리소스를 변경합니다.  
  
5.  **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
6.  오른쪽 창에서 SQL IP Address1(장애 조치(failover) 클러스터 인스턴스 이름)을 마우스 오른쪽 단추로 클릭하고 **오프라인 상태로 만들기**를 선택합니다. SQL IP Address1(장애 조치(Failover) 클러스터 인스턴스 이름), SQL 네트워크 이름(장애 조치(Failover) 클러스터 인스턴스 이름) 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 상태가 온라인에서 오프라인 보류 중으로 바뀐 다음 오프라인으로 바뀌는 것을 볼 수 있습니다.  
  
7.  오른쪽 창에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 마우스 오른쪽 단추로 클릭하고 **온라인 상태로 만들기**를 선택합니다. SQL IP Address1(장애 조치(Failover) 클러스터 인스턴스 이름), SQL 네트워크 이름(장애 조치(Failover) 클러스터 인스턴스 이름) 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 상태가 오프라인에서 온라인 보류 중으로 바뀐 다음 온라인으로 바뀌는 것을 볼 수 있습니다.  
  
8.  장애 조치(failover) 클러스터 관리자 스냅인을 닫습니다.  
  
  
