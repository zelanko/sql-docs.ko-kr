---
title: managed_backup.sp_set_parameter (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_set_parameter_TSQL
- sp_set_parameter
- smart_admin.sp_set_parameter
- smart_admin.sp_set_parameter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_parameter
- smart_admin.sp_set_parameter
ms.assetid: bd8ae5fd-1337-4b7f-b0a4-153cbca9fa5f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 578997f57c4092689e49cb0e3102c8bdf7b4f8d2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47843898"
---
# <a name="managedbackupspsetparameter-transact-sql"></a>managed_backup.sp_set_parameter (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  지정된 스마트 관리 시스템 매개 변수의 값을 설정합니다.  
  
 사용 가능한 매개 변수는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]과 관련되어 있습니다. 이러한 매개 변수는 전자 메일 알림을 설정하고 특정 확장 이벤트를 사용하도록 설정하며 사용자를 통해 정책 기반 관리 정책을 설정하는 데 사용됩니다. 매개 변수 이름과 매개 변수 값 쌍을 지정해야 합니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
EXEC managed_backup.sp_set_parameter   
    [@parameter_name = ] {'SSMBackup2WANotificationEmailIds' | 'SSMBackup2WAEnableUserDefinedPolicy' | 'SSMBackup2WADebugXevent' | 'FileRetentionDebugXevent' | 'StorageOperationDebugXevent'}  
    ,[@parameter_value = ] 'parameter_value'  
```  
  
##  <a name="Arguments"></a> 인수  
 @parameter_name  
 값을 설정하려는 매개 변수의 이름입니다. @parameter_name NVARCHAR(128)입니다. 사용 가능한 매개 변수 이름은 **SSMBackup2WANotificationEmailIds**, **SSMBackup2WADebugXevent**하십시오 **SSMBackup2WAEnableUserDefinedPolicy**를 **FileRetentionDebugXevent**, 및 **StorageOperationDebugXevent**합니다.  
  
 @parameter_value  
 설정하려는 매개 변수의 값입니다. @parameter value는 NVARCHAR(128)입니다.  다음은 허용되는 매개 변수 이름과 값 쌍입니다.  
  
-   @parameter_name = 'SSMBackup2WANotificationEmailIds': @parameter_value = 'email'  
  
-   @parameter_name = 'SSMBackup2WAEnableUserDefinedPolicy' : @parameter_value  = { 'true' | 'false' }  
  
-   @parameter_name = 'SSMBackup2WADebugXevent': @parameter_value = {'true' | false'}  
  
-   @parameter_name = 'FileRetentionDebugXevent': @parameter_value = {'true' | false'}  
  
-   @parameter_name = 'StorageOperationDebugXevent' = { 'true' | 'false' }  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="best-practices"></a>최선의 구현 방법  
 최선의 구현 방법을 설명하는 옵션 섹션에서 사용자는 문 또는 루틴을 실행할 때를 알아야 합니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 필요 **EXECUTE** 에 대 한 권한을 **managed_backup.sp_set_parameter** 저장 프로시저입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 operational 및 debug 확장 이벤트를 사용하도록 설정합니다.  
  
```  
-- to enable operational events  
Use msdb;  
Go  
         EXEC managed_backup.sp_set_parameter 'FileRetentionOperationalXevent', 'True'  
--  to enable debug events  
Use msdb;  
Go  
         EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
```  
  
 다음 예에서는 오류 및 경고에 대한 전자 메일 알림을 사용하도록 설정하고 알림을 전송하는 데 사용할 전자 메일 ID를 설정합니다.  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_set_parameter @parameter_name = 'SSMBackup2WANotificationEmailIds', @parameter_value = '<email address>'  
  
```  
  
  
