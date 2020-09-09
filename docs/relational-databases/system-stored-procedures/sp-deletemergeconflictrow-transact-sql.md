---
description: sp_deletemergeconflictrow(Transact-SQL)
title: sp_deletemergeconflictrow (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletemergeconflictrow
- sp_deletemergeconflictrow_TSQL
helpviewer_keywords:
- sp_deletemergeconflictrow
ms.assetid: 64cf1186-28b8-4cd9-88f1-a7808a9c8d60
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4b2fae5fad15490fee5c239a26e8e0b5e0a25832
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543539"
---
# <a name="sp_deletemergeconflictrow-transact-sql"></a>sp_deletemergeconflictrow(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  충돌 테이블 또는 [MSmerge_conflicts_info &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) 테이블에서 행을 삭제 합니다. 이 저장 프로시저는 충돌 테이블이 저장된 컴퓨터의 모든 데이터베이스에서 실행될 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_deletemergeconflictrow [ [ @conflict_table = ] 'conflict_table' ]  
    [ , [ @source_object = ] 'source_object' ]  
    { , [ @rowguid = ] 'rowguid'  
        , [ @origin_datasource = ] 'origin_datasource' ] }  
    [ , [ @drop_table_if_empty = ] 'drop_table_if_empty' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @conflict_table = ] 'conflict_table'` 충돌 테이블의 이름입니다. *conflict_table* 는 **sysname**이며 기본값은 **%** 입니다. *CONFLICT_TABLE* NULL 또는로 지정 된 경우 **%** 충돌은 삭제 충돌로 간주 되며 *rowguid* 와 *origin_datasource* 및 *Source_object* 일치 하는 행이 [MSmerge_conflicts_info &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) 테이블에서 삭제 됩니다.  
  
`[ @source_object = ] 'source_object'` 원본 테이블의 이름입니다. *source_object* 은 **nvarchar (386)** 이며 기본값은 NULL입니다.  
  
`[ @rowguid = ] 'rowguid'` 삭제 충돌에 대 한 행 식별자입니다. *rowguid* 는 **uniqueidentifier**이며 기본값은 없습니다.  
  
`[ @origin_datasource = ] 'origin_datasource'` 충돌의 원점입니다. *origin_datasource* 는 **varchar (255)** 이며 기본값은 없습니다.  
  
`[ @drop_table_if_empty = ] 'drop_table_if_empty'` 가 비어 있는 경우 *conflict_table* 삭제 됨을 나타내는 플래그입니다. *drop_table_if_empty* 는 **varchar (10)** 이며 기본값은 FALSE입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_deletemergeconflictrow** 는 병합 복제에 사용 됩니다.  
  
 [MSmerge_conflicts_info &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md) 테이블은 비어 있어도 데이터베이스에서 삭제 되지 않고 시스템 테이블입니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_deletemergeconflictrow**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
