---
title: 부분 백업(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- partial backups [SQL Server]
- READ_WRITE_FILEGROUPS option
- database backups [SQL Server], about backing up databases
ms.assetid: fe6b6bb1-38d0-46c4-bab8-31df14e8999c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a2c265d3a373eb53b822142fa2955d07b96b88f2
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68033664"
---
# <a name="partial-backups-sql-server"></a>부분 백업(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복구 모델은 부분 백업을 지원하므로 이 항목에서는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 관련된 내용을 다룹니다. 그러나 부분 백업은 하나 이상의 읽기 전용 파일 그룹을 포함하는 초대형 데이터베이스를 백업할 경우의 유연성 향상을 위해 단순 복구 모델에서 사용하도록 디자인되었습니다.  
  
 부분 백업은 읽기 전용 파일 그룹을 제외할 때마다 유용하게 사용할 수 있습니다. *부분 백업* 은 전체 데이터베이스 백업과 유사하지만 부분 백업에 모든 파일 그룹이 포함되지는 않습니다. 대신 읽기/쓰기 데이터베이스의 경우 부분 백업은 주 파일 그룹, 모든 읽기/쓰기 파일 그룹, 하나 이상의 읽기 전용 파일(선택 사항)의 데이터를 포함합니다. 읽기 전용 데이터베이스의 부분 백업에는 주 파일 그룹만 포함됩니다.  
  
> [!NOTE]  
>  부분 백업 후 읽기 전용 데이터베이스를 읽기/쓰기로 변경하는 경우 부분 백업에는 없는 읽기/쓰기 보조 파일 그룹이 있을 수 있습니다. 이 경우 차등 부분 백업을 시도하면 백업이 실패하며 다른 부분 백업을 수행해야만 데이터베이스의 차등 부분 백업을 만들 수 있습니다. 새 부분 백업은 모든 읽기/쓰기 보조 파일 그룹을 포함하며 차등 부분 백업의 기반으로 사용될 수 있습니다.  
  
 읽기 전용 파일 그룹의 파일 백업을 부분 백업과 결합할 수 있습니다. 파일 백업에 대한 자세한 내용은 [전체 파일 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)을 참조하세요.  
  
 부분 백업은 차등 부분 백업에 대해 *차등 기반* 으로 사용될 수 있습니다. 자세한 내용은 [차등 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)을 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
> [!NOTE]  
>  부분 백업은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 유지 관리 계획 마법사에서 지원하지 않습니다.  
  
 **부분 백업을 만들려면**  
  
-   [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)(READ_WRITE_FILEGROUPS, FILEGROUP 그룹 옵션, 필요한 경우)  
  
 **복원 시퀀스에서 부분 백업을 사용하려면**  
  
-   [예제: 데이터베이스의 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [예제: 일부 파일 그룹만 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="see-also"></a>참고 항목  
 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [파일 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
