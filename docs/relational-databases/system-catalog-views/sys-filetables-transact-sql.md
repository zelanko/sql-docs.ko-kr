---
title: sys.filetables (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- filetables
- filetables_TSQL
- sys.filetables
- sys.filetables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetables catalog view
ms.assetid: a740be59-cd52-4707-9ad2-5203669a63ac
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fff9e99a6e7fbd9e6e2e9490d8b67fce75586b6e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038344"
---
# <a name="sysfiletables-transact-sql"></a>sys.filetables(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 각 FileTable마다 하나의 행을 반환합니다. FileTables 기능에 대한 자세한 내용은 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)를 참조하세요.    
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**||개체 ID입니다. 데이터베이스 내에서 고유합니다.<br /><br /> 자세한 내용은 [sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)합니다.|  
|**is_enabled**|**bit**|1 = FileTable이 'enabled' 상태입니다.|  
|**directory_name**|**varchar(255)**|FileTable의 루트 디렉터리 이름입니다.|  
|**filename_collation_id**||FileTable에 대해 정의된 데이터 정렬 식별자입니다.|  
|**filename_collation_name**||FileTable에 대해 정의된 데이터 정렬 이름입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Filetable 관리](../../relational-databases/blob/manage-filetables.md)   
 [FileTables&#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
  
  
