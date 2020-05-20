---
title: restorefilegroup (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- restorefilegroup_TSQL
- restorefilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], restorefilegroup system table
- restorefilegroup system table
ms.assetid: 3aa15c55-6b72-4f76-97d7-bd88391d105c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b8dbdc6cb36ccfca3abb3966fc6e192200b6b72c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827170"
---
# <a name="restorefilegroup-transact-sql"></a>restorefilegroup(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  복원된 각 파일 그룹에 대해 하나의 행을 포함합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|해당되는 복원 작업을 식별하는 고유 ID입니다. **Restorehistory (restore_history_id)** 를 참조 합니다.|  
|**filegroup_name**|**nvarchar(128)**|복원되는 파일 그룹의 이름입니다. NULL일 수 있습니다.<br /><br /> 데이터베이스를 데이터베이스 스냅샷으로 되돌릴 경우 이 값은 전체 복원과 같은 방식으로 채워집니다.|  
  
## <a name="remarks"></a>설명  
 이 테이블의 행 수와 다른 백업 및 기록 테이블의 행 수를 줄이려면 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) 저장 프로시저를 실행 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;테이블 백업 및 복원](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefile &#40;Transact-sql&#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [restorehistory &#40;Transact-sql&#41;](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
