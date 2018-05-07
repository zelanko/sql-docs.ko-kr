---
title: sys.sysfilegroups (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysfilegroups_TSQL
- sys.sysfilegroups
- sysfilegroups
- sys.sysfilegroups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysfilegroups system table
- sys.sysfilegroups compatibility view
ms.assetid: e567fa07-31cd-43cc-b8c7-ba6108baca80
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7f61d8967602919e096bf3e17ba5dcd71899a06f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="syssysfilegroups-transact-sql"></a>sys.sysfilegroups(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스에 있는 각 파일 그룹에 대해 한 행씩 있습니다. 이 테이블에는 주 파일 그룹에 대한 항목이 적어도 한 개는 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**groupid**|**smallint**|각 데이터베이스에 고유한 그룹 ID입니다.|  
|**allocpolicy**|**smallint**|예약됨|  
|**상태**|**int**|0x8 = 읽기 전용<br /><br /> 0x10 = 기본값|  
|**groupname**|**sysname**|파일 그룹의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
