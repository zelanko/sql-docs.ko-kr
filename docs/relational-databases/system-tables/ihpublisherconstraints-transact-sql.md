---
title: IHpublisherconstraints (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
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
manager: craigg
ms.openlocfilehash: 8d924e432a45d900092be6e84ed110afd66951d6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47732531"
---
# <a name="ihpublisherconstraints-transact-sql"></a>IHpublisherconstraints(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **IHpublisherconstraints** 시스템 테이블에서 SQL Server 이외 게시자는 현재 배포자를 사용 하 여 복제 된 각 제약 조건에 대해 하나의 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisherconstraint_id**|**int**|게시된 제약 조건을 식별합니다.|  
|**table_id**|**int**|테이블을 식별 [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) 제약 조건이 속한 합니다.|  
|**publisher_id**|**smallint**|비-SQL Server 게시자 열이 게시를 식별 합니다.|  
|**이름**|**sysname**|게시된 제약 조건의 이름입니다.|  
|**형식**|**nvarchar(255)**|지원 되는 제약 조건 형식을 합니다 [IHconstrainttypes](../../relational-databases/system-tables/ihconstrainttypes-transact-sql.md) 시스템 테이블입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
