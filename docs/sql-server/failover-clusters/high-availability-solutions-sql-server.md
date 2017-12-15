---
title: "고가용성 솔루션(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 05/19/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: failover-clusters
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- high availability [SQL Server], solutions
- Database Engine [SQL Server], availability
- database availability [SQL Server]
- availability [SQL Server]
- server availability [SQL Server]
ms.assetid: b2eda634-0f8e-4703-801b-7ba895544ff5
caps.latest.revision: "84"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 7af2a4035d3c528189cca77a4506e98db1acd93c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="high-availability-solutions-sql-server"></a>고가용성 솔루션(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 서버나 데이터베이스의 가용성을 개선하는 여러 가지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고가용성 솔루션을 소개합니다. 고가용성 솔루션은 하드웨어 또는 소프트웨어 오류의 영향을 차단하고 응용 프로그램의 가용성을 유지하여 사용자가 인지하는 작동 중단을 최소화합니다.    
    
   
>  **참고!** 지정된 고가용성 솔루션을 지원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 대한 자세한 내용은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)의 "고가용성(Always On)" 섹션을 참조하세요.    
     
    
##  <a name="TermsAndDefinitions"></a> SQL Server 고가용성 솔루션 개요    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 서버 또는 데이터베이스의 고가용성 유지를 위한 여러 가지 옵션을 제공합니다. 고가용성 옵션에는 다음이 포함됩니다.    
    
*  Always On 장애 조치(failover) 클러스터 인스턴스    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Always On 제공을 위해 Always On 장애 조치(failover) 클러스터 인스턴스는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 기능을 사용하여 FCI( *장애 조치(failover) 클러스터 인스턴스* )라고 부르는 서버 인스턴스 수준의 중복성을 통해 로컬 고가용성을 제공합니다. FCI는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 노드 및 다중 서브넷 간에 설치되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 단일 인스턴스입니다. 네트워크에서 FCI는 단일 컴퓨터에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스처럼 보이지만 현재 노드를 사용할 수 없을 경우 FCI가 하나의 WSFC 노드에서 다른 노드로 장애 조치(failover) 기능을 제공합니다.    
    
 자세한 내용은 [Always On 장애 조치(failover) 클러스터 인스턴스&#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)인스턴스를 호스팅하는 장애 조치 클러스터형 인스턴스로 구성됩니다.    
    
*  [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]    
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 은 하나 이상의 사용자 데이터베이스에 대한 가용성을 최대화할 수 있도록 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 에 도입된 엔터프라이즈 수준의 고가용성 및 재해 복구 솔루션입니다. [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 을 사용하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 WSFC(Windows Server 장애 조치(failover) 클러스터링) 노드에 있어야 합니다. 자세한 내용은 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)을 참조하세요.    
    
  
>  **참고!** FCI는 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 을 활용하여 데이터베이스 수준에서 원격 재해 복구 기능을 제공할 수 있습니다. 자세한 내용은 [장애 조치(failover) 클러스터링 및 Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)을 참조하세요.    
    
*  데이터베이스 미러링. **참고!** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 를 사용하는 것이 좋습니다.     
데이터베이스 미러링은 즉석 장애 조치(failover)를 지원함으로써 데이터베이스 가용성을 높여 주는 솔루션입니다. 데이터베이스 미러링을 사용하여 *주 데이터베이스*라는 해당 프로덕션 데이터베이스에 대해 하나의 대기 데이터베이스, 즉 *미러 데이터베이스*를 유지 관리할 수 있습니다. 자세한 내용은 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.    
    
*  로그 전달    
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 및 데이터베이스 미러링과 마찬가지로 로그 전달은 데이터베이스 수준에서 작동합니다. 로그 전달을 사용하여 *주 데이터베이스*라고 하는 단일 프로덕션 데이터베이스에 대한 웜 대기 데이터베이스(*보조 데이터베이스*라고도 함)를 한 개 이상 유지 관리할 수 있습니다. 로그 전달에 대한 자세한 내용은 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)를 참조하세요.    
    
##  <a name="RecommendedSolutions"></a> SQL Server를 사용하여 데이터를 보호하기 위한 권장 솔루션    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경에 데이터 보호 기능을 제공하기 위한 권장 사항은 다음과 같습니다.    
    
-   타사 SAN(공유 디스크 솔루션)을 통해 데이터를 보호하기 위해서는 Always On 장애 조치(failover) 클러스터 인스턴스를 사용하는 것이 좋습니다.    
    
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 통한 데이터 보호를 위해서는 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]을 사용하는 것이 좋습니다.    
    
       >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 지원하지 않는 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]버전을 실행 중인 경우 로그 전달을 사용하는 것이 좋습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 지원하는 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]버전에 대한 자세한 내용은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)의 "고가용성(Always On)" 섹션을 참조하세요.    
    
## <a name="see-also"></a>참고 항목    
 [SQL Server의 WSFC&#40;Windows Server 장애 조치(failover) 클러스터링&#41;](../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)     
 [데이터베이스 미러링: 상호 운용성 및 공존성&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-interoperability-and-coexistence-sql-server.md)     
 [SQL Server 2016에서 사용되지 않는 데이터베이스 엔진 기능](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)    
    
  

