---
title: SQLBindCol (커서 라이브러리) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c29909a96f147a0f5ebc2140a68072dfe544255
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305474"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLBindCol** 함수의 사용에 대해 설명합니다. **SQLBindCol에**대한 일반 정보는 [SQLBindCol 함수를](../../../odbc/reference/syntax/sqlbindcol-function.md)참조하십시오.  
  
 응용 프로그램은 현재 행 집합을 반환하기 위해 커서 라이브러리에 하나 이상의 버퍼를 할당합니다. 이러한 버퍼를 결과 집합에 바인딩하기 위해 **SQLBindCol을** 하나 이상 호출합니다.  
  
 응용 프로그램은 **SQLExtendedFetch,** **SQLFetch**또는 **SQLFetch스크롤이라고**한 후 결과 집합 열을 다시 바인딩하기 위해 **SQLBindCol을** 호출할 수 있습니다. 응용 프로그램은 컬을 닫아 열을 다른 주소로 다시 바인딩할 필요가 없습니다.  
  
 커서 라이브러리는 바인드 오프셋을 사용하도록 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성 설정에 지원됩니다. (이 재바인딩이 발생하기 위해**SQLBindCol을** 호출할 필요는 없습니다.) ODBC *3.x* 드라이버와 함께 커서 라이브러리를 사용하는 경우 **SQLFetch가** 호출될 때 바인드 오프셋이 사용되지 않습니다. 바인드 오프셋은 **SQLFetch가** **SQLExtendedFetch**에 매핑되기 때문에 커서 라이브러리가 ODBC *2.x* 드라이버와 함께 사용될 때 **SQLFetch가** 호출되는 경우에 사용됩니다.  
  
 커서 라이브러리는 **SQLBindCol** 호출을 지원하여 책갈피 열을 바인딩합니다.  
  
 ODBC *2.x* 드라이버로 작업할 때 커서 라이브러리는 **SQLBindCol이** 호출될 때 SQLSTATE HY090(잘못된 문자열 또는 버퍼 길이)을 반환하여 책갈피 열의 버퍼 길이를 4와 같지 않은 값으로 설정합니다. ODBC *3.x* 드라이버로 작업할 때 커서 라이브러리를 사용하면 버퍼의 크기가 다를 수 있습니다.
