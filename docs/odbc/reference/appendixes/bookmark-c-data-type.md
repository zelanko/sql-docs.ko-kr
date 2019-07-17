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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125751"
---
# <a name="bookmark-c-data-type"></a>책갈피 C 데이터 유형
책갈피 C 데이터 형식에는 응용을 프로그램이 책갈피를 검색할 수 있습니다. 책갈피 C 형식은; 길이가 가변적 일 수 있는 책갈피 값을 검색 하는 데에 사용 됩니다. 또한 다른 데이터 형식으로 변환 되지 해야 합니다. 응용 프로그램 검색 결과의 열 0에서 사용 하 여 설정 책갈피 **SQLBulkOperations** (작업과 SQL_ADD의), **SQLFetch**를 **SQLFetchScroll**, 또는 **SQLGetData**합니다. 자세한 내용은 [책갈피](../../../odbc/reference/develop-app/bookmarks-odbc.md)합니다.  
  
 다음 표에서 값을 나열 *CType* 책갈피 C 데이터 형식에 대 한 책갈피 C 데이터 형식 및이 데이터의 정의 구현 하는 ODBC C 데이터 형식을 SQL에서 입력 합니다. 8.  
  
> [!NOTE]
>  SQL_C_BOOKMARK 데이터 형식이 더 이상 사용 되지 않습니다. ODBC *3.x* SQL_C_BOOKMARK 응용 프로그램을 사용 하지 않아야 합니다. ODBC *3.x* 드라이버에서 ODBC를 사용 하려는 경우에 SQL_C_BOOKMARK 지원 해야 *2.x* 을 사용 하는 응용 프로그램입니다. 드라이버 관리자 매핑됩니다 SQL_C_VARBOOKMARK SQL_C_BOOKMARK ODBC를 사용 하 여 응용 프로그램이 작동 하는 경우 *2.x* 드라이버입니다.  
  
|C 형식 식별자|ODBC C typedef|C 형식|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(사용되지 않음)|책갈피|부호 없는 long int|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|
