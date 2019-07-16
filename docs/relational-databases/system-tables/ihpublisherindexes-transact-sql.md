---
title: IHpublisherindexes (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublisherindexes
- IHpublisherindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherindexes system table
ms.assetid: 6008ef89-eeb9-46dc-93a2-f7623298cf0f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 114ffee3ca13d7b5a42c3843957df0a2450b787f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990248"
---
# <a name="ihpublisherindexes-transact-sql"></a>IHpublisherindexes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **IHpublisherindexes** 시스템 테이블에서 SQL Server 이외 게시자는 현재 배포자를 사용 하 여 복제 된 각 인덱스에 대 한 하나의 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**publisherindex_id**|**int**|게시된 인덱스를 식별합니다.|  
|**table_id**|**int**|테이블을 식별 [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) 인덱스가 속한 합니다.|  
|**publisher_id**|**smallint**|-SQL Server 이외 게시자는 인덱스가 게시 되는 식별 합니다.|  
|**name**|**sysname**|게시된 인덱스의 이름입니다.|  
|**type**|**nvarchar(255)**|지원 되는 인덱스 형식을 합니다 [IHindextypes](../../relational-databases/system-tables/ihindextypes-transact-sql.md) 시스템 테이블입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
