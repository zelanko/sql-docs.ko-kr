---
description: sys.debug (Transact-sql)
title: sys.debug (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 25e66ed3-2270-4c5c-9f5a-2c0f165a57ca
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c091649234826080054de942ed96272055a1b595
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810330"
---
# <a name="sysperiods-transact-sql"></a>sys.debug (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  기간이 정의 된 각 테이블에 대해 하나의 행을 반환 합니다.  
  
|열 머리글|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|name|**sysname**|기간 이름|  
|period_type|**tinyint**|기간 유형을 나타내는 숫자 값입니다.<br /><br /> 1 = 시스템 시간 기간|  
|period_type_desc|**nvarchar(60)**|열 유형에 대 한 텍스트 설명입니다.<br /><br /> SYSTEM_TIME_PERIOD|  
|object_id|**int**|Period_type 열을 포함 하는 테이블의 id입니다.|  
|start_column_id|**int**|낮은 기간 경계를 정의 하는 열의 id입니다.|  
|end_column_id|**int**|상한 경계를 정의 하는 열의 id입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 뷰 ](../../t-sql/language-reference.md)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Transact-sql&#41;sys.all_columns &#40;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [ Transact-sql&#41;&#40;tem_columnssys.sys](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)  
  
