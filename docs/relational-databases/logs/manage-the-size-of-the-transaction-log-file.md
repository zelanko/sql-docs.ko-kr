---
title: "트랜잭션 로그 파일 크기 관리 | Microsoft Docs"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction logs [SQL Server], size management
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 9076e3fbddd2af5459e4d8895ce969c61a4315ad
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="manage-the-size-of-the-transaction-log-file"></a>트랜잭션 로그 파일의 크기 관리
이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 트랜잭션 로그 크기 모니터링, 트랜잭션 로그 축소, 트랜잭션 로그 파일에 추가 또는 파일 확장, **tempdb** 트랜잭션 로그 증가율 최적화, 트랜잭션 로그 파일 증가 제어 등을 수행하는 방법에 대해 설명합니다.  

  ##  <a name="MonitorSpaceUse"></a> 로그 공간 사용 모니터링  
[DBCC SQLPERF(LOGSPACE)](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql)를 사용하여 로그 공간 사용을 모니터링합니다. 이 명령은 현재 사용된 로그 공간 크기에 대한 정보를 반환하고 트랜잭션 로그 잘림을 수행해야 하는 시기를 나타냅니다. 자세한 내용은 [DBCC SQLPERF Transact-SQL](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)을 참조하세요. 로그 파일의 현재 크기 및 최대 크기, 파일의 자동 증가 옵션에 대한 정보를 보기 위해 **sys.database_files**에서 해당 로그 파일의 **size**, **max_size** 및 **growth** 열을 사용할 수도 있습니다. 자세한 내용은 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)를 참조하세요.  
  
**중요!** 로그 디스크가 오버로드되지 않도록 하세요.  

  
##  <a name="ShrinkSize"></a> 로그 파일 크기 축소  
 실제 로그 파일의 크기를 줄이려면 로그 파일을 축소해야 합니다. 이는 트랜잭션 로그 파일에 사용되지 않은 공간이 포함되어 있는 경우에 유용합니다. 데이터베이스가 온라인 상태이고 하나 이상의 가상 로그 파일에 여유 공간이 있는 경우에만 로그 파일을 축소할 수 있습니다. 경우에 따라 다음에 로그가 잘릴 때까지 로그를 축소하지 못할 수도 있습니다.  
  
> [!NOTE]
>  장기 실행 트랜잭션과 같이 오랜 시간 동안 가상 로그 파일을 활성 상태로 유지하는 요소가 있으면 로그 축소가 제한되거나 로그를 전혀 축소하지 못할 수 있습니다. 로그 잘림을 지연시킬 수 있는 요소에 대한 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)를 참조하세요.  
  
 로그 파일을 축소하면 논리 로그 부분이 포함되지 않은 하나 이상의 가상 로그 파일( *비활성 가상 로그 파일*)이 제거됩니다. 트랜잭션 로그 파일을 축소하면 비활성 가상 로그 파일이 로그 파일의 끝에서 제거되어 로그가 대략적인 대상 크기로 줍니다.  
  
 **로그 파일 축소(데이터베이스 파일의 축소 없이)**  
  
-   [DBCC SHRINKFILE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
  
-   [파일 축소](../../relational-databases/databases/shrink-a-file.md)  
  
 **로그 파일 축소 이벤트 모니터링**  
  
-   [Log File Auto Shrink Event Class](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md)입니다.  
  
 **로그 공간 모니터링**  
  
-   [DBCC SQLPERF&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)  
  
-   [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)(로그 파일 또는 파일의 **size**, **max_size** 및 **growth** 열 참조)  
  
> [!NOTE]
>  로그 파일이 자동으로 축소되도록 설정할 수 있습니다. 그러나 자동 축소는 사용하지 않는 것이 좋으며 **autoshrink** 데이터베이스 속성도 기본적으로 FALSE로 설정됩니다. **autoshrink** 를 TRUE로 설정하면 파일 공간의 25% 이상이 사용되지 않을 때만 자동 축소에 의해 파일 크기가 줄어듭니다. 파일은 파일의 25%만 사용되지 않을 때의 크기 또는 파일의 원래 크기 중 더 큰 크기로 축소됩니다. **자동 축소** 속성의 설정을 변경하는 방법은 **옵션** 페이지의 **자동 축소** 속성을 사용하는 [데이터베이스의 속성 보기 또는 변경](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md) 또는 AUTO_SHRINK 옵션을 사용하는 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.  
  

##  <a name="AddOrEnlarge"></a> 로그 파일 추가 또는 확장  
 디스크 공간이 충분한 경우 기존의 로그 파일을 확장하거나 일반적으로 다른 디스크에 있는 데이터베이스에 로그 파일을 추가하여 공간을 확보할 수 있습니다.  
  
-   데이터베이스에 로그 파일을 추가하려면 ALTER DATABASE 문의 ADD LOG FILE 절을 사용합니다. 로그 파일을 추가하면 로그가 확장될 수 있습니다.  
  
-   로그 파일을 확장하려면 SIZE 및 MAXSIZE 구문을 지정하여 ALTER DATABASE 문의 MODIFY FILE 절을 사용합니다. 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
    
  
##  <a name="tempdbOptimize"></a> tempdb 트랜잭션 로그 크기 최적화  
 서버 인스턴스를 다시 시작하면 **tempdb** 데이터베이스의 트랜잭션 로그가 자동 증가 이전의 원래 크기로 다시 조정됩니다. 이 경우 **tempdb** 트랜잭션 로그의 성능이 저하될 수 있습니다. 서버 인스턴스를 시작하거나 다시 시작한 후에 **tempdb** 트랜잭션 로그의 크기를 늘려 이 오버헤드를 방지할 수 있습니다. 자세한 내용은 [tempdb Database](../../relational-databases/databases/tempdb-database.md)을(를) 참조하세요.  
  
  
##  <a name="ControlGrowth"></a> 트랜잭션 로그 파일 증가 제어  
 [ALTER DATABASE(Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md) 문을 사용하여 트랜잭션 로그 파일의 증가를 관리합니다. 다음에 유의하세요.  
  
-   현재 파일의 크기(KB, MB, GB 및 TB 단위)를 변경하려면 SIZE 옵션을 사용합니다.  
  -   증분을 변경하려면 FILEGROWTH 옵션을 사용합니다. 값 0은 자동 증가를 사용하지 않고 추가 공간을 허용하지 않음을 나타냅니다. 로그 파일의 자동 증가분이 적어도 성능이 저하될 수 있습니다. 로그 파일의 파일 증가분이 충분히 커야 자주 확장하는 번거로움을 피할 수 있습니다. 대개 기본 증가분인 10%가 알맞습니다.  

로그 파일의 파일 증가 속성을 변경하는 방법은 [ALTER DATABASE(TRANSACT-SQL)](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
-   로그 파일의 최대 크기(KB, MB, GB 및 TB 단위)를 제어하거나 증가를 UNLIMITED로 설정하려면 MAXSIZE 옵션을 사용합니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP(Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [꽉 찬 트랜잭션 로그 문제 해결(SQL Server 오류 9002)](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
  

