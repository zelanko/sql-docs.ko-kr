---
title: sp_validate_redirected_publisher (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_validate_redirected_publisher
- sp_validate_redirected_publisher_TSQL
helpviewer_keywords:
- sp_validate_redirected_publisher
ms.assetid: 2b7fdbad-17e4-4442-b0b2-9b5e8f84b91d
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 89bb592d13d395bff62a09668efb9a3d0ecae60c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37978945"
---
# <a name="spvalidateredirectedpublisher-transact-sql"></a>sp_validate_redirected_publisher(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  게시 데이터베이스의 현재 호스트가 복제를 지원할 수 있는지 확인합니다. 배포 데이터베이스에서 실행해야 합니다. 이 프로시저를 호출할 **sp_get_redirected_publisher**합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
      sp_validate_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>인수  
 [ **@original_publisher** =] **'***original_publisher***'**  
 원래 데이터베이스를 게시한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다. *original_publisher* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 게시할 데이터베이스의 이름입니다. *publisher_db* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [ **@redirected_publisher** =] **'***redirected_publisher***'**  
 리디렉션 대상입니다를 지정 하는 경우 **sp_redirect_publisher** 게시자/데이터베이스 쌍에 대해 호출 되었습니다. *redirected_publisher* 됩니다 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>Remarks  
 게시자와 게시 데이터베이스에 대 한 항목이 없는 경우 **sp_validate_redirected_publisher** 출력 매개 변수에 null을 반환 합니다 *@redirected_publisher*합니다. 항목이 있으면 성공한 경우와 실패한 경우 모두에 대해 해당 항목이 출력 매개 변수에 반환됩니다.  
  
 유효성 검사에 성공 하면 **sp_validate_redirected_publisher** 성공 표시를 반환 합니다.  
  
 유효성 검사에 실패한 경우에는 실패를 설명하는 오류가 발생합니다.  
  
## <a name="permissions"></a>사용 권한  
 호출자 여야의 멤버는 **sysadmin** 고정 서버 역할을 **db_owner** 정의 된 게시에 대 한 게시 액세스 목록의 멤버 또는 배포 데이터베이스에 대 한 고정된 데이터베이스 역할 게시자 데이터베이스를 사용 하 여 연결 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
