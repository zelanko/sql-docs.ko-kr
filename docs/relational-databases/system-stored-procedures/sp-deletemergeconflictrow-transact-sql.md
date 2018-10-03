---
title: sp_deletemergeconflictrow (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_deletemergeconflictrow
- sp_deletemergeconflictrow_TSQL
helpviewer_keywords:
- sp_deletemergeconflictrow
ms.assetid: 64cf1186-28b8-4cd9-88f1-a7808a9c8d60
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fc1152ee4893991a207936c1a08dccc988fbde5a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670649"
---
# <a name="spdeletemergeconflictrow-transact-sql"></a>sp_deletemergeconflictrow(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  충돌 테이블에서 행을 삭제 또는 [MSmerge_conflicts_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) 테이블입니다. 이 저장 프로시저는 충돌 테이블이 저장된 컴퓨터의 모든 데이터베이스에서 실행될 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_deletemergeconflictrow [ [ @conflict_table = ] 'conflict_table' ]  
    [ , [ @source_object = ] 'source_object' ]  
    { , [ @rowguid = ] 'rowguid'  
        , [ @origin_datasource = ] 'origin_datasource' ] }  
    [ , [ @drop_table_if_empty = ] 'drop_table_if_empty' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@conflict_table=**] **'***conflict_table***'**  
 충돌 테이블의 이름입니다. *conflict_table* 됩니다 **sysname**, 기본값은 **%** 합니다. 경우는 *conflict_table* NULL로 지정 되어 또는 **%**, 충돌이 삭제 충돌 및 일치 하는 행으로 간주 됩니다 *rowguid* 및 *origin_datasource* 하 고 *source_object* 에서 삭제 되는 [MSmerge_conflicts_info &#40;Transact SQL&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) 테이블입니다.  
  
 [  **@source_object=**] **'***source_object***'**  
 원본 테이블의 이름입니다. *source_object* 됩니다 **nvarchar(386)**, 기본값은 NULL입니다.  
  
 [  **@rowguid =**] **'***rowguid***'**  
 삭제 충돌에 대한 행 식별자입니다. *rowguid* 됩니다 **uniqueidentifier**, 기본값은 없습니다.  
  
 [  **@origin_datasource=**] **'***origin_datasource***'**  
 충돌이 발생한 곳입니다. *origin_datasource* 됩니다 **varchar(255)**, 기본값은 없습니다.  
  
 [  **@drop_table_if_empty=**] **'***drop_table_if_empty***'**  
 가 나타내는 플래그를 *conflict_table* 경우 삭제할는 빈 합니다. *drop_table_if_empty* 됩니다 **varchar(10)**, 기본값은 FALSE입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_deletemergeconflictrow** 병합 복제에 사용 됩니다.  
  
 [MSmerge_conflicts_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) 테이블은 시스템 테이블 및 비어 있는 경우에 데이터베이스에서 삭제 되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_deletemergeconflictrow**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
