---
title: sys.sysfulltextcatalogs (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysfulltextcatalogs
- sys.sysfulltextcatalogs_TSQL
- sysfulltextcatalogs_TSQL
- sys.sysfulltextcatalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysfulltextcatalogs compatibility view
- sysfulltextcatalogs system table
ms.assetid: 18ac6ad5-01e8-428f-8422-a9ca29626977
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8f04e7dec965ead3d649c90a269de2f8c704ef8a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38061711"
---
# <a name="syssysfulltextcatalogs-transact-sql"></a>sys.sysfulltextcatalogs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  전체 텍스트 카탈로그에 대한 정보를 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**ftcatid**|**smallint**|전체 텍스트 카탈로그의 식별자입니다.|  
|**name**|**sysname**|사용자가 지정한 전체 텍스트 카탈로그 이름입니다.|  
|**상태**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**path**|**nvarchar(260)**|사용자가 지정한 루트 경로입니다.<br /><br /> NULL = 경로가 지정되지 않았습니다. 기본(설치) 경로가 사용되었습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
