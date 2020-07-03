---
title: MSrepl_originators (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_originators_TSQL
- MSrepl_originators
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_originators system table
ms.assetid: a3ac20a6-73f6-4fdc-ad5f-5f72746c9871
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6afe910bc5e758a0003bd15c9376d4d50583eb38
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889498"
---
# <a name="msrepl_originators-transact-sql"></a>MSrepl_originators(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSrepl_originators** 테이블에는 트랜잭션이 시작 된 각 업데이트할 수 있는 구독자에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|업데이트 구독자를 식별합니다.|  
|**publisher_database_id**|**int**|게시 데이터베이스를 식별합니다.|  
|**srvname**|**sysname**|업데이트 서버의 이름입니다.|  
|**dbname**|**sysname**|업데이트 데이터베이스의 이름입니다.|  
|**publication_id**|**int**|게시를 식별합니다.|  
|**dbversion**|**int**|데이터베이스 버전을 식별합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
