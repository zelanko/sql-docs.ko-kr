---
title: SQLGetData (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 96ffa184247c4fd7d05300952133c19127f979af
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909918"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLGetData** 커서 라이브러리의 함수가 있습니다. 에 대 한 일반적인 내용은 **SQLGetData**, 참조 [SQLGetData 함수](../../../odbc/reference/syntax/sqlgetdata-function.md)합니다.  
  
 커서 라이브러리 구현 **SQLGetData** 먼저 생성 하 여 한 **선택** 문을 **여기서** 각 바운드에 대 한 캐시에 저장 된 값을 열거 하는 절 현재 행의 열입니다. 그런 다음 실행는 **선택** 행 및 호출을 다시 선택 하는 문을 **SQLGetData** (캐시) 대비 데이터 원본에서 데이터를 검색 하도록 드라이버에 있습니다.  
  
> [!CAUTION]  
>  **여기서** 절 현재 행을 식별 하는 커서 라이브러리에서 생성 된 모든 행을 식별 하 고, 다른 행을 식별 또는 둘 이상의 행을 식별 되지 않을 수 있습니다. 자세한 내용은 참조 [검색 문을 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)합니다.  
  
 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_VARIABLE로 설정 된 경우 **SQLGetData** 열 책갈피 데이터를 반환 하는 0에서 호출할 수 있습니다.  
  
 에 대 한 호출이 **SQLGetData** 다음과 같은 제한 사항이 적용 됩니다.  
  
-   **SQLGetData** 정방향 전용 커서에 대해 호출할 수 없습니다.  
  
-   **SQLGetData** 다음 조건이 충족 되는 경우에 호출할 수 있습니다:는 **선택** 문은 결과 집합을 생성, **선택** 문에 조인이 포함 되지 않았습니다는  **UNION** 절 또는 **GROUP BY** 절이 없습니다; 및 select 목록의 식이나 별칭을 사용 하는 모든 열이 있는 바인딩되지 않은 **SQLBindCol**합니다.  
  
-   커서 라이브러리는 결과 집합을 실행 하기 전에 나머지 부분을 인출 드라이버 하나의 활성 문만 지 원하는 경우는 **선택** 문과 호출 **SQLGetData**합니다.
