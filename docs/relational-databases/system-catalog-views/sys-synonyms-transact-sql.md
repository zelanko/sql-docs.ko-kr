---
title: sys.synonyms (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.synonyms_TSQL
- synonyms_TSQL
- sys.synonyms
- synonyms
dev_langs: TSQL
helpviewer_keywords: sys.synonyms catalog view
ms.assetid: d6e88ca6-6e3d-4f56-bd3e-d85e26be5499
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5153ece54eb193f661ada777063ff5bb5ad7e4a4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="syssynonyms-transact-sql"></a>sys.synonyms(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  각 동의어 개체에 대해 한 행을 포함 **sys.objects.type** SN = 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Sys.objects에서 상속 된 열 >**||이 뷰가 상속 하는 열 목록은 참조 [sys.objects&#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**base_object_name**|**nvarchar(1035)**|이 동의어의 사용자가 리디렉션되는 개체의 따옴표 붙은 전체 이름입니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
