---
description: 설명자 필드
title: 설명자 필드 | Microsoft Docs
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
ms.openlocfilehash: 56ca1fa7d558101774d10c8daa530fa32f3f7d21
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476735"
---
# <a name="descriptor-fields"></a>설명자 필드
설명자는 열 또는 매개 변수를 완전히 설명 하는 *헤더* 및 *레코드* 필드를 포함 합니다.  
  
 설명자는 다음 헤더 필드의 단일 복사본을 포함 합니다. 머리글 필드를 변경 하면 모든 열 또는 매개 변수에 영향을 줍니다.  

:::row:::
    :::column:::
        SQL_DESC_ALLOC_TYPE  
        SQL_DESC_ARRAY_SIZE  
        SQL_DESC_ARRAY_STATUS_PTR  
        SQL_DESC_BIND_OFFSET_PTR  
    :::column-end:::
    :::column:::
        SQL_DESC_BIND_TYPE  
        SQL_DESC_COUNT  
        SQL_DESC_ROWS_PROCESSED_PTR  
    :::column-end:::
:::row-end:::

 설명자에 설명자 레코드가 0 개 이상 포함 되어 있습니다. 각 레코드는 설명자 유형에 따라 열 또는 매개 변수를 설명 합니다. 새 열 또는 매개 변수가 바인딩되면 설명자에 새 레코드가 추가 됩니다. 열 또는 매개 변수가 바인딩되지 않으면 설명자에서 레코드가 제거 됩니다. 각 레코드에는 다음 필드의 단일 복사본이 포함 됩니다.  

:::row:::
    :::column:::
        SQL_DESC_AUTO_UNIQUE_VALUE  
        SQL_DESC_BASE_COLUMN_NAME  
        SQL_DESC_BASE_TABLE_NAME  
        SQL_DESC_CASE_SENSITIVE  
        SQL_DESC_CATALOG_NAME  
        SQL_DESC_CONCISE_TYPE  
        SQL_DESC_DATA_PTR  
        SQL_DESC_DATETIME_INTERVAL_CODE  
        SQL_DESC_DATETIME_INTERVAL_PRECISION  
        SQL_DESC_DISPLAY_SIZE  
        SQL_DESC_FIXED_PREC_SCALE  
        SQL_DESC_INDICATOR_PTR  
        SQL_DESC_LABEL  
        SQL_DESC_LENGTH  
        SQL_DESC_LITERAL_PREFIX  
        SQL_DESC_LITERAL_SUFFIX  
    :::column-end:::
    :::column:::
        SQL_DESC_LOCAL_TYPE_NAME  
        SQL_DESC_NAME  
        SQL_DESC_NULLABLE  
        SQL_DESC_OCTET_LENGTH  
        SQL_DESC_OCTET_LENGTH_PTR  
        SQL_DESC_PARAMETER_TYPE  
        SQL_DESC_PRECISION  
        SQL_DESC_SCALE  
        SQL_DESC_SCHEMA_NAME  
        SQL_DESC_SEARCHABLE  
        SQL_DESC_TABLE_NAME  
        SQL_DESC_TYPE  
        SQL_DESC_TYPE_NAME  
        SQL_DESC_UNNAMED  
        SQL_DESC_UNSIGNED  
        SQL_DESC_UPDATABLE  
    :::column-end:::
:::row-end:::

 많은 문 특성은 설명자의 헤더 필드에 해당 합니다. **SQLSetStmtAttr** 호출을 통해 이러한 특성을 설정 하 고 **SQLSetDescField** 를 호출 하 여 해당 설명자 헤더 필드를 설정 하면 동일한 효과가 있습니다. 동일한 정보를 검색 하는 **SQLGetStmtAttr** 및 **SQLGetDescField**의 경우에도 마찬가지입니다. 설명자 함수 대신 문 함수를 호출 하면 설명자 핸들을 검색할 필요가 없다는 장점이 있습니다.  
  
 다음 헤더 필드는 문 특성을 설정 하 여 설정할 수 있습니다.  

:::row:::
    :::column:::
        SQL_DESC_ARRAY_SIZE  
        SQL_DESC_ARRAY_STATUS_PTR  
        SQL_DESC_BIND_OFFSET_PTR  
    :::column-end:::
    :::column:::
        SQL_DESC_BIND_TYPE  
        SQL_DESC_ROWS_PROCESSED_PTR  
    :::column-end:::
:::row-end:::

 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [Record Count](../../../odbc/reference/develop-app/record-count.md)  
  
-   [바인딩된 설명자 레코드](../../../odbc/reference/develop-app/bound-descriptor-records.md)  
  
-   [지연 필드](../../../odbc/reference/develop-app/deferred-fields.md)  
  
-   [일관성 확인](../../../odbc/reference/develop-app/consistency-check.md)
