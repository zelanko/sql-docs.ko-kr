---
title: sys.all_views (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.all_views_TSQL
- sys.all_views
- all_views
- all_views_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_views catalog view
ms.assetid: d8829213-fce2-41c6-9ab2-aaab5836c941
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8931b3885df642fc4fbd076b18c4375a48c2b32b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001306"
---
# <a name="sysallviews-transact-sql"></a>sys.all_views(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  모든 사용자 정의 및 시스템 뷰의 UNION을 표시합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**\<열을 상속 >**||이 뷰가 상속 하는 열 목록은 참조 하세요 [sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)합니다.|  
|**is_replicated**|**bit**|1 = 뷰가 복제됩니다.|  
|**has_replication_filter**|**bit**|1 = 뷰에 복제 필터가 있습니다.|  
|**has_opaque_metadata**|**bit**|1 = 뷰에 VIEW_METADATA 옵션이 지정되었습니다. 자세한 내용은 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)를 참조하세요.|  
|**has_unchecked_assembly_data**|**bit**|1 = 테이블은 마지막 ALTER ASSEMBLY를 수행하는 동안 정의가 변경된 어셈블리에 종속되어 있는 데이터를 포함합니다. 다음 번에 DBCC CHECKDB 또는 DBCC CHECKTABLE이 성공적으로 수행된 후에 0으로 다시 설정합니다.|  
|**with_check_option**|**bit**|1 = 뷰 정의에 WITH CHECK OPTION이 지정되었습니다.|  
|**is_date_correlation_view**|**bit**|1 = datetime 열 간 상관 관계 정보를 저장하기 위한 뷰가 시스템에서 자동으로 생성됩니다. DATE_CORRELATION_OPTIMIZATION을 설정 하 여이 뷰는 만들 수 있었습니다 **ON**합니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC CHECKDB&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [ALTER ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [DBCC CHECKTABLE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
  
  
