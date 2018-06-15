---
title: sp_redirect_publisher (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
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
- sp_redirect_publisher_TSQL
- sp_redirect_publisher
helpviewer_keywords:
- sp_redirect_publisher
ms.assetid: af45e2b2-57fb-4bcd-a58b-e61401fb3b26
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e8df59d709ef04d94626ac2ab6a3ba268d63ab76
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32999910"
---
# <a name="spredirectpublisher-transact-sql"></a>sp_redirect_publisher(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  기존 게시자/데이터베이스 쌍에 대한 리디렉션된 게시자를 지정합니다. 게시자 데이터베이스에는 Always On 가용성 그룹에 속한 경우 리디렉션된 게시자는 가용성 그룹에 연결 된 가용성 그룹 수신기 이름입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_redirect_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name'   
    [ , [ @redirected_publisher = ] 'new_publisher' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@original_publisher** =] **'***original_publisher***'**  
 원래 데이터베이스를 게시한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다. *original_publisher* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 게시할 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@redirected_publisher** =] **'***redirected_publisher***'**  
 새 게시자가 될 가용성 그룹과 연결된 가용성 그룹 수신기 이름입니다. *redirected_publisher* 은 **sysname**, 기본값은 없습니다. 가용성 그룹 수신기를 기본 포트가 아닌 다른 포트로 구성한 경우 `'Listenername,51433'`과 같이 포트 번호를 수신기 이름과 함께 지정합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 **sp_redirect_publisher** 복제 게시자는 가용성 그룹 수신기와 함께 게시자/데이터베이스 쌍을 연결 하 여 Always On 가용성 그룹의 현재 주 복제본으로 리디렉션될 수를 허용 하는 데 사용 됩니다. 실행 **sp_redirect_publisher** AG 수신기가 게시 된 데이터베이스를 포함 하는 가용성 그룹에 대해 구성 된 후입니다.  
  
 원래 게시자에서 게시 데이터베이스는 주 복제본에서 가용성 그룹에서 제거 되 면 실행 **sp_redirect_publisher** 에 대 한 값을 지정 하지 않고는 *@redirected_publisher* 게시자/데이터베이스 쌍에 대 한 리디렉션을 제거 하려면 매개 변수입니다. 게시자 리디렉션에 대 한 자세한 내용은 참조 하십시오 [AlwaysOn 게시 데이터베이스 유지 관리 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)합니다.  
  
## <a name="permissions"></a>Permissions  
 호출자 이어야 합니다.의 멤버는 **sysadmin** 고정 서버 역할의 **db_owner** 정의 된 게시에 대 한 게시 액세스 목록의 멤버 또는 배포 데이터베이스에 대 한 고정된 데이터베이스 역할 데이터베이스에 연결 된 게시자입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_get_redirected_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
