---
title: 설명자 필드 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], fields
- header fields [ODBC]
- record fields [ODBC]
ms.assetid: f38623c8-fdd4-4601-b1f0-97c593d31177
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94e70de7d237c2eca9aee81979cb19d5295561b5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305924"
---
# <a name="descriptor-fields"></a>설명자 필드
설명자는 열 또는 매개 변수를 완전히 설명하는 *헤더* 및 *레코드* 필드를 포함합니다.  
  
 설명자는 다음 헤더 필드의 단일 복사본을 포함합니다. 헤더 필드를 변경하면 모든 열이나 매개 변수에 영향을 줍니다.  
  
|||  
|-|-|  
|SQL_DESC_ALLOC_TYPE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_COUNT|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 설명자는 0 개 이상의 설명자 레코드를 포함합니다. 각 레코드는 설명자의 유형에 따라 열 또는 매개 변수를 설명합니다. 새 열 또는 매개 변수가 바인딩되면 설명자에 새 레코드가 추가됩니다. 열 또는 매개 변수가 언바운드되면 설명자에서 레코드가 제거됩니다. 각 레코드에는 다음 필드의 단일 복사본이 포함되어 있습니다.  
  
|||  
|-|-|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_DESC_LOCAL_TYPE_NAME|  
|SQL_DESC_BASE_COLUMN_NAME|SQL_DESC_NAME|  
|SQL_DESC_BASE_TABLE_NAME|SQL_DESC_NULLABLE|  
|SQL_DESC_CASE_SENSITIVE|SQL_DESC_OCTET_LENGTH|  
|SQL_DESC_CATALOG_NAME|SQL_DESC_OCTET_LENGTH_PTR|  
|SQL_DESC_CONCISE_TYPE|SQL_DESC_PARAMETER_TYPE|  
|SQL_DESC_DATA_PTR|SQL_DESC_PRECISION|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_DESC_SCALE|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQL_DESC_SCHEMA_NAME|  
|SQL_DESC_DISPLAY_SIZE|SQL_DESC_SEARCHABLE|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_DESC_TABLE_NAME|  
|SQL_DESC_INDICATOR_PTR|SQL_DESC_TYPE|  
|SQL_DESC_LABEL|SQL_DESC_TYPE_NAME|  
|SQL_DESC_LENGTH|SQL_DESC_UNNAMED|  
|SQL_DESC_LITERAL_PREFIX|SQL_DESC_UNSIGNED|  
|SQL_DESC_LITERAL_SUFFIX|SQL_DESC_UPDATABLE|  
  
 많은 문 특성은 설명자의 헤더 필드에 해당합니다. **SQLSetStmtAttr에** 대 한 호출을 통해 이러한 특성을 설정 하 고 **SQLSetDescField를** 호출 하 여 해당 설명자 헤더 필드를 설정 동일한 효과 있습니다. 같은 정보를 검색 하는 **모두 SQLGetStmtAttr** 및 **SQLGetDescField에**대 한 마찬가지입니다. 설명자 함수 대신 문 함수를 호출하면 설명자 핸들을 검색할 필요가 없다는 장점이 있습니다.  
  
 문 특성을 설정하여 다음 헤더 필드를 설정할 수 있습니다.  
  
|||  
|-|-|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Record Count](../../../odbc/reference/develop-app/record-count.md)  
  
-   [바인딩된 설명자 레코드](../../../odbc/reference/develop-app/bound-descriptor-records.md)  
  
-   [지연 필드](../../../odbc/reference/develop-app/deferred-fields.md)  
  
-   [일관성 검사](../../../odbc/reference/develop-app/consistency-check.md)
