---
title: 북마크 C 데이터 유형 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 566f1065d30a47b2db234ba1f11f877725189fb7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292293"
---
# <a name="bookmark-c-data-type"></a>책갈피 C 데이터 유형
책갈피 C 데이터 형식을 사용하면 응용 프로그램에서 책갈피를 검색할 수 있습니다. 책갈피 C 형식은 길이가 가변적일 수 있는 책갈피 값을 검색하는 데만 사용됩니다. 다른 데이터 유형으로 변환해서는 안 됩니다. 응용 프로그램은 **SQLBulkOperations** (SQL_ADD 작업), **SQLFetch**, **SQLFetchScroll**또는 **SQLGetData를**사용하여 결과 집합의 열 0에서 책갈피를 검색합니다. 자세한 내용은 [북마크](../../../odbc/reference/develop-app/bookmarks-odbc.md)을 참조하십시오.  
  
 다음 표에는 책갈피 C 데이터 형식에 대한 *CType* 값, 책갈피 C 데이터 형식을 구현하는 ODBC C 데이터 형식 및 SQL에서 이 데이터 형식의 정의가 나열됩니다. H.  
  
> [!NOTE]
>  SQL_C_BOOKMARK 데이터 형식이 더 이상 사용되지 않았습니다. ODBC *3.x* 응용 프로그램은 SQL_C_BOOKMARK 사용해서는 안 됩니다. ODBC *3.x* 드라이버는 SQL_C_BOOKMARK 사용하는 ODBC *2.x* 응용 프로그램으로 작업하려는 경우에만 지원해야 합니다. 드라이버 관리자는 응용 프로그램이 ODBC *2.x* 드라이버와 함께 작동할 때 SQL_C_BOOKMARK SQL_C_VARBOOKMARK 매핑합니다.  
  
|C 유형 식별자|ODBC C 타입데프|C 형식|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(사용되지 않음)|책갈피|unsigned long int|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|
