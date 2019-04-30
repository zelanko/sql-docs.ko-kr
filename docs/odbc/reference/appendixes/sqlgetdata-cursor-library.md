---
title: SQLGetData (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e3009b4e3bed6fc871ecfd1aab4e2af2f1f1c86
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188773"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLGetData** 커서 라이브러리의 함수입니다. 에 대 한 일반 정보에 대 한 **SQLGetData**를 참조 하십시오 [SQLGetData 함수](../../../odbc/reference/syntax/sqlgetdata-function.md)합니다.  
  
 커서 라이브러리 구현 **SQLGetData** 첫 번째 구성 하 여를 **선택** 문을 사용 하 여는 **여기서** 각 범위에 대 한 해당 캐시에 저장 된 값을 열거 하는 절 현재 행의 열입니다. 그런 다음 실행 합니다 **선택** 행과 호출을 다시 선택 문을 **SQLGetData** (캐시) 대신 데이터 원본에서 데이터를 검색 하도록 드라이버에.  
  
> [!CAUTION]  
>  합니다 **여기서** 절 현재 행을 식별 하려면 커서 라이브러리에 의해 생성 된 모든 행을 식별 하 고, 다른 행을 식별 또는 둘 이상의 행을 식별 하지 못할 수 있습니다. 자세한 내용은 [검색 문을 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)합니다.  
  
 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_VARIABLE로 설정 된 경우 **SQLGetData** 열 책갈피 데이터를 반환 하는 0에서 호출할 수 있습니다.  
  
 에 대 한 호출 **SQLGetData** 다음과 같은 제한 사항이 적용 됩니다.  
  
-   **SQLGetData** 정방향 전용 커서에 대해 호출할 수 없습니다.  
  
-   **SQLGetData** 다음 조건에 해당 하는 경우에 호출할 수 있습니다:는 **선택** 문이 결과 집합을 생성, **선택** 문에 조인이 포함 되지 않았습니다를  **UNION** 절 또는 **GROUP BY** 절과 select 목록의 식이나 별칭을 사용 하는 모든 열이 사용 하 여 바인딩되지 되었습니다 **SQLBindCol**합니다.  
  
-   커서 라이브러리는 나머지 결과 집합을 실행 하기 전에 인출 드라이버 하나의 활성 문만 지 원하는 경우는 **선택** 문 및 호출 **SQLGetData**합니다.
