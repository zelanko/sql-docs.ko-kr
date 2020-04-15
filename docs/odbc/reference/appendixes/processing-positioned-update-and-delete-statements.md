---
title: 위치 업데이트 및 삭제 명령문 처리 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b3f20da018bcd4e28e8ffca097fb5a4373d7f42
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308024"
---
# <a name="processing-positioned-update-and-delete-statements"></a>위치 지정 업데이트 및 Delete 문 처리
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 커서 라이브러리는 이러한 명령문의 **WHERE CURRENT CURRENT** OR절을 각 바운드 열에 대해 캐시에 저장된 값을 열거하는 **WHERE** 절로 대체하여 위치 업데이트 및 삭제 문을 지원합니다. 커서 라이브러리는 새로 구성된 **UPDATE** 및 **DELETE** 문을 드라이버에 전달하여 실행합니다. 위치 업데이트 문의 경우 커서 라이브러리는 행 집합 버퍼의 값에서 캐시를 업데이트하고 행 상태 배열의 해당 값을 SQL_ROW_UPDATED 설정합니다. 위치 지정 delete 문의 경우 행 상태 배열의 해당 값을 SQL_ROW_DELETED 설정합니다.  
  
> [!CAUTION]  
>  현재 행을 식별하기 위해 커서 라이브러리에서 생성한 **WHERE** 절은 행을 식별하거나 다른 행을 식별하거나 두 개 이상의 행을 식별하지 못할 수 있습니다. 자세한 내용은 [검색된 명령문 생성을](../../../odbc/reference/appendixes/constructing-searched-statements.md)참조하세요.  
  
 위치 업데이트 및 삭제 문은 다음과 같은 제한 사항이 적용됩니다.  
  
-   위치 업데이트 및 delete 문은 **SELECT** 문이 결과 집합을 생성한 경우에만 사용할 수 있습니다. **SELECT** 문에 조인, **UNION** 절 또는 GROUP **BY** 절이 포함되지 않은 경우 및 선택 목록에서 별칭이나 식을 사용하는 열이 **SQLBindCol**.  
  
-   응용 프로그램이 위치 지정 업데이트 또는 delete 문을 준비하는 경우 **SQLFetch** 또는 **SQLFetchScroll**를 호출한 후 이 명령으로 작성해야 합니다. 커서 라이브러리는 준비를 위해 드라이버를 제출하지만 응용 프로그램이 **SQLExecute**를 호출할 때 문을 닫고 직접 실행합니다.  
  
-   드라이버가 활성 문을 하나만 지원하는 경우 커서 라이브러리는 결과 집합의 나머지 부분을 가져온 다음 위치 된 업데이트 또는 delete 문을 실행하기 전에 캐시에서 현재 행 집합을 다시 가져옵니다. 그런 다음 응용 프로그램이 결과 집합에서 메타데이터를 반환하는 함수(예: **SQLNumResultCols** 또는 **SQLDescribeCol)를**호출하면 커서 라이브러리가 오류를 반환합니다.  
  
-   업데이트가 수행될 때마다 자동으로 업데이트되는 타임스탬프 열이 포함된 테이블의 열에서 위치 지정된 업데이트 또는 삭제 문이 수행되는 경우 타임스탬프 열이 바인딩된 경우 모든 후속 위치 업데이트 또는 삭제 문이 실패합니다. 이 문제는 커서 라이브러리가 만드는 검색된 업데이트 또는 delete 문이 업데이트할 행을 정확하게 식별하지 못하기 때문에 발생합니다. 타임스탬프 열에 대한 검색된 문의 값이 타임스탬프 열의 자동으로 업데이트되는 값과 일치하지 않습니다.
