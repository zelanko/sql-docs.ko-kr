---
description: sp_publication_validation(Transact-SQL)
title: sp_publication_validation (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publication_validation
- sp_publication_validation_TSQL
helpviewer_keywords:
- sp_publication_validation
ms.assetid: 06be2363-00c0-4936-97c1-7347f294a936
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dccdb0f168b7b1e113a38c64a111e35e5bf62d77
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535010"
---
# <a name="sp_publication_validation-transact-sql"></a>sp_publication_validation(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  지정된 게시에서 각 아티클에 대한 아티클 유효성 검사 요청을 시작합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_publication_validation [ @publication = ] 'publication'  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @rowcount_only = ] 'rowcount_only'` 테이블에 대 한 행 개수만 반환 하는지 여부입니다. *rowcount_only* 은 **smallint** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 호환 체크섬을 수행합니다.<br /><br /> 참고: 아티클이 행 필터링 되 면 체크섬 작업 대신 행 개수 연산이 수행 됩니다.|  
|**1** (기본값)|행 개수 검사만 수행합니다.|  
|**2**|행 개수와 이진 체크섬을 수행합니다.<br /><br /> 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 7.0 구독자의 경우 행 개수 유효성 검사만 수행 됩니다.|  
  
`[ @full_or_fast = ] 'full_or_fast'` 행 개수를 계산 하는 데 사용 되는 방법입니다. *full_or_fast* 은 **tinyint** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|COUNT(*)를 사용하여 전체 개수를 계산합니다.|  
|**1**|는 **sysindexes 행**에서 빠르게 계산 합니다. [sys.sys인덱스](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) 의 행 수를 계산 하는 것은 실제 테이블의 행 수를 계산 하는 것 보다 훨씬 빠릅니다. 그러나 [sys.sys인덱스](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) 는 지연 업데이트 되므로 행 개수가 정확 하지 않을 수 있습니다.|  
|**2** (기본값)|먼저 빠른 방법을 시도함으로써 조건부로 빠른 계산 방법을 수행합니다. 빠른 방법의 결과에 차이점이 있는 경우 전체 방법으로 전환합니다. *Expected_rowcount* 가 NULL이 고 저장 프로시저를 사용 하 여 값을 가져오는 경우에는 항상 전체 개수 (*)가 사용 됩니다.|  
  
`[ @shutdown_agent = ] 'shutdown_agent'` 유효성 검사가 완료 되 면 즉시 배포 에이전트 종료 해야 하는지 여부입니다. *shutdown_agent* 은 **bit**이며 기본값은 **0**입니다. **0**인 경우 복제 에이전트가 종료 되지 않습니다. **1**인 경우 마지막 아티클의 유효성을 검사 한 후 복제 에이전트가 종료 됩니다.  
  
`[ @publisher = ] 'publisher'` 이외 게시자를 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  게시자에 대 한 유효성 검사를 요청할 때는 *게시자* 를 사용 하면 안 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_publication_validation** 은 트랜잭션 복제에 사용 됩니다.  
  
 **sp_publication_validation** 는 게시와 연결 된 아티클이 활성화 된 후 언제 든 지 호출할 수 있습니다. 프로시저는 수동으로 한 번 실행하거나 데이터의 유효성을 검사하는 예정된 작업의 일부로 정기적으로 실행할 수 있습니다.  
  
 응용 프로그램에 즉시 업데이트 하는 구독자가 있는 경우 **sp_publication_validation** 는 의사 오류를 감지할 수 있습니다. **sp_publication_validation** 는 먼저 게시자에서 행 개수 또는 체크섬을 계산한 다음 구독자에서 계산 합니다. 즉시 업데이트 트리거는 행 개수 또는 체크섬이 게시자에서 완료된 다음에 구독자의 업데이트를 게시자로 전파할 수 있으므로 행 개수 또는 체크섬이 구독자에서 완료되기 전에 값을 변경할 수 있습니다. 게시의 유효성을 검사하는 동안 구독자 및 게시자에서 값이 변경되지 않았는지 확인하려면 유효성 검사 동안 게시자에서 MS DTC(Microsoft Distributed Transaction Coordinator) 서비스를 중지하십시오.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_publication_validation**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [구독자에서 데이터 유효성 검사](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [Transact-sql&#41;sp_article_validation &#40;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [Transact-sql&#41;sp_table_validation &#40;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
