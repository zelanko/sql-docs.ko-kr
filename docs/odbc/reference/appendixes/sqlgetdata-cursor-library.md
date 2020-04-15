---
title: SQLGetData (커서 라이브러리) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307844"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLGetData** 함수의 사용에 대해 설명합니다. **SQLGetData에**대한 일반 정보는 [SQLGetData 함수를](../../../odbc/reference/syntax/sqlgetdata-function.md)참조하십시오.  
  
 커서 라이브러리는 먼저 현재 행의 각 바인딩된 열에 대해 캐시에 저장된 값을 열거하는 **WHERE** 절로 **SELECT** 문을 생성하여 **SQLGetData를** 구현합니다. 그런 다음 **SELECT** 문을 실행하여 행을 다시 선택하고 드라이버에서 **SQLGetData를** 호출하여 캐시가 아닌 데이터 원본에서 데이터를 검색합니다.  
  
> [!CAUTION]  
>  현재 행을 식별하기 위해 커서 라이브러리에서 생성한 **WHERE** 절은 행을 식별하거나 다른 행을 식별하거나 두 개 이상의 행을 식별하지 못할 수 있습니다. 자세한 내용은 [검색된 명령문 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)을 참조하십시오.  
  
 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE 설정된 경우 **SQLGetData를** 열 0에서 호출하여 책갈피 데이터를 반환할 수 있습니다.  
  
 **SQLGetData에** 대한 호출에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   **SQLGetData는** 정방향 전용 커서에 대해 호출할 수 없습니다.  
  
-   **SQLGetData는** 다음 조건이 충족되는 경우에만 호출할 수 있습니다. **SELECT** **SELECT** 문에는 조인, **UNION** 절 또는 **GROUP BY** 절이 포함되어 있지 않습니다. 및 선택 목록에서 별칭 이나 식을 사용 하는 모든 열 **SQLBindCol**.  
  
-   드라이버가 하나의 활성 문만 지원하는 경우 커서 라이브러리는 **SELECT** 문을 실행하고 **SQLGetData를**호출하기 전에 결과 집합의 나머지 부분을 가져옵니다.
