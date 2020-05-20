---
title: sp_get_redirected_publisher (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 55a0c2509a52bb77a4f8ea9779210dac27bc86db
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820425"
---
# <a name="sp_get_redirected_publisher-transact-sql"></a>sp_get_redirected_publisher(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  복제 에이전트에서 배포자를 쿼리하여 원래 게시자가 리디렉션되었는지 여부를 확인하는 데 사용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_get_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @bypass_publisher_validation = ] [0 | 1 ]  
```  
  
## <a name="arguments"></a>인수  
`[ @original_publisher = ] 'original_publisher'`원래 데이터베이스를 게시 한 SQL Server의 인스턴스 이름입니다. *original_publisher* 는 **sysname**이며 기본값은 없습니다.
  
`[ @publisher_db = ] 'publisher_db'`게시 되는 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @bypass_publisher_validation = ] [0 | 1 ]`리디렉션된 게시자의 유효성 검사를 무시 하는 데 사용 됩니다. 0 인 경우 유효성 검사가 수행 됩니다. 1인 경우 유효성 검사가 수행되지 않습니다. *bypass_publisher_validation* 은 **bit**이며 기본값은 0입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**redirected_publisher**|**sysname**|리디렉션 후의 게시자 이름입니다.|  
|**error_number**|**int**|유효성 검사 오류의 오류 번호입니다.|  
|**error_severity**|**int**|유효성 검사 오류의 심각도입니다.|  
|**error_message**|**nvarchar(4000)**|유효성 검사 오류 메시지의 텍스트입니다.|  
  
## <a name="remarks"></a>설명  
 *redirected_publisher* 현재 게시자 이름을 반환 합니다. 게시자 및 게시 데이터베이스가 **sp_redirect_publisher**를 사용 하 여 리디렉션되지 않으면 null을 반환 합니다.  
  
 유효성 검사가 요청 되지 않았거나 게시자 및 게시 데이터베이스에 대 한 항목이 존재 하지 않는 경우 *error_number* 및 *error_severity* 0을 반환 하 고 *error_message* 는 null을 반환 합니다.  
  
 유효성 검사가 요청 되 면 [&#40;transact-sql&#41;sp_validate_redirected_publisher](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md) 유효성 검사 저장 프로시저를 호출 하 여 리디렉션 대상이 게시 데이터베이스에 적합 한 호스트 인지 확인 합니다. 유효성 검사에 성공 하면 **sp_get_redirected_publisher** 는 리디렉션된 게시자 이름을 반환 하 고, *error_number* 및 *error_severity* 열에 대해 0을 반환 하 고, *error_message* 열에 null을 반환 합니다.  
  
 요청된 유효성 검사에 실패한 경우에는 리디렉션된 게시자 이름이 오류 정보와 함께 반환됩니다.  
  
## <a name="permissions"></a>사용 권한  
 호출자는 **sysadmin** 고정 서버 역할의 멤버 이거나 배포 데이터베이스에 대 한 **db_owner** 고정 데이터베이스 역할의 멤버 이거나 게시자 데이터베이스에 연결 된 정의 된 게시에 대 한 게시 액세스 목록의 멤버 여야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;를 &#40;하는 복제 저장 프로시저](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_validate_redirected_publisher &#40;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [Transact-sql&#41;sp_redirect_publisher &#40;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [Transact-sql&#41;sp_validate_replica_hosts_as_publishers &#40;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
