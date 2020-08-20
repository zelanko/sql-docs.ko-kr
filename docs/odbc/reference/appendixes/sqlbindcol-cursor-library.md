---
description: SQLBindCol(커서 라이브러리)
title: SQLBindCol (커서 라이브러리) | Microsoft Docs
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
ms.openlocfilehash: f3b3968687f1c9062457a16ec7c5bc11cb32d3a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456482"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLBindCol** 함수를 사용 하는 방법을 설명 합니다. **SQLBindCol**에 대 한 일반 정보는 [SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)를 참조 하세요.  
  
 응용 프로그램은에서 현재 행 집합을 반환 하기 위해 커서 라이브러리에 대해 하나 이상의 버퍼를 할당 합니다. **SQLBindCol** 를 한 번 이상 호출 하 여 이러한 버퍼를 결과 집합에 바인딩합니다.  
  
 응용 프로그램은 바인딩된 열의 C 데이터 형식, 열 크기 및 10 진수가 동일 하 게 유지 되는 한 **Sqlextendedfetch**, **Sqlfetch**또는 **sqlextendedfetch**을 호출한 후 **SQLBindCol** 를 호출 하 여 결과 집합 열을 다시 바인딩할 수 있습니다. 응용 프로그램은 열을 다른 주소로 다시 바인딩하는 커서를 닫을 필요가 없습니다.  
  
 커서 라이브러리는 바인딩 오프셋을 사용 하도록 SQL_ATTR_ROW_BIND_OFFSET_PTR statement 특성을 설정 하도록 지원 합니다. 이 리바인딩을 수행 하기 위해**SQLBindCol** 를 호출할 필요가 없습니다. ODBC 3.x 드라이버에 커서 라이브러리를 사용 하는 경우 **Sqlfetch** 를 호출할 때 바인드 오프셋이 사용 되지 *않습니다.* 바인딩 오프셋은 sqlfetch가 **Sqlextendedfetch**에 매핑되므로 ODBC *2.x 드라이버에서* 커서 라이브러리를 사용할 때 **sqlfetch** 를 호출 **SQLFetch** 하는 경우에 사용 됩니다.  
  
 커서 라이브러리는 **SQLBindCol** 를 호출 하 여 책갈피 열을 바인딩하는 것을 지원 합니다.  
  
 ODBC 2.x 드라이버를 사용 하는 경우 책갈피 열의 버퍼 길이를 4가 아닌 값으로 설정 하기 위해 **SQLBindCol** 를 호출할 때 커서 라이브러리는 SQLSTATE HY090 (잘못 된 문자열 또는 버퍼 길이)를 반환 *합니다.* ODBC 3.x 드라이버를 사용 하는 경우 커서 라이브러리를 사용 하 여 버퍼 크기를 지정할 수 *있습니다.*
