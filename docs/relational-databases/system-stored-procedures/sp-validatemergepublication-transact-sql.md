---
title: sp_validatemergepublication (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validatemergepublication
- sp_validatemergepublication_TSQL
helpviewer_keywords:
- sp_validatemergepublication
ms.assetid: 5a862f1a-2be1-4758-9954-4cdc8c77d149
author: stevestein
ms.author: sstein
ms.openlocfilehash: 02ffdd0facfedd1b9eb6d8eee083f819566d818d
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72006098"
---
# <a name="sp_validatemergepublication-transact-sql"></a>s sp_validatemergepublication(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  모든 구독(밀어넣기, 끌어오기 및 익명 구독)에 대해 한 번씩 유효성 검사를 하는 게시 차원의 유효성 검사를 수행합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_validatemergepublication [@publication=] 'publication'  
        , [ @level = ] level  
```  
  
## <a name="arguments"></a>인수  
 [ **\@게시 =** ] **'***게시***'**  
 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @level = ] level`는 수행할 유효성 검사의 유형입니다. *level* 은 **tinyint**이며 기본값은 없습니다. 수준은 다음 값 중 하나일 수 있습니다.  
  
|수준 값|설명|  
|-----------------|-----------------|  
|**1.**|행 개수의 유효성만 검사합니다.|  
|**2**|행 개수 및 체크섬의 유효성을 검사합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]구독자의 경우 자동으로 **3**으로 설정 됩니다.|  
|**3**|권장 값입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_validatemergepublication** 는 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_validatemergepublication**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [복제 된 데이터의 유효성 검사](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [Transact-sql &#40;sp_validatemergesubscription&#41;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md)  
  
  
