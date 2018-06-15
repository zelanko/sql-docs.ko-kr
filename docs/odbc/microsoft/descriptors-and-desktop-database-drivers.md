---
title: 데이터베이스 드라이버 설명자 및 바탕 화면 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], descriptors
- Jet-based ODBC drivers [ODBC], descriptors
- descriptors [ODBC], Jet-supported descriptor fields
- ODBC desktop database drivers [ODBC], descriptors
ms.assetid: 9ae2d9b5-365f-4f0a-9116-defe9498b401
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62d827aecfb8b8fdf593291ce179f5c93d638dc1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32903808"
---
# <a name="descriptors-and-desktop-database-drivers"></a>설명자 및 데스크톱 데이터베이스 드라이버
설명자는 동적 매개 변수 또는 열 데이터에 대 한 정보를 보유 하는 데이터 구조입니다. **SQLGetDescField** 는 아래에 나열 된 지원 되는 설명자를 검색 하는 데 사용할 수 있습니다. 구현 매개 변수 설명자 IPD ()는 자동으로 채워지지 때문에 **SQLDescribeParam** 지원 되지 않습니다. 설명자 필드 (예: SQL_DESC_BASE_TABLE_NAME) Jet을 통해 사용할 수 없는 지원 되지 않습니다.  
  
 Jet에서 지 원하는 설명자 필드에 대 한 자세한 내용은 참조는 *Microsoft Jet 데이터베이스 엔진 Programmer's Guide*합니다.  
  
 설명자에 대 한 자세한 내용은 "설명자"에 있는 항목의 참조는 *ODBC Programmer's Reference*합니다.  
  
|설명자 필드|지원 수준|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|지원됨|  
|SQL_DESC_ARRAY_SIZE|카드가 대해서만 지원|  
|SQL_DESC_ARRAY_STATUS_PTR|지원됨|  
|SQL_DESC_BIND_OFFSET_PTR|지원됨|  
|SQL_DESC_BIND_TYPE|지원됨|  
|SQL_DESC_COUNT|지원됨|  
|SQL_DESC_ROWS_PROCESSED_PTR|카드가 대해서만 지원|  
|SQL_DESC_AUTO_UNIQUE_VALUE|지원됨|  
|SQL_DESC_BASE_COLUMN_NAME|지원 (새로운)|  
|SQL_DESC_BASE_TABLE_NAME|지원 (새로운)|  
|SQL_DESC_CASE_SENSITIVE|항상 FALSE|  
|SQL_DESC_CATALOG_NAME|지원되지 않음|  
|SQL_DESC_CONCISE_TYPE|지원됨|  
|SQL_DESC_DATA_PTR|지원됨|  
|SQL_DESC_DATETIME_INTERVAL_CODE|지원됨|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|간격 C 형식에 대 한 지원|  
|SQL_DESC_DISPLAY_SIZE|지원됨|  
|SQL_DESC_FIXED_PREC_SCALE|지원 되는 (비용에 대 한 TRUE)|  
|SQL_DESC_INDICATOR_PTR|지원됨|  
|SQL_DESC_LABEL|지원됨|  
|SQL_DESC_LENGTH|지원됨|  
|SQL_DESC_LITERAL_PREFIX|지원됨|  
|SQL_DESC_LITERAL_SUFFIX|지원됨|  
|SQL_DESC_LOCAL_TYPE_NAME|지원 되지 않습니다 (빈 문자열을 반환)|  
|SQL_DESC_NAME|지원됨|  
|SQL_DESC_NULLABLE|지원됨<br /><br /> **참고** Jet 4.0 이전 버전에서 지원 되지 않습니다|  
|SQL_DESC_NUM_PREC_RADIX|지원됨|  
|SQL_DESC_OCTET_LENGTH|지원됨|  
|SQL_DESC_OCTET_LENGTH_PTR|지원됨|  
|DESC_PARAMETER_TYPE|입력된 매개 변수만|  
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
