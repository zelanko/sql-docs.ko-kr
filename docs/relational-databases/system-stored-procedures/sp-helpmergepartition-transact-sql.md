---
title: sp_helpmergepartition (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- sp_helpmergepartition
- sp_helpmergepartition_TSQL
helpviewer_keywords:
- sp_helpmergepartition
ms.assetid: 184188cc-f519-445d-97ce-aae38f1eb550
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a2c4e931f2da9794392056595ab71b88e005a26f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpmergepartition-transact-sql"></a>sp_helpmergepartition(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 병합 게시에 대한 파티션 정보를 반환합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpmergepartition [ @publication= ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]  
    [ , [ @host_name = ] 'host_name' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication=** ] **'***게시***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@suser_sname=** ] **'***suser_sname***'**  
 파티션을 정의하는 데 사용하는 SUSER_SNAME 값입니다. *suser_sname* 은 **sysname**, 기본값은 NULL입니다. SUSER_SNAME이 제공된 값을 확인하는 파티션으로만 결과 집합을 제한하려면 이 매개 변수를 제공하십시오.  
  
> [!NOTE]  
>  때 *suser_sname* 제공 *host_name* NULL 이어야 합니다  
  
 [  **@host_name=** ] **'***host_name***'**  
 파티션을 정의하는 데 사용하는 HOST_NAME 값입니다. *host_name* 은 **sysname**, 기본값은 NULL입니다. HOST_NAME이 제공된 값을 확인하는 파티션으로만 결과 집합을 제한하려면 이 매개 변수를 제공하십시오.  
  
> [!NOTE]  
>  때 *suser_sname* 제공 *host_name* NULL 이어야 합니다  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**파티션**|**int**|구독자 파티션을 식별합니다.|  
|**host_name**|**sysname**|값으로 필터링 되는 구독에 대 한 파티션을 만들 때 사용 되는 값은 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 구독자에는 함수입니다.|  
|**suser_sname**|**sysname**|값으로 필터링 되는 구독에 대 한 파티션을 만들 때 사용 되는 값은 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 구독자에는 함수입니다.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|구독자의 파티션에 대한 필터링된 데이터 스냅숏의 위치입니다.|  
|**date_refreshed**|**datetime**|파티션에 대한 필터링된 데이터 스냅숏을 생성하기 위해 스냅숏 작업을 마지막으로 실행한 날짜입니다.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|파티션에 대한 필터링된 데이터 스냅숏을 만드는 작업을 식별합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_helpmergepartition** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 및 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_helpmergepartition**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_addmergepartition &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [sp_dropmergepartition &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md)  
  
  
