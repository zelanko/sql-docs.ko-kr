---
title: MSreplication_objects (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- MSreplication_objects
- MSreplication_objects_TSQL
dev_langs: TSQL
helpviewer_keywords: MSreplication_objects system table
ms.assetid: 08f9710d-976d-448e-bead-ac9835e87bc5
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bf9eef9834dca254f153c8f7a984f77a1ad33c0f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="msreplicationobjects-transact-sql"></a>MSreplication_objects(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_objects** 테이블은 복제 구독자 데이터베이스에 연결 된 각 개체에 대해 하나의 행을 포함 합니다. 이 테이블은 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|게시자의 이름입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**게시**|**sysname**|게시의 이름입니다.|  
|**object_name**|**sysname**|개체 이름입니다.|  
|**object_type**|**char(2)**|개체 형식입니다.<br /><br /> **u** = 테이블입니다.<br /><br /> **t** = 트리거.<br /><br /> **p** = 저장된 프로시저입니다.|  
|**문서**|**sysname**|개체가 연결된 아티클의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
