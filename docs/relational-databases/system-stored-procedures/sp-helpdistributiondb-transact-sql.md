---
title: sp_helpdistributiondb (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdistributiondb_TSQL
- sp_helpdistributiondb
helpviewer_keywords:
- sp_helpdistributiondb
ms.assetid: a2917020-26d1-4011-99f8-9212d120fd2d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 040970c34e8154538135e355744746e3ee1e3cb6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdistributiondb-transact-sql"></a>sp_helpdistributiondb(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 배포 데이터베이스의 속성을 반환합니다. 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpdistributiondb [ [ @database= ] 'database_name' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@database=**] **'***database_name***'**  
 속성이 반환되는 데이터베이스 이름입니다. *a s e _* 은 **sysname**, 기본값은  **%**  에 배포자와 관련 된 모든 데이터베이스에 대 한 사용자에 게 권한이 있습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|배포 데이터베이스의 이름입니다.|  
|**min_distretention**|**int**|트랜잭션을 삭제하기 전 최소 보존 기간(시간)을 표시합니다.|  
|**max_distretention**|**int**|트랜잭션을 삭제하기 전 최대 보존 기간(시간)을 표시합니다.|  
|**기록 보존**|**int**|기록을 보존할 기간(시간)입니다.|  
|**history_cleanup_agent**|**sysname**|기록 정리 에이전트의 이름입니다.|  
|**distribution_cleanup_agent**|**sysname**|배포 정리 에이전트의 이름입니다.|  
|**상태**|**int**|내부적으로만 사용됩니다.|  
|**data_folder**|**nvarchar(255)**|데이터베이스 파일을 저장하는 데 사용되는 디렉터리 이름입니다.|  
|**data_file**|**nvarchar(255)**|데이터베이스 파일의 이름입니다.|  
|**data_file_size**|**int**|초기 데이터 파일의 크기(MB)입니다.|  
|**log_folder**|**nvarchar(255)**|데이터베이스 로그 파일의 디렉터리 이름입니다.|  
|**log_file**|**nvarchar(255)**|로그 파일의 이름입니다.|  
|**log_file_size**|**int**|초기 로그 파일의 크기(MB)입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_helpdistributiondb** 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 멤버는 **db_owner** 고정된 데이터베이스 역할 또는 **replmonitor** 배포 데이터베이스에서 역할 및 배포 데이터베이스를 사용 하는 게시의 게시 액세스 목록에 사용자가 실행할 수 있습니다 **sp_helpdistributiondb** 파일 관련 정보를 반환 합니다. 멤버는 **공용** 역할이 실행할 수 있는 **sp_helpdistributiondb** 액세스 권한이 있는 배포 데이터베이스에 대 한 파일-관련 없는 정보를 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
