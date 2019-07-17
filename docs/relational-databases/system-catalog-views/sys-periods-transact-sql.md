---
title: sys.periods (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: eea7709c67eab0dc9fe1890135f9ae03225cdff2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068090"
---
# <a name="sysperiods-transact-sql"></a>sys.periods (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  기간 정의 된 각 테이블에 대 한 행을 반환 합니다.  
  
|열 머리글|데이터 형식|설명|  
|-------------------|---------------|-----------------|  
|name|**sysname**|기간 이름|  
|period_type|**tinyint**|기간 유형을 나타내는 숫자 값입니다.<br /><br /> 1 = 시스템 시간 기간|  
|period_type_desc|**nvarchar(60)**|열 형식에 대 한 텍스트 설명.<br /><br /> SYSTEM_TIME_PERIOD|  
|object_id|**int**|Period_type 열이 포함 된 테이블의 id|  
|start_column_id|**int**|낮은 기간 경계를 정의 하는 열 id|  
|end_column_id|**int**|상위 기간 경계를 정의 하는 열의 id|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 뷰 &#40;TRANSACT-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.all_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.system_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [SQL Server 시스템 카탈로그 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)  
  
  
