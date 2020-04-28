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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07200d48f439c97003da7062fc218cd2f3081d1b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307844"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLGetData** 함수를 사용 하는 방법을 설명 합니다. **Sqlgetdata**에 대 한 일반 정보는 [sqlgetdata 함수](../../../odbc/reference/syntax/sqlgetdata-function.md)를 참조 하세요.  
  
 커서 라이브러리는 현재 행의 각 바인딩된 열에 대해 해당 캐시에 저장 된 값을 열거 하는 **where** 절을 사용 하 여 **SELECT** 문을 먼저 생성 함으로써 **SQLGetData** 를 구현 합니다. 그런 다음 **SELECT** 문을 실행 하 여 행을 다시 선택 하 고 드라이버의 **SQLGetData** 를 호출 하 여 캐시와는 반대로 데이터 원본에서 데이터를 검색 합니다.  
  
> [!CAUTION]  
>  현재 행을 식별 하기 위해 커서 라이브러리로 생성 된 **where** 절은 행을 식별 하거나 다른 행을 식별 하거나 둘 이상의 행을 식별 하는 데 실패할 수 있습니다. 자세한 내용은 [검색 문 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)을 참조 하세요.  
  
 SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_VARIABLE로 설정 된 경우 열 0에서 **SQLGetData** 를 호출 하 여 책갈피 데이터를 반환할 수 있습니다.  
  
 **SQLGetData** 호출에는 다음과 같은 제한 사항이 적용 됩니다.  
  
-   앞 으로만 이동 가능한 커서에 대해서는 **SQLGetData** 를 호출할 수 없습니다.  
  
-   **SQLGetData** 는 다음 조건이 충족 될 경우에만 호출할 수 있습니다. **SELECT** 문에서 결과 집합을 생성 했습니다. **SELECT** 문에 Join, **UNION** 절 또는 **GROUP BY** 절이 포함 되어 있지 않습니다. select 목록에서 별칭이 나 식을 사용한 모든 열은 **SQLBindCol**와 바인딩되지 않았습니다.  
  
-   드라이버가 하나의 활성 문만 지 원하는 경우 커서 라이브러리는 **SELECT** 문을 실행 하 고 **SQLGetData**를 호출 하기 전에 나머지 결과 집합을 인출 합니다.
