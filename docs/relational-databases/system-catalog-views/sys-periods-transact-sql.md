---
title: sys.periods (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 25e66ed3-2270-4c5c-9f5a-2c0f165a57ca
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1fc56165753b0ee2344826ee87c6c049a8ad1dda
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sysperiods-transact-sql"></a>sys.periods (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  기간 정의 된 각 테이블에 대 한 행을 반환 합니다.  
  
|열 머리글|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|period_type|**sysname**|기간 이름|  
|period_type_desc|**tinyint**|기간 유형을 나타내는 숫자 값입니다.<br /><br /> 1 = 시스템 시간 기간|  
|object_id|**nvarchar(60)**|열의 유형의 텍스트 설명:<br /><br /> SYSTEM_TIME_PERIOD|  
|object_id|**int**|Period_type 열이 포함 된 테이블의 id|  
|start_column_id|**int**|하위 기간 경계를 정의 하는 열 id|  
|end_column_id|**int**|상위 기간 경계를 정의 하는 열 id|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 뷰 &#40; Transact SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [개체 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.all_columns &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.system_columns &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [SQL Server 시스템 카탈로그 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)  
  
  
