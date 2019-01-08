---
title: sp_publication_validation (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8612b3713113435461ca59845710b9f7284f1a78
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591407"
---
# <a name="sppublicationvalidation-transact-sql"></a>sp_publication_validation(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 게시에서 각 아티클에 대한 아티클 유효성 검사 요청을 시작합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_publication_validation [ @publication = ] 'publication'  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
 [**@publication=**] **'**_게시 '_  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [**@rowcount_only=**] *rowcount_only*  
 테이블에 대해 행 개수만 반환할 것인지 여부입니다. *rowcount_only* 됩니다 **smallint** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 호환 체크섬을 수행합니다.<br /><br /> 참고: 아티클이 행 필터링되면 체크섬 작업 대신 행 개수 작업이 수행됩니다.|  
|**1** (기본값)|행 개수 검사만 수행합니다.|  
|**2**|행 개수와 이진 체크섬을 수행합니다.<br /><br /> 참고: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 7.0 구독자에 대해서는 행 개수 유효성 검사만 수행합니다.|  
  
 [**@full_or_fast=**] *full_or_fast*  
 행 개수를 계산하는 데 사용하는 방법입니다. *full_or_fast* 됩니다 **tinyint** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|COUNT(*)를 사용하여 전체 개수를 계산합니다.|  
|**1**|빠른 계산 **sysindexes.rows**합니다. 사용한 행 계산은 [sys.sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) 실제 테이블의 행 계산 보다 훨씬 빠릅니다. 그러나 때문 [sys.sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) 는 느리게 업데이트 행 개수가 정확 하지 않을 합니다.|  
|**2** (기본값)|먼저 빠른 방법을 시도함으로써 조건부로 빠른 계산 방법을 수행합니다. 빠른 방법의 결과에 차이점이 있는 경우 전체 방법으로 전환합니다. 하는 경우 *expected_rowcount* 가 NULL이 저장된 프로시저 되 고 값을 가져오려면, 전체 그룹은 항상 사용 합니다.|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 유효성 검사가 종료되면 배포 에이전트가 즉시 종료되어야 하는지 여부입니다. *shutdown_agent* 됩니다 **비트**, 기본값은 **0**합니다. 하는 경우 **0**, 복제 에이전트가 종료 되지 않습니다. 하는 경우 **1**, 마지막 아티클의 유효성을 검사 한 후 복제 에이전트가 종료 되었습니다.  
  
 [ **@publisher** =] **'**_게시자_**'**  
 지정 된 비- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 해서는 안에서 유효성 검사를 요청할 때를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_publication_validation** 트랜잭션 복제에 사용 됩니다.  
  
 **sp_publication_validation** 게시와 연관 된 아티클이 활성화 된 후 언제 든 지 호출할 수 있습니다. 프로시저는 수동으로 한 번 실행하거나 데이터의 유효성을 검사하는 예정된 작업의 일부로 정기적으로 실행할 수 있습니다.  
  
 응용 프로그램에 즉시 업데이트 구독자가 있으면 **sp_publication_validation** 의사 오류를 발견할 수 있습니다. **sp_publication_validation** 먼저 행 개수 또는 체크섬 게시자 및 구독자에서 다음을 계산 합니다. 즉시 업데이트 트리거는 행 개수 또는 체크섬이 게시자에서 완료된 다음에 구독자의 업데이트를 게시자로 전파할 수 있으므로 행 개수 또는 체크섬이 구독자에서 완료되기 전에 값을 변경할 수 있습니다. 게시의 유효성을 검사하는 동안 구독자 및 게시자에서 값이 변경되지 않았는지 확인하려면 유효성 검사 동안 게시자에서 MS DTC(Microsoft Distributed Transaction Coordinator) 서비스를 중지하십시오.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_publication_validation**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [구독자에서 데이터 유효성 검사](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_article_validation &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_table_validation &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
