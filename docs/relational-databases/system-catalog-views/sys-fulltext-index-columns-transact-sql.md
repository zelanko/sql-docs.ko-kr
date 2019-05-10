---
title: sys.fulltext_index_columns (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_index_columns
- fulltext_index_columns
- sys.fulltext_index_columns_TSQL
- fulltext_index_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], columns
- sys.fulltext_index_columns catalog view
- full-text indexes [SQL Server], properties
ms.assetid: c34b8625-e53c-4281-ace6-d46230d5cb84
aauthor: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 00e3776a4bc3f712665744062de9de01f35eca89
ms.sourcegitcommit: 04c031f7411aa33e2174be11dfced7feca8fbcda
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/30/2019
ms.locfileid: "64945566"
---
# <a name="sysfulltextindexcolumns-transact-sql"></a>sys.fulltext_index_columns(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  전체 텍스트 인덱스의 일부인 각 열에 대한 행을 포함합니다.    
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|이 열이 속한 개체의 ID입니다.|  
|**column_id**|**int**|전체 텍스트 인덱스의 일부인 열의 ID입니다.|  
|**type_column_id**|**int**|지정된 된 행에는 사용자 제공 문서 파일 확장명-".doc", "xls" 및 등의 문서를 저장 하는 유형 열의 ID입니다. 유형 열은 전체 텍스트 인덱싱 중에 해당 데이터를 필터링해야 하는 열에 대해서만 지정됩니다. 적용되지 않는 경우 NULL입니다. 자세한 내용은 [고급 분석 확장 구성 및 관리](../../relational-databases/search/configure-and-manage-filters-for-search.md)를 참조하세요.|  
|**language_id**|**int**|단어 분리기에서 이 전체 텍스트 열을 인덱싱하는 데 사용하는 언어의 LCID입니다.<br /><br /> 0 = 중립입니다.<br /><br /> 자세한 내용은 [sys.fulltext_languages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)합니다.|  
|**statistical_semantics**|**int**|1 = 이 열에 전체 텍스트 인덱싱 외에도 통계 의미 체계를 사용하도록 설정되어 있습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
