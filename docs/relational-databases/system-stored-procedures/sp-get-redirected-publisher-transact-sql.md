---
title: sp_get_redirected_publisher (Transact SQL) | Microsoft Docs
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
- sp_get_redirected_publisher_TSQL
- sp_get_redirected_publisher
ms.assetid: d47a9ab5-f2cc-42a8-8be9-a33895ce44f0
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 28785969ea0bab2319d52461aa3e9a60f9be916d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32994990"
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
 [ **@original_publisher** =] **'***original_publisher***'**  
 게시할 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 게시할 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@bypass_publisher_validation** = ] [0 | 1 ]  
 리디렉션된 게시자의 유효성 검사를 무시하는 데 사용됩니다. 0 인 경우, 유효성 검사가 수행 됩니다. 1인 경우 유효성 검사가 수행되지 않습니다. *bypass_publisher_validation* 은 **비트**, 기본값은 0입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**redirected_publisher**|**sysname**|리디렉션 후의 게시자 이름입니다.|  
|**error_number**|**int**|유효성 검사 오류의 오류 번호입니다.|  
|**error_severity**|**int**|유효성 검사 오류의 심각도입니다.|  
|**error_message**|**nvarchar(4000)**|유효성 검사 오류 메시지의 텍스트입니다.|  
  
## <a name="remarks"></a>주의  
 *redirected_publisher* 현재 게시자 이름을 반환 합니다. 게시자 및 게시 데이터베이스가 리디렉션되지 않은 사용 하는 경우 null을 반환 **sp_redirect_publisher**합니다.  
  
 유효성 검사가 요청 되지 또는 게시자 및 게시 데이터베이스에 대 한 항목이 없는 경우 *error_number* 및 *error_severity* 0을 반환 하 고 *error_message* null을 반환합니다.  
  
 유효성 검사 저장 프로시저 유효성 검사를 요청한 경우 [sp_validate_redirected_publisher &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md) 리디렉션 대상이 게시에 적합 한 호스트 인지 확인 하기 위해 호출 데이터베이스입니다. 유효성 검사에 성공한 경우 **sp_get_redirected_publisher** 0에 대 한 리디렉션된 게시자 이름을 반환 된 *error_number* 및 *error_severity* 열 및에 null *error_message* 열입니다.  
  
 요청된 유효성 검사에 실패한 경우에는 리디렉션된 게시자 이름이 오류 정보와 함께 반환됩니다.  
  
## <a name="permissions"></a>Permissions  
 호출자 이어야 합니다.의 멤버는 **sysadmin** 고정 서버 역할의 **db_owner** 정의 된 게시에 대 한 게시 액세스 목록의 멤버 또는 배포 데이터베이스에 대 한 고정된 데이터베이스 역할 데이터베이스에 연결 된 게시자입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
