---
title: sp_changemergefilter (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: bfe3cd91150d1990acc410cb4a61af9485c61f4b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72304943"
---
# <a name="sp_changemergefilter-transact-sql"></a>sp_changemergefilter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  일부 병합 필터 속성을 변경합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'`아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @filtername = ] 'filtername'`필터의 현재 이름입니다. *filtername* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @property = ] 'property'`변경할 속성의 이름입니다. *속성* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @value = ] 'value'`지정 된 속성의 새 값입니다. *value*는 **nvarchar (1000)** 이며 기본값은 없습니다.  
  
 다음 표에서는 아티클의 속성 및 해당 속성의 값을 설명합니다.  
  
|속성|값|Description|  
|--------------|-----------|-----------------|  
|**filter_type**|**1**|조인 필터입니다.<br /><br /> 이 옵션은 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자를 지원하는 데 필요합니다.|  
||**2**|논리적 레코드 관계입니다.|  
||**3**|조인 필터가 논리적 레코드 관계도 됩니다.|  
|**filtername**||필터의 이름입니다.|  
|**join_articlename**||조인 아티클의 이름입니다.|  
|**join_filterclause**||필터 절입니다.|  
|**join_unique_key**|**true**|조인이 고유 키에 있습니다.|  
||**false**|조인이 고유 키에 없습니다.|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`이 저장 프로시저가 수행한 동작으로 인해 기존 스냅숏이 무효화 될 수 있음을 승인 합니다. *force_invalidate_snapshot* 은 **bit**이며 기본값은 **0**입니다.  
  
 **0** 은 병합 아티클에 대 한 변경으로 인해 스냅숏이 무효화 되지 않도록 지정 합니다. 저장 프로시저가 새 스냅샷을 필요로 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 병합 아티클에 대 한 변경으로 인해 스냅숏이 무효화 될 수 있음을 의미 하며, 새 스냅숏이 필요한 기존 구독이 있는 경우 기존 스냅숏이 사용 되지 않는 것으로 표시 되 고 새 스냅숏으로 생성 될 수 있는 권한을 부여 합니다.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`이 저장 프로시저가 수행한 동작으로 인해 기존 구독을 다시 초기화 해야 할 수도 있습니다. *force_reinit_subscription* 은 **bit** 이며 기본값은 **0**입니다.  
  
 **0** 은 병합 아티클에 대 한 변경으로 인해 구독이 다시 초기화 되지 않도록 지정 합니다. 저장 프로시저가 기존 구독을 다시 초기화해야 하는 변경을 감지하면 오류가 발생하며 변경이 수행되지 않습니다.  
  
 **1** 은 병합 아티클에 대 한 변경으로 인해 기존 구독이 다시 초기화 됨을 의미 하며 구독을 다시 초기화할 수 있는 권한을 부여 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changemergefilter** 는 병합 복제에 사용 됩니다.  
  
 병합 아티클의 필터를 변경하려면 스냅샷이 하나 있는 경우 이를 다시 만들어야 합니다. 이는 ** \@force_invalidate_snapshot** **1**로 설정 하 여 수행 됩니다. 또한 이 아티클에 대한 구독이 있을 경우 구독을 다시 초기화해야 합니다. 이 작업은 ** \@force_reinit_subscription** **1**로 설정 하 여 수행 합니다.  
  
 논리적 레코드를 사용하려면 게시 및 아티클이 여러 가지 요구 사항을 만족해야 합니다. 자세한 내용은 [논리적 레코드를 사용하여 관련된 행의 변경 내용 그룹화](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_changemergefilter**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Transact-sql&#41;sp_addmergefilter &#40;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [Transact-sql&#41;sp_dropmergefilter &#40;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [Transact-sql&#41;sp_helpmergefilter &#40;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
