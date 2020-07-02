---
title: sp_helpmergepartition (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepartition
- sp_helpmergepartition_TSQL
helpviewer_keywords:
- sp_helpmergepartition
ms.assetid: 184188cc-f519-445d-97ce-aae38f1eb550
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3812f7c59790d05f3519b94185a80dd6e22626cd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733076"
---
# <a name="sp_helpmergepartition-transact-sql"></a>sp_helpmergepartition(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  지정한 병합 게시에 대한 파티션 정보를 반환합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpmergepartition [ @publication= ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]  
    [ , [ @host_name = ] 'host_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @suser_sname = ] 'suser_sname'`파티션을 정의 하는 데 사용 되는 SUSER_SNAME 값입니다. *suser_sname* 는 **sysname**이며 기본값은 NULL입니다. SUSER_SNAME이 제공된 값을 확인하는 파티션으로만 결과 집합을 제한하려면 이 매개 변수를 제공하십시오.  
  
> [!NOTE]  
>  *Suser_sname* 제공 되는 경우 *host_name* 은 NULL 이어야 합니다.  
  
`[ @host_name = ] 'host_name'`파티션을 정의 하는 데 사용 되는 HOST_NAME 값입니다. *host_name* 는 **sysname**이며 기본값은 NULL입니다. HOST_NAME이 제공된 값을 확인하는 파티션으로만 결과 집합을 제한하려면 이 매개 변수를 제공하십시오.  
  
> [!NOTE]  
>  *Suser_sname* 제공 되는 경우 *host_name* 은 NULL 이어야 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**파티션마다**|**int**|구독자 파티션을 식별합니다.|  
|**host_name**|**sysname**|구독자에서 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 함수의 값으로 필터링 되는 구독에 대 한 파티션을 만들 때 사용 되는 값입니다.|  
|**suser_sname**|**sysname**|구독자에서 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 함수의 값으로 필터링 되는 구독에 대 한 파티션을 만들 때 사용 되는 값입니다.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|구독자의 파티션에 대한 필터링된 데이터 스냅샷의 위치입니다.|  
|**date_refreshed**|**datetime**|파티션에 대한 필터링된 데이터 스냅샷을 생성하기 위해 스냅샷 작업을 마지막으로 실행한 날짜입니다.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|파티션에 대한 필터링된 데이터 스냅샷을 만드는 작업을 식별합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpmergepartition** 는 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 및 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_helpmergepartition**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addmergepartition &#40;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [Transact-sql&#41;sp_dropmergepartition &#40;](../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md)  
  
  
