---
title: managed_backup. sp_backup_on_demand (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.sp_backup_on_demand
- smart_admin.sp_backup_on_demand_TSQL
- sp_backup_on_demand_TSQL
- sp_backup_on_demand
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.sp_backup_on_demand
- sp_backup_on_demand
ms.assetid: 638f809f-27fa-4c44-a549-9cf37ecc920c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e34cf20585ea7dcd3690d80ee415fc274bf852ca
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155396"
---
# <a name="managed_backupsp_backup_on_demand-transact-sql"></a>managed_backup. sp_backup_on_demand (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  지정된 데이터베이스 백업을 수행하려면 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 요청합니다.  
  
 이 저장 프로시저를 사용하면 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]으로 구성된 데이터베이스에 대한 임시 백업을 수행할 수 있습니다. 이렇게 하면 백업 체인의 모든 중단을 방지 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 하 고 프로세스를 인식 하며 백업이 동일한 Azure Blob storage 컨테이너에 저장 됩니다.  
  
 백업이 성공적으로 완료된 다음에는 전체 백업 파일 경로가 반환됩니다. 여기에는 백업 작업으로 발생하는 새 백업 파일의 이름 및 위치가 포함됩니다.  
  
 지정된 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 지정된 유형의 백업을 실행하는 중에 있으면 오류가 반환됩니다. 이 경우 반환된 오류 메시지에는 현재 백업을 업그레이드 중인 전체 백업 파일 경로가 포함됩니다.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
EXEC managed_backup.sp_backup_on_demand   
[@database_name  =]  'database name',[@type = ] { 'Database' | 'Log' }  
  
```  
  
##  <a name="Arguments"></a> 인수  
 @database_name  
 백업을 수행할 데이터베이스의 이름입니다. 는 @database_name **SYSNAME**입니다.  
  
 @type  
 수행할 백업 유형:  데이터베이스 또는 로그. 매개 @type 변수는 **NVARCHAR (32)** 입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 **ALTER ANY CREDENTIAL** 권한이 있는 **db_backupoperator** 데이터베이스 역할의 멤버 자격 및 **sp_delete_backuphistory**저장 프로시저에 대 한 **EXECUTE** 권한이 필요 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 ' TestDB ' 데이터베이스에 대 한 데이터베이스 백업 요청을 만듭니다. 이 데이터베이스에는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 설정되어 있습니다.  
  
```  
Use MSDB  
Go  
EXEC managed_backup.sp_backup_on_demand  
 @database_name = 'TestDB'  
,@type = 'Database'  
  
```  
  
 각 코드 조각에 대해 언어 특성 필드에서 'tsql'을 선택합니다.  
  
  
