---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b512ff83d0002ef4a7c79b48cd8829fc2dbb9ba3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696582"
---
# <a name="descriptor-fields"></a>설명자 필드
설명자 포함 *머리글* 하 고 *레코드* 완전히 열 또는 매개 변수를 설명 하는 필드.  
  
 설명자 헤더 필드의 단일 복사본을 포함합니다. 헤더 필드를 변경 합니다. 모든 열 또는 매개 변수에 영향을 줍니다.  
  
|||  
|-|-|  
|SQL_DESC_ALLOC_TYPE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_COUNT|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 설명자를 0 개 이상의 설명자 레코드를 포함합니다. 열 또는 매개 변수 설명자의 유형에 따라 각 레코드에 설명합니다. 새 열 또는 매개 변수는 바인딩되는 경우 새 레코드를 설명자에 추가 됩니다. 열 또는 매개 변수를 바인딩 해제 되는 레코드 설명자에서 제거 됩니다. 각 레코드는 다음 필드의 단일 복사본이 포함 되어 있습니다.  
  
|||  
|-|-|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_DESC_LOCAL_TYPE_NAME|  
|SQL_DESC_BASE_COLUMN_NAME|SQL_DESC_NAME|  
|SQL_DESC_BASE_TABLE_NAME|SQL_DESC_NULLABLE|  
|SQL_DESC_CASE_SENSITIVE|SQL_DESC_OCTET_LENGTH|  
|SQL_DESC_CATALOG_NAME|SQL_DESC_OCTET_LENGTH_PTR|  
|SQL_DESC_CONCISE_TYPE|DESC_PARAMETER_TYPE|  
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
  
 여러 문 특성 설명자 헤더 필드에 해당합니다. 호출을 통해 이러한 특성을 설정 **SQLSetStmtAttr** 를 호출 하 여 해당 설명자 헤더 필드를 설정 하 고 **SQLSetDescField** 효과 동일 합니다. 같은 기준이 **SQLGetStmtAttr** 및 **SQLGetDescField**, 동일한 정보를 검색할 둘 다. 설명자 함수 대신 문 함수 호출 없다는 이점이 설명자 핸들을 검색할 필요가 없습니다.  
  
 문 특성을 설정 하 여 다음 헤더 필드를 설정할 수 있습니다.  
  
|||  
|-|-|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [레코드 수](../../../odbc/reference/develop-app/record-count.md)  
  
-   [바인딩된 설명자 레코드](../../../odbc/reference/develop-app/bound-descriptor-records.md)  
  
-   [지연 필드](../../../odbc/reference/develop-app/deferred-fields.md)  
  
-   [일관성 검사](../../../odbc/reference/develop-app/consistency-check.md)
