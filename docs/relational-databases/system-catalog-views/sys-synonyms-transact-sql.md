---
description: sys.synonyms(Transact-SQL)
title: sys. 동의어 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.synonyms_TSQL
- synonyms_TSQL
- sys.synonyms
- synonyms
dev_langs:
- TSQL
helpviewer_keywords:
- sys.synonyms catalog view
ms.assetid: d6e88ca6-6e3d-4f56-bd3e-d85e26be5499
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f7afb67a5371ca85bc3a0fa623b42519370e133a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545028"
---
# <a name="syssynonyms-transact-sql"></a>sys.synonyms(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  각 동의어 개체에 대 한 행을 포함 합니다. 여기에는 **sys.debug** = SN이 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||이 뷰가 상속 하는 열 목록은 [sys. 개체 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조 하세요.|  
|**base_object_name**|**nvarchar (1035)**|이 동의어의 사용자가 리디렉션되는 개체의 따옴표 붙은 전체 이름입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
