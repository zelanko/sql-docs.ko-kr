---
title: SQLFetch (커서 라이브러리) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2cb829f065421a13d3c7df06c670808bc3d9d77c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064430"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLFetch** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLFetch**를 참조 하십시오 [SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)합니다.  
  
 커서 라이브러리를 사용 하는 경우 호출 **SQLFetch** 중 하나를 호출 하 여 혼합할 수 없습니다 **SQLFetchScroll** 하거나 **SQLExtendedFetch**합니다.  
  
 하는 경우 **SQLFetch** 라고 커서 라이브러리는 드라이버에 대 한 호출을 전달 하는 데 사용 하 여 SQL_ATTR_ROW_ARRAY_SIZE가 1 보다 큰 값으로 설정 합니다. 드라이버는 ODBC 2 인 경우 *x* 드라이버를 행 집합 크기를 무시할지를 호출 **SQLFetch** 데이터의 단일 행을 반환 합니다.  
  
 ODBC 2를 사용 하 여 커서 라이브러리를 사용 합니다. *x* 드라이버를 오프셋 (SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성에 의해 정의 됨) 하 여 바인드 아닙니다 때 사용 되는 **SQLFetch** 라고 합니다.  
  
 커서 라이브러리를 로드 하는 경우 응용 프로그램 호출할 수 없습니다 **SQLFetch** 책갈피 열을 인출 하려면. 커서 라이브러리에 대 한 호출을 전달 **SQLFetch** 통해 드라이버 하지만 함수에는 책갈피 열을 바인딩하고 책갈피 사용에 대 한 호출에 의해 차단 됩니다 커서 라이브러리입니다.
