---
title: sp_helpreplicationdboption (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpreplicationdboption_TSQL
- sp_helpreplicationdboption
helpviewer_keywords:
- sp_helpreplicationdboption
ms.assetid: 143ce689-108b-49d7-9892-fd3a86897f38
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1066644508c586fe2542d2e86bd3f67059d22663
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpreplicationdboption-transact-sql"></a>sp_helpreplicationdboption(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시자에서 데이터베이스가 복제를 사용할 수 있도록 설정되었는지 여부를 표시합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다. *Oracle 게시자에 대해서는 지원 되지 않습니다.*  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpreplicationdboption [ [ @dbname =] 'dbname' ]  
    [ , [ @type = ] 'type' ]  
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@dbname=**] **'***dbname***'**  
 데이터베이스의 이름입니다. *dbname* 은 **sysname**, 기본값은 **%** 합니다. 경우 **%**, 다음 결과 집합에 게시자에서 모든 데이터베이스가 포함 되지만, 그렇지 않으면 지정된 된 데이터베이스에 대 한 정보만 반환 됩니다. 아래에 설명된 바와 같이 사용자가 적절한 권한을 가지고 있지 않은 데이터베이스에 대해서는 정보가 반환되지 않습니다.  
  
 [  **@type=**] **'***형식***'**  
 결과 집합에 데이터베이스만 포함 되도록 제한 지정한 복제 옵션인 *형식* 값이 설정 된 합니다. *형식* 은 **sysname**, 다음 값 중 하나가 될 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**게시**|트랜잭션 복제가 허용됩니다.|  
|**병합 게시**|병합 복제가 허용됩니다.|  
|**복제가 허용** (기본값)|트랜잭션 또는 병합 복제가 허용됩니다.|  
  
 [  **@reserved=** ] *예약*  
 기존 게시 및 구독에 대한 정보를 반환할지 여부를 지정합니다. *예약 된* 은 **비트**을 기본값인 0으로 합니다. 경우 **1**, 결과 집합 지정 된 데이터베이스의 모든 기존 게시 또는 구독에 있는지 여부에 대 한 정보가 포함 됩니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|데이터베이스의 이름입니다.|  
|**id**|**int**|데이터베이스 식별자입니다.|  
|**transpublish**|**bit**|스냅숏 또는 트랜잭션 게시에 대 한 데이터베이스를 사용 하도록 설정 된 경우 여기서 값 **1** 스냅숏 또는 트랜잭션 게시를 사용할 수 있음을 의미 합니다.|  
|**mergepublish**|**bit**|병합 게시에 대 한 데이터베이스를 사용 하도록 설정 된 경우 여기서 값 **1** 게시를 병합 하는 수단을 사용 하도록 설정 합니다.|  
|**dbowner**|**bit**|사용자가 멤버인 경우는 **db_owner** 고정 데이터베이스 역할입니다; 여기서 값 **1** 사용자가이 역할의 멤버 임을 나타냅니다.|  
|**dbreadonly**|**bit**|데이터베이스는 읽기 전용으로 표시 됩니다. 여기서 값 **1** 읽기 전용 데이터베이스 임을 의미 합니다.|  
|**haspublications**|**bit**|데이터베이스에 기존 게시가 있는지는 여기서 값 **1** 기존 게시가 있음을 의미 합니다.|  
|**haspullsubscriptions**|**bit**|데이터베이스에 기존 끌어오기 구독이 있는; 경우 여기서 값 **1** 는 기존 끌어오기 구독이 것을 의미 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_helpreplicationdboption** 스냅숏, 트랜잭션 및 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_helpreplicationdboption** 모든 데이터베이스에 대 한 합니다. 멤버는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_helpreplicationdboption** 해당 데이터베이스에 대 한 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_replicationdboption &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
