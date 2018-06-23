---
title: 장애 조치(failover) 클러스터 인스턴스 관리 및 유지 관리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- user accounts [SQL Server], failover clustering
- clusters [SQL Server], maintaining
- nodes [Faillover Clustering]
- failover clustering [SQL Server], maintaining
- adding nodes
- virtual servers [SQL Server], removing nodes
- clustered instance of SQL Server
- nodes [Faillover Clustering], removing
- nodes [Faillover Clustering], adding
- service accounts [SQL Server]
- removing nodes
- virtual servers [SQL Server], adding nodes
ms.assetid: 2d5c63e9-8061-45c3-94db-8dd3100b8a91
caps.latest.revision: 34
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 3c5364ad63b446abc4e79e0d3ac986f86e8432a3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184628"
---
# <a name="failover-cluster-instance-administration-and-maintenance"></a>장애 조치(failover) 클러스터 인스턴스 관리 및 유지 관리
  사용 하 여 노드 추가 또는 제거에서 기존 AlwaysOn 장애 조치 클러스터 인스턴스 (FCI) 등의 유지 관리 작업 수행은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램. IP 주소 리소스 변경, 특정 FCI 시나리오 복구 등과 같은 다른 관리 태스크는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 서비스용 관리 스냅인인 장애 조치(Failover) 클러스터 관리자 스냅인을 사용하여 수행합니다.  
  
## <a name="maintaining-a-failover-cluster-instance"></a>장애 조치(Failover) 클러스터 인스턴스 유지 관리  
 FCI는 설치한 후에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 사용하여 변경하거나 복구할 수 있습니다. 예를 들어 FCI에 노드를 더 추가하거나 FCI를 독립 실행형 인스턴스로 실행하거나 FCI 구성에서 노드를 제거할 수 있습니다.  
  
### <a name="adding-a-node-to-an-existing-failover-cluster-instance"></a>기존 장애 조치 클러스터 인스턴스에 노드 추가  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램에서 기존 FCI의 유지 관리 옵션이 제공됩니다. 이 옵션을 선택하면 FCI를 추가하려는 컴퓨터에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하여 FCI에 다른 노드를 추가할 수 있습니다. 자세한 내용은 [새 SQL Server 장애 조치(failover) 클러스터 만들기&#40;설치&#41;](../install/create-a-new-sql-server-failover-cluster-setup.md) 및 [SQL Server 장애 조치(Failover) 클러스터에서 노드 추가 또는 제거&#40;설치&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)를 참조하세요.  
  
### <a name="removing-a-node-from-an-existing-failover-cluster-instance"></a>기존 장애 조치 클러스터 인스턴스에서 노드 제거  
 FCI에서 제거하려는 컴퓨터에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하여 FCI에서 노드를 제거할 수 있습니다. FCI의 각 노드는 FCI의 다른 노드에 대한 종속성이 없는 피어로 간주되므로 노드를 제거할 수 있습니다. 손상된 노드를 반드시 제거할 수 있어야 하는 것은 아니며 제거 프로세스에서는 사용할 수 없는 노드에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이진 파일을 제거하지 않습니다. 제거된 노드는 언제든지 FCI로 다시 추가할 수 있습니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)을 참조하세요.  
  
### <a name="changing-service-accounts"></a>서비스 계정 변경  
 FCI 노드가 다운되거나 오프라인일 때는 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정의 암호를 변경하지 말아야 합니다. 변경해야 할 경우 모든 노드가 다시 온라인 상태로 전환되면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 암호를 다시 설정해야 합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 서비스 계정이 클러스터의 관리자가 아니면 클러스터의 모든 노드에서 관리자 공유를 삭제할 수 없습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가 제대로 작동하려면 클러스터에서 관리자 공유를 사용할 수 있어야 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정과 WSFC 서비스 계정에 같은 계정을 사용하지 마십시오. WSFC 서비스 계정의 암호를 변경하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 설치할 수 없습니다.  
  
 [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)]에서 서비스 SID는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정에 사용됩니다. 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)를 참조하세요.  
  
## <a name="administering-a-failover-cluster-instance"></a>장애 조치(Failover) 클러스터 인스턴스 관리  
  
|태스크 설명|항목 링크|  
|----------------------|----------------|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스에 종속성을 추가하는 방법에 대해 설명합니다.|[SQL Server 리소스에 종속성 추가](add-dependencies-to-a-sql-server-resource.md)|  
|Kerberos는 클라이언트/서버 응용 프로그램을 위한 강력한 인증을 제공하기 위해 디자인된 네트워크 인증 프로토콜입니다. Kerberos는 상호 운용성의 기반을 제공하고 기업 전체의 네트워크 인증 보안을 강화합니다. Kerberos 인증을 사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 독립 실행형 인스턴스 또는 AlwaysOn Fci 합니다.|[Kerberos 연결의 서비스 사용자 이름 등록](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).|  
|Kerberos 인증을 사용하는 방법을 설명하는 콘텐츠에 대한 링크를 제공합니다.||  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 오류를 복구하는 데 사용되는 프로시저에 대해 설명합니다.|[장애 조치(failover) 클러스터 인스턴스 오류 복구](recover-from-failover-cluster-instance-failure.md)|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스에 대한 IP 주소 리소스를 변경하는 데 사용되는 프로시저에 대해 설명합니다.|[장애 조치(failover) 클러스터 인스턴스의 IP 주소 변경](change-the-ip-address-of-a-failover-cluster-instance.md)|  
  
## <a name="see-also"></a>관련 항목  
 [HealthCheckTimeout 속성 설정 구성](configure-healthchecktimeout-property-settings.md)   
 [FailureConditionLevel 속성 설정 구성](configure-failureconditionlevel-property-settings.md)   
 [장애 조치(failover) 클러스터 인스턴스 진단 로그 보기 및 읽기](view-and-read-failover-cluster-instance-diagnostics-log.md)  
  
  