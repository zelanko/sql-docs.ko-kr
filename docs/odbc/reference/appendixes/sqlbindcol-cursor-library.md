---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e9e1018754977ee73ecdc21db30b3d8c2aae8b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199688"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLBindCol** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLBindCol**를 참조 하십시오 [SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)합니다.  
  
 응용 프로그램의 현재 행 집합을 반환 하려면 커서 라이브러리에 대 한 하나 이상의 버퍼를 할당 합니다. 호출한 **SQLBindCol** 한 번 이상 나타나는 결과 집합에 이러한 버퍼를 바인딩합니다.  
  
 응용 프로그램에서 호출할 수 있습니다 **SQLBindCol** 호출한 후 집합 열 결과 바인딩할 **SQLExtendedFetch**하십시오 **SQLFetch**, 또는 **SQLFetchScroll**로 C 데이터 형식, 열 크기 및 연결된 된 필드의 10 진수 동일 하 게 유지 합니다. 응용 프로그램 서로 다른 주소에는 열을 바인딩할 커서를 닫지 필요.  
  
 커서 라이브러리 지원 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성 바인딩 오프셋을 사용 하도록 설정 합니다. (**SQLBindCol** 이렇게 다시 바인딩하기 위해서는 발생에 대해 호출할 필요가 없습니다.) 커서 라이브러리는 ODBC 3을 사용 하 여 사용 됩니다 *.x* 드라이버를 바인딩 오프셋이 잘못 되었습니다. 때 사용 되는 **SQLFetch** 라고 합니다. 바인딩 오프셋 하는 경우 사용 됩니다 **SQLFetch** 커서 라이브러리는 ODBC 2를 사용 하 여 사용 될 때 호출 됩니다. *x* 드라이버 때문 **SQLFetch** 다음 매핑할 **SQLExtendedFetch**합니다.  
  
 커서 라이브러리 호출을 지 원하는 **SQLBindCol** 책갈피 열을 바인딩합니다.  
  
 ODBC 2 작업할 때. *x* 드라이버 커서 라이브러리에는 SQLSTATE HY090 반환 합니다 (잘못 된 문자열 또는 버퍼 길이) 때 **SQLBindCol** 4 같지 않은 값으로 책갈피 열에 대 한 버퍼 길이 설정 하기 위해 호출 됩니다. ODBC 3을 사용 하는 경우 *.x* 드라이버 커서 라이브러리를 통해 버퍼 크기입니다.
