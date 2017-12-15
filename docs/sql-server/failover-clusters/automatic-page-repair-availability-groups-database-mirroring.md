---
title: "자동 페이지 복구(가용성 그룹: 데이터베이스 미러링) | Microsoft 문서"
ms.custom: 
ms.date: 05/17/2016
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
- automatic page repair
- Availability Groups [SQL Server], automatic page repair
- database mirroring [SQL Server], automatic page repair
- suspect pages [SQL Server]
ms.assetid: cf2e3650-5fac-4f34-b50e-d17765578a8e
caps.latest.revision: "31"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b1f5007a8c6b8f222d0708692ecc802f6409738d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="automatic-page-repair-availability-groups-database-mirroring"></a>자동 페이지 복구(가용성 그룹: 데이터베이스 미러링)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 자동 페이지 복구는 데이터베이스 미러링과 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]에서 지원됩니다. 특정 유형의 오류로 인해 페이지가 손상되어 읽을 수 없게 되면 데이터베이스 미러링 파트너(주 파트너 또는 미러 파트너) 또는 가용성 복제본(주 복제본 또는 보조 복제본)이 자동으로 페이지를 복구하려고 시도합니다. 페이지를 읽을 수 없는 파트너 또는 복제본은 해당 파트너나 다른 복제본에 페이지의 새 복사본을 요청합니다. 이 요청이 성공하면 읽을 수 없는 페이지는 읽을 수 있는 복사본으로 대체되고 일반적으로 오류가 해결됩니다.  
  
 일반적으로 데이터베이스 미러링과 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 은 동일한 방식으로 I/O 오류를 처리합니다. 여기에서 몇 가지 차이점을 명시적으로 소개합니다.  
  
> [!NOTE]  
>  자동 페이지 복구는 DBCC 복구와 다릅니다. 이 경우 모든 데이터가 유지됩니다. 반대로 DBCC REPAIR_ALLOW_DATA_LOSS 옵션을 사용하여 오류를 수정하는 경우에는 일부 페이지 및 데이터가 삭제될 수 있습니다.  
  
