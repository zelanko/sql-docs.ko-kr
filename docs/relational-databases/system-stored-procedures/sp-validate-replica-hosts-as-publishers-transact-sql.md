---
title: sp_validate_replica_hosts_as_publishers (T-sql)
description: 모든 보조 복제본의 유효성을 검사할 수 있도록 하는 sp_validate_replica_hosts_as_publishers 저장 프로시저에 대해 설명 합니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validate_replica_hosts_as_publishers_TSQL
- sp_validate_replica_hosts_as_publishers
helpviewer_keywords:
- sp_validate_replica_hosts_as_publishers
ms.assetid: 45001fc9-2dbd-463c-af1d-aa8982d8c813
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9375be2a2af2b7653b3f0f036405533f1571ff3f
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75320011"
---
# <a name="sp_validate_replica_hosts_as_publishers-transact-sql"></a>sp_validate_replica_hosts_as_publishers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **sp_validate_replica_hosts_as_publishers** 은 현재 주 복제본 뿐만 아니라 모든 보조 복제본의 유효성을 검사할 수 있는 **sp_validate_redirected_publisher** 의 확장입니다. **sp_validate_replicat_hosts_as_publisher** 는 전체 Always On 복제 토폴로지의 유효성을 검사 합니다. 이중 홉 보안 오류 (21892)를 방지 하기 위해 원격 데스크톱 세션을 사용 하 여 배포자에서 직접 **sp_validate_replica_hosts_as_publishers** 를 실행 해야 합니다.  
  
 ![토픽 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-sql 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_validate_replica_hosts_as_publishers   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>인수  
`[ @original_publisher = ] 'original_publisher'`원래 데이터베이스를 게시 한 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이름입니다. *original_publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시 되는 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @redirected_publisher = ] 'redirected_publisher'`원래 게시자/게시 된 데이터베이스 쌍에 대해 **sp_redirect_publisher** 가 호출 된 경우의 리디렉션 대상입니다. *redirected_publisher* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 게시자 및 게시 데이터베이스에 대 한 항목이 없는 경우 **sp_validate_redirected_publisher** 는 출력 매개 변수 * \@redirected_publisher*에 대해 null을 반환 합니다. 그렇지 않고 게시자 및 게시 데이터베이스에 대한 항목이 있는 경우에는 성공 및 실패 모두에 대해 연결된 리디렉션된 게시자가 반환됩니다.  
  
 유효성 검사가 성공 하면 **sp_validate_redirected_publisher** 는 성공 표시를 반환 합니다.  
  
 유효성 검사에 실패한 경우에는 해당 오류가 발생합니다.  **sp_validate_redirected_publisher** 는 처음에 발생 한 것이 아니라 모든 문제를 발생 시키기 위한 최상의 노력을 합니다.  
  
> [!NOTE]  
>  읽기 액세스를 허용 하지 않거나 읽기 전용을 지정 해야 하는 보조 복제본 호스트의 유효성을 검사할 때 다음 오류가 발생 하 여 **sp_validate_replica_hosts_as_publishers** 실패 합니다.  
>   
>  메시지 21899, 수준 11, 상태 1, 프로시저 **sp_hadr_verify_subscribers_at_publisher**, 줄 109  
>   
>  '976' 오류로 인해 리디렉션된 게시자 'MyReplicaHostName'에서 원래 게시자 'MyOriginalPublisher'의 구독자에 대한 sysserver 항목이 있는지 확인하기 위한 쿼리에 실패했습니다(오류 메시지 '오류 976, 수준 14, 상태 1, 메시지: 대상 데이터베이스 'MyPublishedDB'이(가) 가용성 그룹에 참여 중이며 현재 쿼리로 액세스할 수 없습니다. 데이터 이동이 일시 중지되었거나 가용성 복제본이 읽기 액세스로 설정되지 않았습니다. 이 데이터베이스 및 가용성 그룹 내 다른 데이터베이스에 읽기 전용 액세스를 허용하려면 그룹 내 하나 이상의 보조 가용성 복제본에 읽기 액세스를 설정하세요.  자세한 내용은 **온라인 설명서의** ALTER AVAILABILITY GROUP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문을 참조하세요.'.  
>   
>  복제본 호스트 'MyReplicaHostName'에 대해 하나 이상의 게시자 유효성 검사 오류가 발생했습니다.  
  
## <a name="permissions"></a>권한  
 호출자는 **sysadmin** 고정 서버 역할의 멤버 이거나 배포 데이터베이스에 대 한 **db_owner** 고정 데이터베이스 역할의 멤버 이거나 게시자 데이터베이스에 연결 된 정의 된 게시에 대 한 게시 액세스 목록의 멤버 여야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;를 &#40;하는 복제 저장 프로시저](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_get_redirected_publisher &#40;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [Transact-sql&#41;sp_redirect_publisher &#40;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [Transact-sql&#41;sp_validate_redirected_publisher &#40;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)  
  
  
