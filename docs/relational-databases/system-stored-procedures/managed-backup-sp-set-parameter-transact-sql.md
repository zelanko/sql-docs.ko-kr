---
title: managed_backup. sp_set_parameter (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3eab417e1d959c990e53aca3119546a73a3e1aad
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052919"
---
# <a name="managed_backupsp_set_parameter-transact-sql"></a>managed_backup. sp_set_parameter (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  지정된 스마트 관리 시스템 매개 변수의 값을 설정합니다.  
  
 사용 가능한 매개 변수는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]과 관련되어 있습니다. 이러한 매개 변수는 전자 메일 알림을 설정하고 특정 확장 이벤트를 사용하도록 설정하며 사용자를 통해 정책 기반 관리 정책을 설정하는 데 사용됩니다. 매개 변수 이름과 매개 변수 값 쌍을 지정해야 합니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
EXEC managed_backup.sp_set_parameter   
    [@parameter_name = ] {'SSMBackup2WANotificationEmailIds' | 'SSMBackup2WAEnableUserDefinedPolicy' | 'SSMBackup2WADebugXevent' | 'FileRetentionDebugXevent' | 'StorageOperationDebugXevent'}  
    ,[@parameter_value = ] 'parameter_value'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>인수의  
 @parameter_name  
 값을 설정하려는 매개 변수의 이름입니다. @parameter_name는 NVARCHAR (128)입니다. 사용할 수 있는 매개 변수 이름은 **SSMBackup2WANotificationEmailIds**, **SSMBackup2WADebugXevent**, **SSMBackup2WAEnableUserDefinedPolicy**, **FileRetentionDebugXevent**및 **storageoperationdebugxevent**입니다.  
  
 @parameter_value  
 설정하려는 매개 변수의 값입니다. @parameter값은 NVARCHAR (128)입니다.  다음은 허용되는 매개 변수 이름과 값 쌍입니다.  
  
-   @parameter_name= ' SSMBackup2WANotificationEmailIds ': @parameter_value = ' email '  
  
-   @parameter_name= ' SSMBackup2WAEnableUserDefinedPolicy ': @parameter_value = {' true ' | ' false '}  
  
-   @parameter_name= ' SSMBackup2WADebugXevent ': @parameter_value = {' true ' | ' false '}  
  
-   @parameter_name= ' FileRetentionDebugXevent ': @parameter_value = {' true ' | ' false '}  
  
-   @parameter_name= ' StorageOperationDebugXevent ' = {' true ' | ' false '}  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="best-practices"></a>모범 사례  
 최선의 구현 방법을 설명하는 옵션 섹션에서 사용자는 문 또는 루틴을 실행할 때를 알아야 합니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 **Managed_backup. sp_set_parameter** 저장 프로시저에 대 한 **EXECUTE** 권한이 필요 합니다.  
  
## <a name="examples"></a>예제  
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
  
  
