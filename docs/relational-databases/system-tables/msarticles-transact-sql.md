---
title: MSarticles (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSarticles
- MSarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSarticles system table
ms.assetid: 1acd79a5-b3e2-4161-9592-7acc2a41ba38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: de2edcb376cbd58b4186fb7e2dd55c16953a48ad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47829621"
---
# <a name="msarticles-transact-sql"></a>MSarticles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSarticles** 게시자에 의해 복제 되는 각 아티클당 하나의 행을 포함 하는 테이블입니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**publication_id**|**int**|게시의 ID입니다.|  
|**article**|**sysname**|아티클의 이름입니다.|  
|**article_id**|**int**|아티클의 ID입니다.|  
|**destination_object**|**sysname**|구독자에서 생성되는 테이블의 이름입니다.|  
|**source_owner**|**sysname**|게시자에서 원본 테이블의 스키마 이름입니다.|  
|**source_object**|**sysname**|아티클을 추가할 출처가 되는 원본 개체의 이름입니다.|  
|**description**|**nvarchar(255)**|아티클에 대한 설명입니다.|  
|**destination_owner**|**sysname**|구독자에서 생성된 테이블의 스키마 이름입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
