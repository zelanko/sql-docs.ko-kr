---
title: 위치 지정 업데이트 및 Delete 문을 처리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d898fcc7d1b35230173afa0443219d59c54720ae
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057076"
---
# <a name="processing-positioned-update-and-delete-statements"></a>위치 지정 업데이트 및 Delete 문 처리
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 배치 커서 라이브러리에서 지 원하는 업데이트 및 교체 하 여 delete 문의 **WHERE CURRENT OF** 사용 하 여 이러한 문에 절을 **여기서** 해당 캐시에 저장 된 값을 열거 하는 절 바인딩된 각 열입니다. 커서 라이브러리를 새로 생성 된 전달 **업데이트** 하 고 **삭제** 실행에 대 한 드라이버는 문입니다. 위치 지정된 update 문에 대 한 커서 라이브러리는 다음 행 집합 버퍼 값에서 캐시를 업데이트 하 고 SQL_ROW_UPDATED 행 상태 배열에서 해당 값을 설정 합니다. 위치 지정된 delete 문에 대 한 sql_row_deleted가 행 상태 배열에서 해당 값을 설정합니다.  
  
> [!CAUTION]  
>  합니다 **여기서** 절 현재 행을 식별 하려면 커서 라이브러리에 의해 생성 된 모든 행을 식별 하 고, 다른 행을 식별 또는 둘 이상의 행을 식별 하지 못할 수 있습니다. 자세한 내용은 [검색 문을 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)이 부록의 뒷부분에 나오는.  
  
 위치 지정 업데이트 및 삭제 문을 다음과 같은 제한 사항이 적용 됩니다.  
  
-   위치 지정 업데이트 및 삭제 문은 다음과 같은 경우에만 사용할 수 있습니다: 때를 **선택** 문이 결과 집합 생성는 경우를 **선택** 문에 조인이 포함 되지 않았습니다는  **UNION** 절 또는 **GROUP BY** 절 및 select 목록의 식이나 별칭을 사용 하는 열에 없습니다 사용 하 여 바인딩된 **SQLBindCol**합니다.  
  
-   응용 프로그램 위치 지정된 update 또는 delete 문을 준비를 수행 해야 하므로 호출한 후 **SQLFetch** 하거나 **SQLFetchScroll**합니다. 문을 닫습니다 준비에 대 한 드라이버 해당 문을 전송 하는 커서 라이브러리, 있지만 및 응용 프로그램을 호출할 때 직접 실행 **SQLExecute**합니다.  
  
-   드라이버 하나의 활성 문만 지 원하는 경우에 결과의 나머지 부분 설정 하 고 배치를 실행 하기 전에 해당 캐시의 현재 행 집합을 한 다음 다시 커서 라이브러리 인출 update 또는 delete 문입니다. 그러면 응용 프로그램이 결과 집합의 메타 데이터를 반환 하는 함수를 호출 하는 경우 (예를 들어 **SQLNumResultCols** 또는 **SQLDescribeCol**), 커서 라이브러리 오류를 반환 합니다.  
  
-   위치 지정된 update 또는 delete 문을 업데이트 수행 될 때마다 자동으로 업데이트 되는 타임 스탬프 열이 포함 된 테이블의 열에서 수행 하는 경우 모든 후속 위치 지정된 업데이트 또는 삭제 문을 실행 하지 못합니다 타임 스탬프 열이 바인딩됩니다. 이 때문에 발생 된 검색 업데이트 또는 삭제 문이 커서 라이브러리를 만들기는 업데이트할 행을 정확 하 게 식별 하지 않습니다. 타임 스탬프 열에 대 한 검색 문에서 값을 자동으로 업데이트 된 타임 스탬프 열 값을 일치 하지 않습니다.
