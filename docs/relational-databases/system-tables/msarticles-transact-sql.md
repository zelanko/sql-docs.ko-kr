---
title: MSarticles (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSarticles
- MSarticles_TSQL
dev_langs: TSQL
helpviewer_keywords: MSarticles system table
ms.assetid: 1acd79a5-b3e2-4161-9592-7acc2a41ba38
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 458e353da5dd67489565948892b8a51025658fd8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="msarticles-transact-sql"></a>MSarticles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSarticles** 테이블 게시자가 복제 되는 각 아티클당 하나의 행을 포함 합니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**publication_id**|**int**|게시의 ID입니다.|  
|**문서**|**sysname**|아티클의 이름입니다.|  
|**article_id**|**int**|아티클의 ID입니다.|  
|**destination_object**|**sysname**|구독자에서 생성되는 테이블의 이름입니다.|  
|**source_owner**|**sysname**|게시자에서 원본 테이블의 스키마 이름입니다.|  
|**source_object**|**sysname**|아티클을 추가할 출처가 되는 원본 개체의 이름입니다.|  
|**설명**|**nvarchar(255)**|아티클에 대한 설명입니다.|  
|**destination_owner**|**sysname**|구독자에서 생성된 테이블의 스키마 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블 &#40; Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
