---
title: 설명자 및 데스크톱 데이터베이스 드라이버 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], descriptors
- Jet-based ODBC drivers [ODBC], descriptors
- descriptors [ODBC], Jet-supported descriptor fields
- ODBC desktop database drivers [ODBC], descriptors
ms.assetid: 9ae2d9b5-365f-4f0a-9116-defe9498b401
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ef79855f71d23e5a884822371f1894eb83442a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303514"
---
# <a name="descriptors-and-desktop-database-drivers"></a>설명자 및 데스크톱 데이터베이스 드라이버
설명자는 열 데이터 또는 동적 매개 변수에 대한 정보를 보유하는 데이터 구조입니다. **SQLGetDescField는** 아래에 나열된 지원되는 설명기를 검색하는 데 사용할 수 있습니다. **SQLDescribeParam이** 지원되지 않기 때문에 IPD(구현 매개 변수 설명자)는 자동으로 채워지지 않습니다. Jet(예: SQL_DESC_BASE_TABLE_NAME)를 통해 사용할 수 없는 설명자 필드도 지원되지 않습니다.  
  
 Jet 지원 설명자 필드에 대한 자세한 내용은 *Microsoft Jet 데이터베이스 엔진 프로그래머 가이드를*참조하십시오.  
  
 설명자에 대한 자세한 내용은 *ODBC 프로그래머 의 참조에서*"설명자" 아래의 항목을 참조하십시오.  
  
|설명자 필드|지원 수준|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|지원됨|  
|SQL_DESC_ARRAY_SIZE|ARD에서만 지원|  
|SQL_DESC_ARRAY_STATUS_PTR|지원됨|  
|SQL_DESC_BIND_OFFSET_PTR|지원됨|  
|SQL_DESC_BIND_TYPE|지원됨|  
|SQL_DESC_COUNT|지원됨|  
|SQL_DESC_ROWS_PROCESSED_PTR|ARD에서만 지원|  
|SQL_DESC_AUTO_UNIQUE_VALUE|지원됨|  
|SQL_DESC_BASE_COLUMN_NAME|지원(신규)|  
|SQL_DESC_BASE_TABLE_NAME|지원(신규)|  
|SQL_DESC_CASE_SENSITIVE|항상 false|  
|SQL_DESC_CATALOG_NAME|지원 안 함|  
|SQL_DESC_CONCISE_TYPE|지원됨|  
|SQL_DESC_DATA_PTR|지원됨|  
|SQL_DESC_DATETIME_INTERVAL_CODE|지원됨|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|INTERVAL C 유형에 지원|  
|SQL_DESC_DISPLAY_SIZE|지원됨|  
|SQL_DESC_FIXED_PREC_SCALE|지원 (돈을 위해 TRUE)|  
|SQL_DESC_INDICATOR_PTR|지원됨|  
|SQL_DESC_LABEL|지원됨|  
|SQL_DESC_LENGTH|지원됨|  
|SQL_DESC_LITERAL_PREFIX|지원됨|  
|SQL_DESC_LITERAL_SUFFIX|지원됨|  
|SQL_DESC_LOCAL_TYPE_NAME|지원되지 않음(EMPTY 문자열 반환)|  
|SQL_DESC_NAME|지원됨|  
|SQL_DESC_NULLABLE|지원됨<br /><br /> **참고 사항** Jet 4.0 이전 버전에서는 지원되지 않음|  
|SQL_DESC_NUM_PREC_RADIX|지원됨|  
|SQL_DESC_OCTET_LENGTH|지원됨|  
|SQL_DESC_OCTET_LENGTH_PTR|지원됨|  
|SQL_DESC_PARAMETER_TYPE|입력 매개 변수만|  
|SQL_DESC_PRECISION|지원됨|  
|SQL_DESC_SCALE|지원됨|  
|SQL_DESC_SCHEMA_NAME|지원 안 함|  
|SQL_DESC_SEARCHABLE|지원됨|  
|SQL_DESC_TABLE_NAME|지원 안 함|  
|SQL_DESC_TYPE|지원됨|  
|SQL_DESC_TYPE_NAME|지원됨|  
|SQL_DESC_UNNAMED|지원됨|  
|SQL_DESC_UNSIGNED|지원됨|  
|SQL_DESC_UPDATABLE|지원됨|
