---
title: SQLGetDesc필드 및 SQLGetDescRec (커서 라이브러리) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49ceea6b6180e1b51f2f103f74412c3e2b4cbe02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307834"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField 및 SQLGetDescRec(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLGetDescField** 및 **SQLGetDescRec** 함수의 사용에 대해 설명합니다. 이러한 함수에 대한 일반적인 내용은 [SQLGetDescField 함수](../../../odbc/reference/syntax/sqlgetdescfield-function.md) 및 [SQLGetDescRec 함수를](../../../odbc/reference/syntax/sqlgetdescrec-function.md)참조하십시오.  
  
 커서 라이브러리는 **SQLGetDescRec을** 실행하여 책갈피 열에 대한 메타데이터를 반환합니다. 커서 라이브러리는 **SQLGetDescField를** 실행하여 SQL_DESC_NAME, SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE 및 SQL_DESC_NULLABLE **SQLGetDescRec에서**반환되는 동일한 필드를 반환합니다. 일관성을 위해 **SQLGetDescField도** SQL_DESC_UNNAMED 반환합니다.  
  
 커서 라이브러리는 바인딩 북마크 열에 대해 설정된 다음 필드(SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR 및 SQL_DESC_LENGTH 값을 반환하기 위해 호출될 때 **SQLGetDescField를** 실행합니다.  
  
 커서 라이브러리는 SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE 또는 SQL_DESC_ROW_STATUS_PTR 필드의 값을 반환하기 위해 호출될 때 **SQLGetDescField를** 실행합니다. 이러한 필드는 책갈피 행뿐만 아니라 모든 행에 대해 반환될 수 있습니다.  
  
 응용 프로그램에서 **SQLGetDescField를** 호출하여 앞에서 언급한 필드 이외의 필드의 값을 반환하면 커서 라이브러리는 호출을 드라이버에 전달합니다.
