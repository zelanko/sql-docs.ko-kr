---
title: sys.function_order_columns (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- function_order_columns
- sys.function_order_columns_TSQL
- function_order_columns_TSQL
- sys.function_order_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.function_order_columns catalog view
ms.assetid: 29287973-3125-4d35-8ca9-92cb45828854
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 901dfe1cd895914b209008a474b9c7d0c9d3b847
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysfunctionordercolumns-transact-sql"></a>sys.function_order_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  일부인 열 하나당 하나의 행을 반환 합니다.는 **순서** 는 공용 언어 런타임 (CLR) 테이블 반환 함수의 식입니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|순서가 정의된 개체(CLR 테이블 반환 함수)의 ID입니다.|  
|**order_column_id**|**int**|순서 열의 ID입니다. **order_column_id** 내 에서만 고유 **object_id**합니다.<br /><br /> **order_column_id** 순서에서이 열의 위치를 나타냅니다.|  
|**column_id**|**int**|에 있는 열의 ID **object_id**합니다.<br /><br /> **column_id** 내 에서만 고유 **object_id**합니다.|  
|**is_descending**|**bit**|1 = 순서 열이 내림차순으로 정렬됩니다.<br /><br /> 0 = 순서 열이 오름차순으로 정렬됩니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
