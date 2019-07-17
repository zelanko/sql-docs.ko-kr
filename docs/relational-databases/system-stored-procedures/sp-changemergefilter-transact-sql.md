---
title: sp_changemergefilter (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergefilter_TSQL
- sp_changemergefilter
helpviewer_keywords:
- sp_changemergefilter
ms.assetid: e08fdfdd-d242-4e85-817b-9f7a224fe567
author: stevestein
ms.author: sstein
ms.openlocfilehash: e0c38af1089a1d59c9964e39aecca6b1773a8e22
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124888"
---
# <a name="spchangemergefilter-transact-sql"></a>sp_changemergefilter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  일부 병합 필터 속성을 변경합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changemergefilter [ @publication= ] 'publication'  
        , [ @article= ] 'article'  
        , [ @filtername= ] 'filtername'  
        , [ @property= ] 'property'  
        , [ @value= ] 'value'  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @article = ] 'article'` 아티클의 이름이입니다. *문서* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @filtername = ] 'filtername'` 필터의 현재 이름이입니다. *filtername* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @property = ] 'property'` 변경할 속성의 이름이입니다. *속성* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @value = ] 'value'` 지정된 된 속성에 대 한 새 값이입니다. *값*됩니다 **nvarchar(1000)** , 기본값은 없습니다.  
  
 다음 표에서는 아티클의 속성 및 해당 속성의 값을 설명합니다.  
  
|속성|값|설명|  
|--------------|-----------|-----------------|  
|**filter_type**|**1**|조인 필터입니다.<br /><br /> 이 옵션은 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자를 지원하는 데 필요합니다.|  
||**2**|논리적 레코드 관계입니다.|  
||**3**|조인 필터가 논리적 레코드 관계도 됩니다.|  
|**filtername**||필터의 이름입니다.|  
|**join_articlename**||조인 아티클의 이름입니다.|  
|**join_filterclause**||필터 절입니다.|  
|**join_unique_key**|**true**|조인이 고유 키에 있습니다.|  
||**false**|조인이 고유 키에 없습니다.|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 으로 인해이 저장된 프로시저가 수행한 동작 기존 스냅숏을 무효화 될 수 있습니다. *force_invalidate_snapshot* 되는 **비트**, 기본값 **0**합니다.  
  
 **0** 병합 아티클에 대 한 변경 인해 스냅숏이 무효화 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅샷을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 의미 병합 아티클에 대 한 변경을 유효 하지 않게 스냅숏을 무효화 하는 새 스냅숏이 필요한 기존 구독이 있는 경우 제공 되지 않음으로 표시 될 기존 스냅숏과 하 고 새 스냅숏을 생성할 권한을 합니다.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` 이 저장된 프로시저가 수행한 동작 기존 구독을 다시 초기화에 필요할 수 있음을 승인 합니다. *force_reinit_subscription* 되는 **비트** 이며 기본값은 **0**합니다.  
  
 **0** 병합 아티클에 대 한 변경으로 인해 구독이 다시 초기화 해야 되지 않습니다 지정 합니다. 저장 프로시저가 기존 구독을 다시 초기화해야 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 의미 하는 병합 아티클을 변경 하는 기존 구독이 다시 초기화 하면 구독을 다시 초기화할 수 있는 권한을 부여 하 고 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changemergefilter** 병합 복제에 사용 됩니다.  
  
 병합 아티클의 필터를 변경하려면 스냅샷이 하나 있는 경우 이를 다시 만들어야 합니다. 이 작업을 설정 하 여 수행 됩니다 합니다 **@force_invalidate_snapshot** 하려면 **1**합니다. 또한 이 아티클에 대한 구독이 있을 경우 구독을 다시 초기화해야 합니다. 설정 하 여 이렇게 합니다 **@force_reinit_subscription** 하 **1**.  
  
 논리적 레코드를 사용하려면 게시 및 아티클이 여러 가지 요구 사항을 만족해야 합니다. 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_changemergefilter**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_dropmergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
