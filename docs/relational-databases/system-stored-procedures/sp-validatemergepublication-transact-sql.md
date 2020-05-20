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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6a0ca36329c8ddb68c9727fe1b9d2cf17674c93a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82808874"
---
# <a name="sp_validatemergepublication-transact-sql"></a>s sp_validatemergepublication(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  모든 구독(밀어넣기, 끌어오기 및 익명 구독)에 대해 한 번씩 유효성 검사를 하는 게시 차원의 유효성 검사를 수행합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_validatemergepublication [@publication=] 'publication'  
        , [ @level = ] level  
```  
  
## <a name="arguments"></a>인수  
 [** \@ 게시 =**] **'***게시***'**  
 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @level = ] level`수행할 유효성 검사의 유형입니다. *level* 은 **tinyint**이며 기본값은 없습니다. 수준은 다음 값 중 하나일 수 있습니다.  
  
|수준 값|Description|  
|-----------------|-----------------|  
|**1**|행 개수의 유효성만 검사합니다.|  
|**2**|행 개수 및 체크섬의 유효성을 검사합니다. 구독자의 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이는 자동으로 **3**으로 설정 됩니다.|  
|**3**|권장 값입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_validatemergepublication** 는 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_validatemergepublication**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [복제 된 데이터의 유효성 검사](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [Transact-sql&#41;sp_validatemergesubscription &#40;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md)  
  
  
