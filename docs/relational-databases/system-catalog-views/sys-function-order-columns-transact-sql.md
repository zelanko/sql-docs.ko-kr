---
description: sys.function_order_columns(Transact-SQL)
title: sys. function_order_columns (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5c7ac555630f4472e5cf58ad9017cdb03643ae2b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546800"
---
# <a name="sysfunction_order_columns-transact-sql"></a>sys.function_order_columns(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  입력 mon CLR (언어 런타임) 테이블 반환 함수의 **순서** 식에 포함 되는 열 마다 한 행을 반환 합니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|순서가 정의된 개체(CLR 테이블 반환 함수)의 ID입니다.|  
|**order_column_id**|**int**|순서 열의 ID입니다. **order_column_id** 는 **object_id**내 에서만 고유 합니다.<br /><br /> 순서에서이 열의 위치를 나타내는 **order_column_id** 입니다.|  
|**column_id**|**int**|**Object_id**열의 ID입니다.<br /><br /> **column_id** 는 **object_id**내 에서만 고유 합니다.|  
|**is_descending**|**bit**|1 = 순서 열이 내림차순으로 정렬됩니다.<br /><br /> 0 = 순서 열이 오름차순으로 정렬됩니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
