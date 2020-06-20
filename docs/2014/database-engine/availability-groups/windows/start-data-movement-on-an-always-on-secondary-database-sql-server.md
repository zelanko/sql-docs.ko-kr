---
title: AlwaysOn 보조 데이터베이스에서 데이터 이동 시작 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], databases
ms.assetid: 498eb3fb-6a43-434d-ad95-68a754232c45
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9b1ab796d9e48292dfa3426cd102faadecdabb2f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936374"
---
# <a name="start-data-movement-on-an-alwayson-secondary-database-sql-server"></a>AlwaysOn 보조 데이터베이스에서 데이터 이동 시작(SQL Server)
  이 항목에서는 AlwaysOn 가용성 그룹에 데이터베이스를 추가한 후 데이터 동기화를 시작하는 방법에 대해 설명합니다. 각 새로운 주 복제본에 대해 보조 복제본을 호스팅하는 서버 인스턴스에서 보조 데이터베이스를 준비해야 합니다. 그런 다음 이러한 각 보조 데이터베이스를 가용성 그룹에 수동으로 조인해야 합니다.  
  
> [!NOTE]  
>  가용성 그룹의 가용성 복제본을 호스팅하는 모든 서버 인스턴스에서 파일 경로가 동일한 경우 [새 가용성 그룹 마법사](use-the-availability-group-wizard-sql-server-management-studio.md), [가용성 그룹에 복제본 추가 마법사](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)또는 [가용성 그룹에 데이터베이스 추가 마법사](availability-group-add-database-to-group-wizard.md) 를 사용하여 데이터 동기화를 자동으로 시작할 수 있습니다.  
  
 데이터 동기화를 수동으로 시작하려면 가용성 그룹의 보조 복제본을 호스팅하는 각 서버 인스턴스에 차례로 연결하여 다음 단계를 완료해야 합니다.  
  
1.  각 주 데이터베이스와 해당 트랜잭션 로그의 현재 백업을 복원합니다(RESTORE WITH NORECOVERY 사용). 다음과 같은 다른 방법 중 하나를 사용할 수 있습니다.  
  
    -   RESTORE WITH NORECOVERY를 사용하여 주 데이터베이스의 최신 데이터베이스 백업을 수동으로 복원한 다음 RESTORE WITH NORECOVERY를 사용하여 각 후속 로그 백업을 복원합니다. 가용성 그룹의 보조 복제본을 호스팅하는 모든 서버 인스턴스에서 이 복원 시퀀스를 수행합니다.  
  
         **자세한 내용은 다음을 참조하세요.**  
  
         [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
    -   하나 이상의 로그 전달 주 데이터베이스를 가용성 그룹에 추가하는 경우 로그 전달에서 하나 이상의 해당 보조 데이터베이스를 AlwaysOn 가용성 그룹으로 마이그레이션할 수 있습니다. 로그 전달 보조 데이터베이스를 마이그레이션하려면 해당 데이터베이스가 주 데이터베이스와 동일한 이름을 사용하고 가용성 그룹에 대한 보조 복제본을 호스팅하는 서버 인스턴스에 있어야 합니다. 또한 주 복제본이 백업에 기본적으로 사용되고 백업 수행 대상이 되도록, 즉 백업 우선 순위가 0보다 크도록 가용성 그룹을 구성해야 합니다. 주 데이터베이스에서 백업 작업이 실행되고 나면 백업 작업을 사용하지 않도록 설정하고, 지정된 보조 데이터베이스에서 복원 작업이 실행되고 나면 복원 작업을 사용하지 않도록 설정해야 합니다.  
  
        > [!NOTE]  
        >  가용성 그룹에 대해 모든 보조 데이터베이스를 만든 후에는 보조 복제본에서 백업을 수행할 경우 가용성 그룹의 자동화된 백업 기본 설정을 다시 구성해야 합니다.  
  
         **자세한 내용은 다음을 참조하세요.**  
  
         [로그 전달에서 AlwaysOn 가용성 그룹 &#40;SQL Server로 마이그레이션하기 위한 필수 구성 요소&#41;](prereqs-migrating-log-shipping-to-always-on-availability-groups.md)  
  
         [가용성 복제본에 백업 구성&#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
2.  새로 준비된 각 보조 데이터베이스를 최대한 빨리 가용성 그룹에 조인합니다.  
  
     **자세한 내용은 다음을 참조하세요.**  
  
     [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
##  <a name="related-tasks"></a><a name="LaunchWiz"></a> 관련 작업  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 그룹에 복제본 추가 마법사 사용&#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [가용성 그룹에 데이터베이스 추가 마법사 사용&#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>참고 항목  
 [AlwaysOn 가용성 그룹 &#40;SQL Server 개요&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
