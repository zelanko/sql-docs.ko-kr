---
title: IHpublisherindexes (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHpublisherindexes
- IHpublisherindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherindexes system table
ms.assetid: 6008ef89-eeb9-46dc-93a2-f7623298cf0f
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 427df96d3f6808cbaa00d079546ad766d42fb701
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33004050"
---
# <a name="ihpublisherindexes-transact-sql"></a>IHpublisherindexes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHpublisherindexes** 시스템 테이블에서 SQL Server 이외 게시자는 현재 배포자를 사용 하 여 복제 된 각 인덱스에 대 한 하나의 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisherindex_id**|**int**|게시된 인덱스를 식별합니다.|  
|**table_id**|**int**|테이블을 식별 [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) 인덱스가 속해 있는 합니다.|  
|**publisher_id**|**smallint**|비-SQL Server 게시자 인덱스가 게시 되 고 식별 합니다.|  
|**name**|**sysname**|게시된 인덱스의 이름입니다.|  
|**type**|**nvarchar(255)**|지원 되는 인덱스 형식을 [IHindextypes](../../relational-databases/system-tables/ihindextypes-transact-sql.md) 시스템 테이블입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [복제 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
