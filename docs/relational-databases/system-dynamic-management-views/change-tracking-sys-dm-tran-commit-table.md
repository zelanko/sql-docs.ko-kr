---
title: sys.dm_tran_commit_table (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_tran_commit_table
- dm_tran_commit_table_TSQL
- sys.dm_tran_commit_table
- sys.dm_tran_commit_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_commit_table dynamic management view
ms.assetid: 732d23c5-1f6c-4e96-bc85-8f29b520cf0e
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 17e42e8bf81db76b3034c6bf1e2e0111a6fc9671
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="change-tracking---sysdmtrancommittable"></a>변경 내용 추적-sys.dm_tran_commit_table
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변경 내용 추적에서 추적된 테이블에 대해 커밋한 각 트랜잭션을 한 행으로 표시합니다. Sys.dm_tran_commit_table 관리 뷰 지원 가능성을 위해 제공 되 고 변경 내용 추적 되는 트랜잭션 관련 정보를 표시 하는 sys.syscommittab 시스템 테이블에 저장 합니다. sys.syscommittab 테이블에서는 데이터베이스별 트랜잭션 ID를 트랜잭션의 커밋 LSN(로그 시퀀스 번호) 및 커밋 타임스탬프에 지속적으로 매핑하는 효과적인 방법을 제공합니다. sys.syscommittab 테이블에 저장되고 이 관리 뷰에 표시되는 데이터는 변경 내용 추적을 구성할 때 지정한 보존 기간에 따라 정리될 수 있습니다.  
  
> [!NOTE]  
>  이 메서드를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 또는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_tran_commit_table**합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|commit_ts|**bigint**|커밋된 각 트랜잭션의 데이터베이스별 타임스탬프 역할을 하는 단계적으로 늘어나는 숫자입니다.|  
|xdes_id|**bigint**|트랜잭션의 데이터베이스별 내부 ID입니다.|  
|commit_lbn|**bigint**|트랜잭션의 커밋 로그 레코드를 포함하는 로그 블록 수입니다.|  
|commit_csn|**bigint**|트랜잭션의 인스턴스별 커밋 시퀀스 번호입니다.|  
|commit_time|**smalldatetime**|트랜잭션이 커밋된 시간입니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [변경 내용 추적 정보&#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
  


