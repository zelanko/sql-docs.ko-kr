---
title: "MSSQLSERVER_3159 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3159 (Database Engine error)
ms.assetid: c93c1003-0e3a-40aa-9873-44a0f5b8b57e
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 718f42e23ceaf9aacf0d12ecd161a132ee503174
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver3159"></a>MSSQLSERVER_3159
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|이벤트 ID|3159|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LDDB_LOGNOTBACKEDUP|  
|메시지 텍스트|데이터베이스 "%ls"의 비상 로그 백업이 수행되지 않았습니다. 로그에 포함된 작업이 손실되지 않도록 하려면 BACKUP LOG WITH NORECOVERY를 사용하여 로그를 백업하십시오. 로그 내용을 덮어쓰려면 RESTORE 문에 WITH REPLACE나 WITH STOPAT 절을 사용하십시오.|  
  
## <a name="explanation"></a>설명  
대부분의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 전체 또는 대량 로그 복구 모델을 사용할 경우 아직 백업되지 않은 로그 레코드를 캡처하기 위해 비상 로그 백업을 수행해야 합니다. 복원 작업 바로 전에 수행한 비상 로그의 로그 백업을 비상 로그 백업이라고 합니다.  
  
데이터베이스를 실패 지점으로 복구할 때는 비상 로그 백업이 복구 계획의 마지막 백업입니다. 비상 로그를 백업할 수 없으면 실패 전에 생성된 마지막 백업의 끝으로만 데이터베이스를 복구할 수 있습니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 일반적으로 데이터베이스를 복원하기 전에 비상 로그 백업을 수행해야 합니다. 비상 로그 백업은 작업 손실을 방지하고 로그 체인을 그대로 유지합니다. 그러나 모든 복원 시나리오에서 비상 로그 백업이 필요한 것은 아닙니다. 복구 지점이 이전 로그 백업에 포함된 경우 또는 데이터베이스를 이동 또는 대체(덮어쓰기)하는 중이고 가장 최근 백업 이후의 시점으로 이를 복원할 필요가 없는 경우에는 비상 로그 백업이 필요하지 않습니다. 또한 로그 파일이 손상되었고 비상 로그 백업을 만들 수 없으면 비상 로그 백업을 사용하지 않고 데이터베이스를 복원해야 합니다. 최신 로그 백업 이후 커밋된 모든 트랜잭션은 손실됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "비상 로그 백업을 사용하지 않고 복원"을 참조하십시오.  
  
> [!CAUTION]  
> REPLACE는 신중한 검토 후에만 사용해야 하며 되도록 사용하지 않아야 합니다.  
  
## <a name="user-action"></a>사용자 동작  
비상 로그 백업을 수행하고 복원 작업을 다시 시도합니다.  
  
비상 로그를 백업할 수 없으면 RESTORE 문에 WITH STOPAT 또는 WITH REPLACE를 사용합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](~/relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
[데이터베이스가 손상된 경우 트랜잭션 로그 백업&#40;SQL Server&#41;](~/relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
[트랜잭션 로그 백업&#40;SQL Server&#41;](~/relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
[비상 로그 백업&#40;SQL Server&#41;](~/relational-databases/backup-restore/tail-log-backups-sql-server.md)  
  
