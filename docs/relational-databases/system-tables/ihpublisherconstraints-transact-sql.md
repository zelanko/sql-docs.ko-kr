---
title: IHpublisherconstraints (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublisherconstraints
- IHpublisherconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherconstraints system table
ms.assetid: 537b1e1a-7228-4680-aa27-5ad7072ea01e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 44987e1b610483e6ce3cbca26c1efb8a1ef4c241
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67990255"
---
# <a name="ihpublisherconstraints-transact-sql"></a>IHpublisherconstraints(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublisherconstraints** 시스템 테이블은 현재 배포자를 사용 하 여 SQL Server 이외 게시자에서 복제 된 각 제약 조건에 대해 하나의 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisherconstraint_id**|**int**|게시된 제약 조건을 식별합니다.|  
|**table_id**|**int**|제약 조건이 속한 [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) 에서 테이블을 식별 합니다.|  
|**publisher_id**|**smallint**|열이 게시되는 SQL Server 이외 게시자를 식별합니다.|  
|**이름**|**Sysname 이며**|게시된 제약 조건의 이름입니다.|  
|**Type**|**nvarchar(255)**|[IHconstrainttypes](../../relational-databases/system-tables/ihconstrainttypes-transact-sql.md) 시스템 테이블에서 지원 되는 제약 조건 유형입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
