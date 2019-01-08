---
title: sp_mergearticlecolumn (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergearticlecolumn
- sp_mergearticlecolumn_TSQL
helpviewer_keywords:
- sp_mergearticlecolumn
ms.assetid: b4f2b888-e094-4759-a472-d893638995eb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d28c8da014a3922a9dbd1cba533b4cbf1d7a9215
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590077"
---
# <a name="spmergearticlecolumn-transact-sql"></a>sp_mergearticlecolumn(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 게시를 열로 분할합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_mergearticlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column'  
    [ , [ @operation = ] 'operation'   
    [ , [ @schema_replication = ] 'schema_replication' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]   
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]   
```  
  
## <a name="arguments"></a>인수  
 [  **@publication =**] **'**_게시_**'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@article =**] **'**_문서_**'**  
 게시에 있는 아티클의 이름입니다. *문서* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@column =**] **'**_열_**'**  
 수직 분할을 만들 열을 식별합니다. *열* 됩니다 **sysname**, 기본값은 NULL입니다. NULL 및 `@operation = N'add'`일 경우 원본 테이블의 모든 열이 기본적으로 아티클에 추가됩니다. *열* 인 경우 NULL 일 수 없습니다 *작업이* 로 설정 되어 **drop**합니다. 아티클에서 열을 제외 하려면 실행 **sp_mergearticlecolumn** 지정 *열* 하 고 `@operation = N'drop'` 제거할 각 열에 대해 지정 된 *문서*.  
  
 [  **@operation =**] **'**_작업이_**'**  
 복제 상태입니다. *작업이* 됩니다 **nvarchar(4)**, 기본값은 ADD 사용 하 여 합니다. **추가** 복제에 대 한 열을 표시 합니다. **drop** 열을 지웁니다.  
  
 [  **@schema_replication=**] **'**_schema_replication_**'**  
 병합 에이전트가 실행될 때 스키마 변경 내용이 전파되도록 지정합니다. *schema_replication* 됩니다 **nvarchar(5)**, 기본값은 FALSE입니다.  
  
> [!NOTE]  
>  만 **FALSE** 지원 됩니다 *schema_replication*합니다.  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 스냅숏 무효화 기능을 설정하거나 해제합니다. *force_invalidate_snapshot* 되는 **비트**, 기본값은 **0**합니다.  
  
 **0** 병합 아티클에 대 한 변경 인해 스냅숏이 무효화 되지 않도록 지정 합니다.  
  
 **1** 은 병합 아티클의 변경이을 유효 하지 않게 스냅숏을 무효화를 지정 하는 경우, 값 및 **1** 새 스냅숏 발생에 대 한 사용 권한을 부여 합니다.  
  
 [  **@force_reinit_subscription =]**_force_reinit_subscription_  
 구독 다시 초기화 기능을 설정하거나 해제합니다. *force_reinit_subscription* 은 bit 이며 기본값은 **0**합니다.  
  
 **0** 병합 아티클에 대 한 변경 인해 구독이 다시 초기화 되지 않도록 지정 합니다.  
  
 **1** 아티클의 병합 아티클에 대 한 변경 될 수 있습니다 구독 다시 초기화 해야 하는 경우, 값 및 **1** 구독을 다시 초기화할 수 있는 권한을 부여 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_mergearticlecolumn** 병합 복제에 사용 됩니다.  
  
 자동 ID 범위 관리가 사용되는 경우 아티클에서 ID 열을 삭제할 수 없습니다. 자세한 내용은 [ID 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)를 참조하세요.  
  
 초기 스냅숏이 생성된 후에 응용 프로그램이 새로운 수직 분할을 설정한 경우 새로운 스냅숏을 생성하여 각 구독에 다시 적용해야 합니다. 스냅숏은 예약된 다음 스냅숏과 배포 또는 병합 에이전트가 실행될 때 적용됩니다.  
  
 충돌 감지에 행 추적을 사용하는 경우(기본값) 기본 테이블에 최대 1,024개의 열을 포함할 수 있지만 아티클에서 열을 필터링해야 하므로 최대 246개의 열이 게시됩니다. 열 추적을 사용하면 기본 테이블은 최대 246개의 열을 포함할 수 있습니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-mergearticlecolumn-tr_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_mergearticlecolumn**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [병합 아티클 사이에서 조인 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [게시된 데이터 필터링](../../relational-databases/replication/publish/filter-published-data.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
