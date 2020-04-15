---
title: SQLFetch (커서 라이브러리) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bee83ccb5497888b57a45673599af6b92931a704
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298723"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLFetch** 함수의 사용에 대해 설명합니다. **SQLFetch에**대한 일반 정보는 [SQLFetch 함수를](../../../odbc/reference/syntax/sqlfetch-function.md)참조하십시오.  
  
 커서 라이브러리를 사용하는 경우 **SQLFetch에** 대한 호출을 **SQLFetchScroll** 또는 **SQLExtendedFetch**에 대한 호출과 혼합할 수 없습니다.  
  
 **SQLFetch가** 1보다 큰 값으로 설정된 SQL_ATTR_ROW_ARRAY_SIZE 호출하면 커서 라이브러리는 호출을 드라이버에 전달합니다. 드라이버가 ODBC 2인 경우. *x* 드라이버, 행 집합 크기는 무시 되 고 **SQLFetch에** 대 한 호출 데이터의 단일 행을 반환 합니다.  
  
 커서 라이브러리가 ODBC 2와 함께 사용되는 경우. *x* 드라이버, 바인드 오프셋 (SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성에 의해 정의 된 대로) **SQLFetch** 호출 될 때 사용 되지 않습니다.  
  
 커서 라이브러리가 로드되면 응용 프로그램은 **SQLFetch를** 호출하여 책갈피 열을 가져올 수 없습니다. 커서 라이브러리는 **SQLFetch에** 대한 호출을 드라이버로 전달하지만 책갈피를 활성화하고 책갈피 열을 바인딩하는 함수 호출은 커서 라이브러리에 의해 가로챌 수 있습니다.
