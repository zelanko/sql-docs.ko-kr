---
title: managed_backup. fn_is_master_switch_on (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_is_master_switch_on
- fn_is_master_switch_on_TSQL
- smart_admin.fn_is_master_switch_on
- smart_admin.fn_is_master_switch_on_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_is_master_switch_on
- fn_is_master_switch_on
ms.assetid: e8c2108d-b104-46cb-9645-a15f46112c86
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 044cdc1b334732a0730cd2c223d5690e4089a0cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68140638"
---
# <a name="managed_backupfn_is_master_switch_on-transact-sql"></a>managed_backup. fn_is_master_switch_on (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  SQL Server 인스턴스에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 작업의 상태를 반환합니다.  
  
 이 함수를 사용하면 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]의 현재 상태를 가져올 수 있습니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
managed_backup.fn_is_master_switch_on ()  
```  
  
##  <a name="Arguments"></a> 인수  
 None  
  
## <a name="return-type"></a>반환 형식  
 **조금**  
  
 1 = [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 활성 상태임, 0 = [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 일시 중지됨  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 함수에 대해 SELECT 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft Azure에 대한 SQL Server Managed Backup](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
