---
description: 설명자 및 데스크톱 데이터베이스 드라이버
title: 설명자 및 데스크톱 데이터베이스 드라이버 | Microsoft Docs
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
ms.openlocfilehash: 80565f912ef3136dc03cf7216ff3f997ee3eeba3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340799"
---
# <a name="descriptors-and-desktop-database-drivers"></a>설명자 및 데스크톱 데이터베이스 드라이버
설명자는 열 데이터 또는 동적 매개 변수에 대 한 정보를 포함 하는 데이터 구조입니다. **SQLGetDescField** 은 아래에 나열 된 지원 되는 설명자를 검색 하는 데 사용할 수 있습니다. **SQLDescribeParam** 가 지원 되지 않으므로 IPD (구현 매개 변수 설명자)가 자동으로 채워지지 않습니다. Jet를 통해 사용할 수 없는 설명자 필드 (예: SQL_DESC_BASE_TABLE_NAME)도 지원 되지 않습니다.  
  
 Jet 지원 설명자 필드에 대 한 자세한 내용은 *Microsoft Jet 데이터베이스 엔진 프로그래머 가이드*를 참조 하세요.  
  
 설명자에 대 한 자세한 내용은 *ODBC 프로그래머 참조*의 "설명자"에 있는 항목을 참조 하십시오.  
  
|설명자 필드|지원 수준|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|지원됨|  
|SQL_DESC_ARRAY_SIZE|인 경우에만 지원 됨|  
|SQL_DESC_ARRAY_STATUS_PTR|지원됨|  
|SQL_DESC_BIND_OFFSET_PTR|지원됨|  
|SQL_DESC_BIND_TYPE|지원됨|  
|SQL_DESC_COUNT|지원됨|  
|SQL_DESC_ROWS_PROCESSED_PTR|인 경우에만 지원 됨|  
|SQL_DESC_AUTO_UNIQUE_VALUE|지원됨|  
|SQL_DESC_BASE_COLUMN_NAME|지원 됨 (신규)|  
|SQL_DESC_BASE_TABLE_NAME|지원 됨 (신규)|  
|SQL_DESC_CASE_SENSITIVE|항상 FALSE|  
|SQL_DESC_CATALOG_NAME|지원되지 않음|  
|SQL_DESC_CONCISE_TYPE|지원됨|  
|SQL_DESC_DATA_PTR|지원됨|  
|SQL_DESC_DATETIME_INTERVAL_CODE|지원됨|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|간격 C 유형에 지원 됨|  
|SQL_DESC_DISPLAY_SIZE|지원됨|  
|SQL_DESC_FIXED_PREC_SCALE|지원 됨 (money의 경우 TRUE)|  
|SQL_DESC_INDICATOR_PTR|지원됨|  
|SQL_DESC_LABEL|지원됨|  
|SQL_DESC_LENGTH|지원됨|  
|SQL_DESC_LITERAL_PREFIX|지원됨|  
|SQL_DESC_LITERAL_SUFFIX|지원됨|  
|SQL_DESC_LOCAL_TYPE_NAME|지원 되지 않음 (빈 문자열 반환)|  
|SQL_DESC_NAME|지원됨|  
|SQL_DESC_NULLABLE|지원됨<br /><br /> **참고** Jet 4.0 이전 버전에서는 지원 되지 않음|  
|SQL_DESC_NUM_PREC_RADIX|지원됨|  
|SQL_DESC_OCTET_LENGTH|지원됨|  
|SQL_DESC_OCTET_LENGTH_PTR|지원됨|  
|SQL_DESC_PARAMETER_TYPE|입력 매개 변수만|  
|SQL_DESC_PRECISION|지원됨|  
|SQL_DESC_SCALE|지원됨|  
|SQL_DESC_SCHEMA_NAME|지원되지 않음|  
|SQL_DESC_SEARCHABLE|지원됨|  
|SQL_DESC_TABLE_NAME|지원되지 않음|  
|SQL_DESC_TYPE|지원됨|  
|SQL_DESC_TYPE_NAME|지원됨|  
|SQL_DESC_UNNAMED|지원됨|  
|SQL_DESC_UNSIGNED|지원됨|  
|SQL_DESC_UPDATABLE|지원됨|
