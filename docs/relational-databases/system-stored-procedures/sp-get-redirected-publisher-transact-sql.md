---
title: sp_get_redirected_publisher (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_get_redirected_publisher_TSQL
- sp_get_redirected_publisher
ms.assetid: d47a9ab5-f2cc-42a8-8be9-a33895ce44f0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 49bffb24c5ddc45c1c6b88fb424ab419445819fb
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529970"
---
# <a name="spgetredirectedpublisher-transact-sql"></a>sp_get_redirected_publisher(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  복제 에이전트에서 배포자를 쿼리하여 원래 게시자가 리디렉션되었는지 여부를 확인하는 데 사용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_get_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @bypass_publisher_validation = ] [0 | 1 ]  
```  
  
## <a name="arguments"></a>인수  
`[ @original_publisher = ] 'original_publisher'` 게시 데이터베이스의 이름입니다. *publisher_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시 데이터베이스의 이름입니다. *publisher_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @bypass_publisher_validation = ] [0 | 1 ]` 리디렉션된 게시자의 유효성 검사를 무시 하는 데 사용 합니다. 0 인 경우 유효성 검사가 수행 됩니다. 1인 경우 유효성 검사가 수행되지 않습니다. *bypass_publisher_validation* 됩니다 **비트**, 기본값은 0입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**redirected_publisher**|**sysname**|리디렉션 후의 게시자 이름입니다.|  
|**error_number**|**int**|유효성 검사 오류의 오류 번호입니다.|  
|**error_severity**|**int**|유효성 검사 오류의 심각도입니다.|  
|**error_message**|**nvarchar(4000)**|유효성 검사 오류 메시지의 텍스트입니다.|  
  
## <a name="remarks"></a>Remarks  
 *redirected_publisher* 현재 게시자 이름을 반환 합니다. 게시자 및 게시 데이터베이스가 리디렉션되지 않은 사용 하는 경우 null을 반환 합니다 **sp_redirect_publisher**합니다.  
  
 유효성 검사는 요청 되지 않은 경우 또는 게시자와 게시 데이터베이스에 대 한 항목이 없는 경우 *error_number* 하 고 *error_severity* 0을 반환 하 고 *error_message* null을 반환합니다.  
  
 유효성 검사 저장 프로시저 유효성 검사 요청 되 면 [sp_validate_redirected_publisher &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md) 리디렉션의 대상 게시에 적합 한 호스트 인지 확인 하기 위해 호출 됩니다 데이터베이스입니다. 유효성 검사에 성공 하면 **sp_get_redirected_publisher** 리디렉션된 게시자 이름, 0을 반환 합니다 *error_number* 하 고 *error_severity* 열 및 null 합니다 *error_message* 열입니다.  
  
 요청된 유효성 검사에 실패한 경우에는 리디렉션된 게시자 이름이 오류 정보와 함께 반환됩니다.  
  
## <a name="permissions"></a>사용 권한  
 호출자 여야의 멤버는 **sysadmin** 고정 서버 역할을 **db_owner** 정의 된 게시에 대 한 게시 액세스 목록의 멤버 또는 배포 데이터베이스에 대 한 고정된 데이터베이스 역할 게시자 데이터베이스를 사용 하 여 연결 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
