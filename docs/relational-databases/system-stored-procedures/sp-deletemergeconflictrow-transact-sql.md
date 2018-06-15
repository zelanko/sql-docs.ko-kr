---
title: sp_deletemergeconflictrow (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sp_deletemergeconflictrow
- sp_deletemergeconflictrow_TSQL
helpviewer_keywords:
- sp_deletemergeconflictrow
ms.assetid: 64cf1186-28b8-4cd9-88f1-a7808a9c8d60
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 971d7dcce23ed908e5bd880da1f96681be6ad88c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32989552"
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
 충돌 테이블의 이름입니다. *conflict_table* 은 **sysname**, 기본값은 **%** 합니다. 경우는 *conflict_table* NULL로 지정 되어 또는 **%**, 삭제 충돌 하 고 일치 하는 행이 되도록 간주 되며 *rowguid* 및 *origin_datasource* 및 *source_object* 에서 삭제 되는 [MSmerge_conflicts_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) 테이블입니다.  
  
 [  **@source_object=**] **'***source_object***'**  
 원본 테이블의 이름입니다. *source_object* 은 **nvarchar (386)**, 기본값은 NULL입니다.  
  
 [  **@rowguid =**] **'***rowguid***'**  
 삭제 충돌에 대한 행 식별자입니다. *rowguid* 은 **uniqueidentifier**, 기본값은 없습니다.  
  
 [  **@origin_datasource=**] **'***origin_datasource***'**  
 충돌이 발생한 곳입니다. *origin_datasource* 은 **varchar (255)**, 기본값은 없습니다.  
  
 [  **@drop_table_if_empty=**] **'***drop_table_if_empty***'**  
 가 있음을 나타내는 플래그는 *conflict_table* 삭제 하는 경우에 비어 있습니다. *drop_table_if_empty* 은 **varchar (10)**, 기본값은 FALSE입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_deletemergeconflictrow** 병합 복제에 사용 됩니다.  
  
 [MSmerge_conflicts_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) 테이블은 시스템 테이블 및 비어 있는 경우에 데이터베이스에서 삭제 되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_deletemergeconflictrow**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
