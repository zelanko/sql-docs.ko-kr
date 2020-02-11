---
title: 책갈피 C 데이터 형식 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86488da93470a61a54638e9c60e6e1795a9da4dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125751"
---
# <a name="bookmark-c-data-type"></a>책갈피 C 데이터 유형
책갈피 C 데이터 형식을 사용 하면 응용 프로그램에서 책갈피를 검색할 수 있습니다. 책갈피 C 형식은 길이가 가변적 일 수 있는 책갈피 값을 검색 하는 데만 사용 됩니다. 다른 데이터 형식으로 변환 하면 안 됩니다. 응용 프로그램은 **SQLBulkOperations** 를 사용 하 여 결과 집합의 0 열에서 책갈피를 검색 합니다 (SQL_ADD 작업 포함), **sqlfetch**, **sqlfetchscroll**또는 **SQLGetData**. 자세한 내용은 [책갈피](../../../odbc/reference/develop-app/bookmarks-odbc.md)를 참조 하세요.  
  
 다음 표에서는 책갈피 C 데이터 형식에 대 한 *CType* 의 값, 책갈피 c 데이터 형식을 구현 하는 ODBC C 데이터 형식 및 SQL의이 데이터 형식에 대 한 정의를 나열 합니다. 넣기.  
  
> [!NOTE]
>  SQL_C_BOOKMARK 데이터 형식은 더 이상 사용 되지 않습니다. ODBC *3.x 응용 프로그램은 SQL_C_BOOKMARK* 를 사용 하면 안 됩니다. ODBC *3.x 드라이버는* 이를 사용 하는 odbc *2.x 응용 프로그램* 을 사용 하려는 경우에만 SQL_C_BOOKMARK을 지원 해야 합니다. 응용 *프로그램이 ODBC 2.x* 드라이버를 사용 하 여 작동 하는 경우 드라이버 관리자는 SQL_C_VARBOOKMARK를 SQL_C_BOOKMARK에 매핑합니다.  
  
|C 형식 식별자|ODBC C typedef|C 형식|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(사용되지 않음)|책갈피|unsigned long int|  
|SQL_C_VARBOOKMARK|SQLCHAR|unsigned char *|
