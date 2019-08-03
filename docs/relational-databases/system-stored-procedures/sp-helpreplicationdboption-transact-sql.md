---
title: sp_helpreplicationdboption (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplicationdboption_TSQL
- sp_helpreplicationdboption
helpviewer_keywords:
- sp_helpreplicationdboption
ms.assetid: 143ce689-108b-49d7-9892-fd3a86897f38
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7aa68b2ee2e592f264f5a64c4c675103253da495
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771526"
---
# <a name="sphelpreplicationdboption-transact-sql"></a>sp_helpreplicationdboption(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  게시자에서 데이터베이스가 복제를 사용할 수 있도록 설정되었는지 여부를 표시합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다. *Oracle 게시자에 대해서는 지원 되지 않습니다.*  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpreplicationdboption [ [ @dbname =] 'dbname' ]  
    [ , [ @type = ] 'type' ]  
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>인수  
`[ @dbname = ] 'dbname'`데이터베이스의 이름입니다. *dbname* 은 **sysname**이며 기본값 **%** 은입니다. 이면 **%** 결과 집합에 게시자의 모든 데이터베이스가 포함 되 고, 그렇지 않으면 지정 된 데이터베이스에 대 한 정보만 반환 됩니다. 아래에 설명된 바와 같이 사용자가 적절한 권한을 가지고 있지 않은 데이터베이스에 대해서는 정보가 반환되지 않습니다.  
  
`[ @type = ] 'type'`지정 된 복제 옵션 *유형* 값이 설정 된 데이터베이스만 포함 하도록 결과 집합을 제한 합니다. *형식은* **sysname**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**publish**|트랜잭션 복제가 허용됩니다.|  
|**병합 게시**|병합 복제가 허용됩니다.|  
|**복제 허용** 기본|트랜잭션 또는 병합 복제가 허용됩니다.|  
  
`[ @reserved = ] reserved`기존 게시 및 구독에 대 한 정보를 반환할지 여부를 지정 합니다. *reserved* 는 **bit**이며 기본값은 0입니다. **1**인 경우 지정한 데이터베이스에 기존 게시 또는 구독이 있는지 여부에 대 한 정보가 결과 집합에 포함 됩니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|데이터베이스의 이름입니다.|  
|**id**|**int**|데이터베이스 식별자입니다.|  
|**transpublish**|**bit**|데이터베이스가 스냅숏 또는 트랜잭션 게시를 사용 하도록 설정 된 경우 값이 **1** 이면 스냅숏 또는 트랜잭션 게시를 사용할 수 있음을 의미 합니다.|  
|**mergepublish**|**bit**|데이터베이스가 병합 게시를 사용 하도록 설정 된 경우 값 **1** 은 병합 게시를 사용할 수 있음을 의미 합니다.|  
|**dbowner**|**bit**|사용자가 **db_owner** 고정 데이터베이스 역할의 멤버 이면이 고, 그렇지 않으면입니다. 값이 **1** 이면 사용자가이 역할의 구성원 임을 나타냅니다.|  
|**dbreadonly**|**bit**|데이터베이스가 읽기 전용으로 표시 되어 있으면이 고, 그렇지 않으면입니다. 값이 **1** 이면 데이터베이스가 읽기 전용입니다.|  
|**haspublications**|**bit**|데이터베이스에 기존 게시가 있는지 여부입니다. 값 **1** 은 기존 게시가 있음을 의미 합니다.|  
|**haspullsubscriptions**|**bit**|데이터베이스에 기존 끌어오기 구독이 있는지 여부입니다. 값이 **1** 이면 기존 끌어오기 구독이 있음을 의미 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpreplicationdboption** 는 스냅숏, 트랜잭션 및 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버는 모든 데이터베이스에 대해 **sp_helpreplicationdboption** 을 실행할 수 있습니다. **Db_owner** 고정 데이터베이스 역할의 멤버는 해당 데이터베이스에 대해 **sp_helpreplicationdboption** 을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_replicationdboption &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
