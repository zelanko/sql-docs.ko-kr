---
description: sp_helpmergefilter(Transact-SQL)
title: sp_helpmergefilter (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergefilter
- sp_helpmergefilter_TSQL
helpviewer_keywords:
- sp_helpmergefilter
ms.assetid: f133a094-0009-4771-b93b-e86a5c01e40b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: faa3b2922f8d73875b5213603b980560d69465ff
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89526994"
---
# <a name="sp_helpmergefilter-transact-sql"></a>sp_helpmergefilter(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  병합 필터에 관한 정보를 반환합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpmergefilter [ @publication= ] 'publication'   
    [ , [ @article= ] 'article']  
    [ , [ @filtername= ] 'filtername']  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'` 아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 **%** 모든 아티클의 이름을 반환 하는입니다.  
  
`[ @filtername = ] 'filtername'` 정보를 반환할 필터의 이름입니다. *filtername* 는 **sysname**이며 기본값은 **%** 아티클 또는 게시에 정의 된 모든 필터에 대 한 정보를 반환 하는입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**join_filterid**|**int**|조인 필터 ID입니다.|  
|**filtername**|**sysname**|필터의 이름입니다.|  
|**join article name**|**sysname**|조인 아티클의 이름입니다.|  
|**join_filterclause**|**nvarchar (2000)**|조인을 한정하는 필터 절입니다.|  
|**join_unique_key**|**int**|고유 키에 조인이 설정되어 있는지를 지정합니다.|  
|**base table owner**|**sysname**|기본 테이블 소유자의 이름입니다.|  
|**base table name**|**sysname**|기본 테이블의 이름입니다.|  
|**join table owner**|**sysname**|기본 테이블에 조인되는 테이블 소유자의 이름입니다.|  
|**join table name**|**sysname**|기본 테이블에 조인되는 테이블의 이름입니다.|  
|**article name**|**sysname**|기본 테이블에 조인되는 테이블 아티클의 이름입니다.|  
|**filter_type**|**tinyint**|병합 필터의 유형으로 다음 중 하나일 수 있습니다.<br /><br /> **1** = 조인 필터만<br /><br /> **2** = 논리적 레코드 관계<br /><br /> **3** = 모두|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpmergefilter** 는 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 및 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_helpmergefilter**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [sp_addmergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
