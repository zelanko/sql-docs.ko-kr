---
title: sp_validatemergesubscription (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_validatemergesubscription
- sp_validatemergesubscription_TSQL
helpviewer_keywords:
- sp_validatemergesubscription
ms.assetid: d73ad03c-e5b3-4606-a0ee-7d75e12762a6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5c142ab2f8de6db1bfdd288734a47f6a4e9e6946
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746561"
---
# <a name="spvalidatemergesubscription-transact-sql"></a>sp_validatemergesubscription(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 구독에 대해 유효성 검사를 수행합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_validatemergesubscription [@publication=] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @subscriber_db = ] 'subscriber_db'  
        , [ @level = ] level  
```  
  
## <a name="arguments"></a>인수  
 [**@publication=**] **'***게시***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@subscriber=** ] **'***구독자***'**  
 구독자의 이름입니다. *구독자* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@subscriber_db=** ] **'***subscriber_db***'**  
 구독 데이터베이스의 이름입니다. *subscriber_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@level=** ] *수준*  
 수행할 유효성 검사의 유형입니다. *수준* 됩니다 **tinyint**, 기본값은 없습니다. 수준은 다음 값 중 하나일 수 있습니다.  
  
|수준 값|Description|  
|-----------------|-----------------|  
|**1**|행 개수의 유효성만 검사합니다.|  
|**2**|행 개수 및 체크섬의 유효성을 검사합니다.|  
|**3**|행 개수 및 이진 체크섬의 유효성을 검사합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_validatemergesubscription** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_validatemergesubscription**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [복제 된 데이터 유효성 검사](../../relational-databases/replication/validate-replicated-data.md)   
 [sp_validatemergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md)  
  
  
