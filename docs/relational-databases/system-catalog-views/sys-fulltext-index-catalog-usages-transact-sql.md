---
title: sys.fulltext_index_catalog_usages (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_index_catalog_usages
- sys.fulltext_index_catalog_usages_TSQL
- fulltext_index_catalog_usages
- fulltext_index_catalog_usages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_index_catalog_usages catalog view
ms.assetid: d095ab62-270b-484b-a541-9f9e7c951cf0
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4d9714230ff13588e490ecdbb502c98bb8c2223d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47617881"
---
# <a name="sysfulltextindexcatalogusages-transact-sql"></a>sys.fulltext_index_catalog_usages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  전체 텍스트 인덱스 참조에 대한 각 전체 텍스트 카탈로그에 대해 행을 반환합니다.    
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|전체 텍스트 인덱싱된 테이블의 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**index_id**|**int**|전체 텍스트 인덱스의 ID입니다.|  
|**fulltext_catalog_id**|**int**|전체 텍스트 카탈로그의 ID입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [데이터 공간 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)  
  
  
