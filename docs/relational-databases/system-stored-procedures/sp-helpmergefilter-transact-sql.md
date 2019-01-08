---
title: sp_helpmergefilter (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3785eb45e8ecca7a573f499d8c48b184a22e6efc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52779365"
---
# <a name="sphelpmergefilter-transact-sql"></a>sp_helpmergefilter(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 필터에 관한 정보를 반환합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpmergefilter [ @publication= ] 'publication'   
    [ , [ @article= ] 'article']  
    [ , [ @filtername= ] 'filtername']  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication=**] **'***publication***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@article=**] **'***문서***'**  
 아티클의 이름입니다. *문서* 는 **sysname**, 기본값은 **%**, 모든 아티클의 이름을 반환 합니다.  
  
 [  **@filtername=**] **'***filtername***'**  
 정보를 반환할 필터의 이름입니다. *filtername* 됩니다 **sysname**, 기본값은 **%**, 아티클 또는 게시에서 정의 된 모든 필터에 대 한 정보를 반환 하는 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**join_filterid**|**int**|조인 필터 ID입니다.|  
|**filtername**|**sysname**|필터의 이름입니다.|  
|**조인 아티클 이름**|**sysname**|조인 아티클의 이름입니다.|  
|**join_filterclause**|**nvarchar(2000)**|조인을 한정하는 필터 절입니다.|  
|**join_unique_key**|**int**|고유 키에 조인이 설정되어 있는지를 지정합니다.|  
|**기본 테이블 소유자**|**sysname**|기본 테이블 소유자의 이름입니다.|  
|**기본 테이블 이름**|**sysname**|기본 테이블의 이름입니다.|  
|**조인 테이블 소유자**|**sysname**|기본 테이블에 조인되는 테이블 소유자의 이름입니다.|  
|**조인 테이블 이름**|**sysname**|기본 테이블에 조인되는 테이블의 이름입니다.|  
|**문서 이름**|**sysname**|기본 테이블에 조인되는 테이블 아티클의 이름입니다.|  
|**filter_type**|**tinyint**|병합 필터의 유형으로 다음 중 하나일 수 있습니다.<br /><br /> **1** = 조인 필터만<br /><br /> **2** = 논리적 레코드 관계<br /><br /> **3** = 모두|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpmergefilter** 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 및 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_helpmergefilter**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_addmergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
