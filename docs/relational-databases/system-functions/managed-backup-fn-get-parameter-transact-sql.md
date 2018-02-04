---
title: managed_backup.fn_get_parameter (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/03/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_get_parameter_TSQL
- smart_admin.fn_get_parameter
- fn_get_parameter_TSQL
- fn_get_parameter
dev_langs:
- TSQL
helpviewer_keywords:
- fn_get_parameter
- smart_admin.fn_get_parameter
ms.assetid: ed94e54d-4516-4806-a8ce-f013d3a04122
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 204891340d07d504522765f1f7982768d2bfc50c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="managedbackupfngetparameter-transact-sql"></a>managed_backup.fn_get_parameter (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  매개 변수와 값 쌍에 대해 0, 1 또는 그 이상의 행이 포함된 테이블을 반환합니다.  
  
 이 저장 프로시저를 사용하여 스마트 관리에 대한 모든 또는 특정 구성 설정을 검토할 수 있습니다.  
  
 매개 변수가 이전에 구성되지 않은 경우, 함수가 0개 행을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
managed_backup.fn_get_parameter ('parameter_name' | '' | NULL )  
```  
  
##  <a name="Arguments"></a> 인수  
 parameter_name  
 매개 변수의 이름입니다. parameter_name은 **nvarchar (128)**합니다. 함수에 NULL 또는 빈 문자열이 인수로 제공된 경우 구성된 모든 스마트 관리 매개 변수에 대한 이름-값 쌍이 반환됩니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|parameter_name|NVARCHAR(128)|매개 변수의 이름입니다. 다음은 반환되는 현재 매개 변수 목록입니다.<br/><br/>**FileRetentionDebugXevent**<br/><br/>**SSMBackup2WADebugXevent**<br/><br/>**SSMBackup2WANotificationEmailIds**<br/><br/>**SSMBackup2WAEnableUserDefinedPolicy**<br/><br/>**SSMBackup2WAEverConfigured**<br/><br/>**StorageOperationDebugXevent**|  
|parameter_value|NVARCHAR(128)|매개 변수의 현재 설정 값입니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 함수에 대해 SELECT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 이전에 한 번 이상 구성된 모든 매개 변수와 해당 매개 변수의 현재 값을 반환합니다.  
  
```  
USE MSDB  
GO  
SELECT *   
FROM managed_backup.fn_get_parameter (NULL)  
  
```  
  
 다음 예제에서는 오류 알림을 수신하도록 지정된 전자 메일 ID를 반환합니다. 행이 반환되지 않으면 이 전자 메일 알림 옵션이 설정되지 않았음을 의미합니다.  
  
```  
USE MSDB  
GO  
SELECT *  
FROM managed_backup.fn_get_parameter ('SSMBackup2WANotficationEmailIds')  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft Azure에 대한 SQL Server Managed Backup](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
