---
title: 로그 전달을 가용성 그룹으로 변환하기 위한 필수 구성 요소
description: 로그 전달을 Always On 가용성 그룹으로 변환하는 데 필요한 필수 구성 요소에 대한 설명입니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 2738ce65-205e-4682-92d8-dc7e37c58b2b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 73cd348f9cb1f22eca30c28cee97ce8e81a20b16
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68014508"
---
# <a name="prerequisites-to-convert-log-shipping-to-always-on-availability-groups"></a>로그 전달을 Always On 가용성 그룹으로 변환하기 위한 필수 구성 요소
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 하나 이상의 보조 데이터베이스와 함께 로그 전달 주 데이터베이스를 Always On 주 데이터베이스 및 보조 데이터베이스로 변환하기 위한 필수 조건에 대해 설명합니다.  
  
> [!NOTE]  
>  가용성 그룹에서 읽기 가능한 주 데이터베이스 또는 보조 데이터베이스를 로그 전달 주 데이터베이스로 구성할 수 있습니다.  
  
  
##  <a name="AGPrereqsRealAddress"></a> 가용성 그룹 사전 요구 사항  
 가용성 그룹의 주 복제본에서 백업 작업이 실행되도록 허용하려면 다음 Always On 가용성 그룹 백업 설정을 사용합니다.  
  
|속성|설정|  
|--------------|-------------|  
|가용성 그룹의 자동화된 백업 기본 설정|주 복제본에만|  
|주 복제본의 백업 우선 순위|>0|  
  
 **자세한 내용은 다음을 참조하세요.**  
  
 [가용성 그룹 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
 [가용성 복제본에 백업 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="LogShipPrereqs"></a> 로그 전달 사전 요구 사항  
  
-   로그 전달 주 데이터베이스가 가용성 그룹의 초기/현재 주 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 있어야 합니다.  
  
-   Always On 보조 데이터베이스로 변환할 지정된 로그 전달 보조 데이터베이스는 다음 조건을 충족해야 합니다.  
  
    -   주 데이터베이스와 동일한 이름을 사용합니다.  
  
    -   가용성 그룹에 대한 보조 복제본을 호스팅하는 서버 인스턴스에 있습니다.  
  
 주 데이터베이스에서 백업 작업이 실행되고 나면 백업 작업을 사용하지 않도록 설정하고, 지정된 보조 데이터베이스에서 복원 작업이 실행되고 나면 복원 작업을 사용하지 않도록 설정하십시오.  
  
 가용성 그룹에 대해 모든 보조 데이터베이스를 만든 후에는 보조 복제본에서 백업을 수행할 경우 가용성 그룹의 자동화된 백업 기본 설정을 다시 구성해야 합니다.  
  
 **자세한 내용은 다음을 참조하세요.**  
  
 [로그 전달 구성을 가용성 그룹으로 변환](https://blogs.msdn.microsoft.com/sqlalwayson/2012/01/09/converting-a-logshipping-configuration-to-availability-group/)(SQL Server 블로그)  
  
##  <a name="RelatedTasks"></a> 관련 작업  
 **로그 전달**  
  
-   [SQL Server 2016으로 로그 전달 업그레이드&#40;Transact-SQL&#41;](../../../database-engine/log-shipping/upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [로그 전달 제거&#40;SQL Server&#41;](../../../database-engine/log-shipping/remove-log-shipping-sql-server.md)  
  
 **Always On 가용성 그룹**  
  
-   [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 그룹 만들기&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [가용성 그룹 만들기&#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)  
  
-   [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [가용성 복제본에 백업 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   **블로그:**  
  
     [로그 전달 구성을 가용성 그룹으로 변환](https://blogs.msdn.microsoft.com/sqlalwayson/2012/01/09/converting-a-logshipping-configuration-to-availability-group/)  
  
     [기존 가용성 그룹에 로그 전달 주 데이터베이스 및 보조 데이터베이스 추가](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/01/add-a-log-shipping-primary-database-and-secondary-databases-to-an-existing-availability-group/)  
  
     [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server 엔지니어 블로그](https://blogs.msdn.com/b/psssql/)  
  
-   **백서:**  
  
     [마이그레이션 가이드: 데이터베이스 미러링 및 로그 전달을 조합하는 이전 배포에서 Always On 가용성 그룹으로 마이그레이션](https://msdn.microsoft.com/library/jj635217)  
  
     [SQL Server 2012에 대한 Microsoft 백서](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 고객 자문 팀 백서](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 정보&#40;SQL Server&#41;](../../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 모니터링&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
  
