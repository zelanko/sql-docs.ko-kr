---
title: sys.function_order_columns (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43ce8d82bc286e7005d57d5a829e09814ffdd240
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643523"
---
# <a name="sysfunctionordercolumns-transact-sql"></a>sys.function_order_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  일부인 열 하나당 하나의 행을 반환 합니다는 **순서** 식 공용 언어 런타임 (CLR) 테이블 반환 함수입니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|순서가 정의된 개체(CLR 테이블 반환 함수)의 ID입니다.|  
|**order_column_id**|**int**|순서 열의 ID입니다. **order_column_id** 내 에서만 고유 **object_id**합니다.<br /><br /> **order_column_id는 정렬** 순서에서이 열의 위치를 나타냅니다.|  
|**column_id**|**int**|ID 열의 **object_id**합니다.<br /><br /> **column_id** 내 에서만 고유 **object_id**합니다.|  
|**is_descending**|**bit**|1 = 순서 열이 내림차순으로 정렬됩니다.<br /><br /> 0 = 순서 열이 오름차순으로 정렬됩니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