-   [자동 페이지 복구 시도가 발생하는 오류 유형](#ErrorTypes)  
  
-   [자동으로 복구될 수 없는 페이지 유형](#UnrepairablePageTypes)  
  
-   [주/기본 데이터베이스에서 I/O 오류 처리](#PrimaryIOErrors)  
  
-   [미러/보조 데이터베이스에서 I/O 오류 처리](#SecondaryIOErrors)  
  
-   [개발자를 위한 최선의 구현 방법](#DevBP)  
  
-   [방법: 자동 페이지 복구 시도 보기](#ViewAPRattempts)  
  
##  <a name="ErrorTypes"></a> Error Types That Cause an Automatic Page-Repair Attempt  
 데이터베이스 미러링 자동 페이지 복구는 다음 표에 나열된 오류 중 하나로 인해 실패한 작업이 있는 데이터 파일의 페이지만 복구하도록 시도합니다.  
  
|오류 번호|설명|자동 페이지 복구 시도가 발생되는 인스턴스|  
|------------------|-----------------|---------------------------------------------------------|  
|823|운영 체제가 데이터에서 실패한 CRC(순환 중복 검사)를 수행한 경우에만 동작이 수행됩니다.|ERROR_CRC이며 이 오류에 대한 운영 체제 값은 23입니다.|  
|824|논리 오류입니다.|조각난 쓰기 오류 또는 잘못된 페이지 체크섬과 같은 논리적 데이터 오류입니다.|  
|829|페이지가 복원 보류로 표시되었습니다.|모두|  
  
 최근에 발생한 823 CRC 오류 및 824 오류를 보려면 [msdb](../../relational-databases/system-tables/suspect-pages-transact-sql.md) 데이터베이스의 [suspect_pages](../../relational-databases/databases/msdb-database.md) 테이블을 참조하세요.  

  
##  <a name="UnrepairablePageTypes"></a> Page Types That Cannot Be Automatically Repaired  
 다음 컨트롤 페이지 유형은 자동 페이지 복구를 통해 복구할 수 없습니다.  
  
-   파일 헤더 페이지(페이지 ID 0)  
  
-   9페이지(데이터베이스 부트 페이지)  
  
-   할당 페이지: GAM(전역 할당 맵) 페이지, SGAM(공유 전역 할당 맵) 페이지 및 PFS(페이지 여유 공간) 페이지.  
  
 
##  <a name="PrimaryIOErrors"></a> Handling I/O Errors on the Principal/Primary Database  
 주/기본 데이터베이스에서는 데이터베이스가 SYNCHRONIZED 상태이고 주/기본 데이터베이스가 미러/보조 데이터베이스에 대한 로그 레코드를 계속 보내는 경우에만 자동 페이지 복구가 시도됩니다. 자동 페이지 복구 시도에서 기본적인 동작 시퀀스는 다음과 같습니다.  
  
1.  주/기본 데이터베이스의 데이터 페이지에서 읽기 오류가 발생하면 주/기본 데이터베이스는 해당 오류 상태와 함께 [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) 테이블에 행을 삽입합니다. 그런 다음 데이터베이스 미러링의 경우에는 주 데이터베이스가 미러 데이터베이스에 해당 페이지의 복사본을 요청합니다. [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]의 경우에는 주 데이터베이스가 해당 요청을 모든 보조 데이터베이스에 브로드캐스팅하고 응답할 첫 번째 데이터베이스에서 페이지를 가져옵니다. 이 요청에는 페이지 ID와 현재 플러시된 로그 끝에 있는 LSN이 지정됩니다. 페이지가 *복원 보류*로 표시되므로 자동 페이지 복구 시도 중에는 액세스할 수 없습니다. 복구 시도 중에 이 페이지에 액세스하려고 하면 오류 829(복원 보류)가 발생하며 실패합니다.  
  
2.  페이지 요청을 받으면 미러/보조 데이터베이스는 요청에 지정된 LSN까지 로그를 다시 수행할 때까지 대기합니다. 그런 다음 미러/보조 데이터베이스는 데이터베이스의 해당 복사본에 있는 페이지에 액세스하려고 시도합니다. 페이지에 액세스할 수 있는 경우 미러/보조 데이터베이스는 해당 페이지의 복사본을 주/기본 데이터베이스로 보냅니다. 액세스할 수 없는 경우 미러/보조 데이터베이스는 주/기본 데이터베이스로 오류를 반환하고 자동 페이지 복구 시도가 실패합니다.  
  
3.  주/기본 데이터베이스는 해당 페이지의 새 복사본이 포함된 응답을 처리합니다.  
  
4.  자동 페이지 복구 시도로 주의 대상 페이지가 수정되면 해당 페이지는 **suspect_pages** 테이블에 복원된 것으로(**event_type** = 5) 표시됩니다.  
  
5.  페이지 I/O 오류로 인해 [지연된 트랜잭션](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)이 발생한 경우 페이지를 복구하고 나면 주/기본 데이터베이스에서 이러한 트랜잭션을 해결하려고 시도합니다.  
  
 
##  <a name="SecondaryIOErrors"></a> Handling I/O Errors on the Mirror/Secondary Database  
 미러/보조 데이터베이스에서 발생하는 데이터 페이지에 대한 I/O 오류는 일반적으로 데이터베이스 미러링 및 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]에서와 동일한 방식으로 처리됩니다.  
  
1.  데이터베이스 미러링을 사용하는 경우 로그 레코드를 다시 실행할 때 미러 데이터베이스에 하나 이상의 페이지 I/O 오류가 발생한 경우 미러링 세션은 SUSPENDED 상태가 됩니다. [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]을 사용하는 경우 로그 레코드를 다시 실행할 때 보조 복제본에 하나 이상의 페이지 I/O 오류가 발생한 경우 보조 데이터베이스는 SUSPENDED 상태가 됩니다. 이때 미러/보조 데이터베이스는 해당 오류 상태와 함께 **suspect_pages** 테이블에 행을 삽입합니다. 그런 다음 미러/보조 데이터베이스는 주/기본 데이터베이스에 해당 페이지의 복사본을 요청합니다.  
  
2.  주/기본 데이터베이스는 데이터베이스의 해당 복사본에 있는 페이지에 액세스하려고 시도합니다. 페이지에 액세스할 수 있는 경우 주/기본 데이터베이스는 해당 페이지의 복사본을 미러/보조 데이터베이스로 보냅니다.  
  
3.  미러/보조 데이터베이스가 요청한 모든 페이지의 복사본을 받을 경우 미러/보조 데이터베이스는 미러링 세션을 다시 시작합니다. 자동 페이지 복구 시도로 주의 대상 페이지가 수정되면 해당 페이지는 **suspect_pages** 테이블에 복원된 것으로(**event_type** = 4) 표시됩니다.  
  
     미러/보조 데이터베이스가 요청한 페이지를 주/기본 데이터베이스로부터 받지 못할 경우 자동 페이지 복구 시도가 실패합니다. 데이터베이스 미러링을 사용하는 경우 미러링 세션은 일시 중단된 상태로 남게 됩니다. [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]을 사용하는 경우에는 보조 데이터베이스가 일시 중단된 상태로 남게 됩니다 미러링 세션 또는 보조 데이터베이스를 수동으로 다시 시작하는 경우 손상된 페이지는 동기화 단계 중에 다시 나타납니다.  
  
 
##  <a name="DevBP"></a> Developer Best Practice  
 자동 페이지 복구는 백그라운드로 실행되는 비동기 프로세스입니다. 따라서 읽을 수 없는 페이지를 요청하는 데이터베이스 작업은 실패하게 되고 오류를 일으킨 조건과 상관없이 오류 코드가 반환됩니다. 미러된 데이터베이스 또는 가용성 데이터베이스에 대한 응용 프로그램을 개발하는 경우 실패한 작업에 대한 예외를 차단해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 코드가 823, 824 또는 829인 경우 작업을 나중에 다시 시도해야 합니다.  
  

##  <a name="ViewAPRattempts"></a> How To: View Automatic Page-Repair Attempts  
 다음 동적 관리 뷰는 지정된 가용성 데이터베이스 또는 미러된 데이터베이스에 대한 최근 자동 페이지 복구 시도에 해당하는 행을 데이터베이스당 최대 100개까지 반환합니다.  
  
-   **Always On 가용성 그룹:**  
  
     [sys.dm_hadr_auto_page_repair&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-auto-page-repair-transact-sql.md)  
  
     서버 인스턴스가 모든 가용성 그룹에 대해 호스팅하는 가용성 복제본의 모든 가용성 데이터베이스에 대해 수행하는 자동 페이지 복구 시도당 한 개의 행을 반환합니다.  
  
-   **데이터베이스 미러링:**  
  
     [sys.dm_db_mirroring_auto_page_repair&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-auto-page-repair.md)  
  
     서버 인스턴스의 미러된 데이터베이스에 대한 각 자동 페이지 복구 시도당 하나의 행을 반환합니다.  
  
 
## <a name="see-also"></a>참고 항목  
 [suspect_pages 테이블 관리&#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  


