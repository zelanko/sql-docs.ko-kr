---
title: "Update 및 Delete 문을 처리 배치 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 367062f5e671b366771b1a04f129b8e312f48cca
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="processing-positioned-update-and-delete-statements"></a>Update 및 Delete 문을 처리 배치
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 배치 커서 라이브러리 지원 업데이트 및 대체 하 여 delete 문의 **WHERE CURRENT OF** 절와 이러한 문에서 **여기서** 에 대 한 캐시에 저장 된 값을 열거 하는 절 바인딩된 각 열입니다. 커서 라이브러리 새로 생성 된 전달 **업데이트** 및 **삭제** 문을 실행 하기 위해 드라이버를 합니다. 위치 지정된 update 문에 대 한 커서 라이브러리는 다음 행 집합 버퍼의 값에서 캐시를 업데이트 하 고 SQL_ROW_UPDATED 행 상태 배열이의 해당 값을 설정 합니다. 위치 지정된 delete 문에 대 한 행은 SQL_ROW_DELETED 상태 배열의 해당 하는 값을 설정합니다.  
  
> [!CAUTION]  
>  **여기서** 절 현재 행을 식별 하는 커서 라이브러리에서 생성 된 모든 행을 식별 하 고, 다른 행을 식별 또는 둘 이상의 행을 식별 되지 않을 수 있습니다. 자세한 내용은 참조 [검색 문을 생성](../../../odbc/reference/appendixes/constructing-searched-statements.md)이 부록의 뒷부분에 나오는 합니다.  
  
 위치 update 및 delete 문은 다음과 같은 제한 사항이 적용 됩니다.  
  
-   위치 update 및 delete 문은 다음과 같은 경우에만 사용할 수 있습니다: 때는 **선택** 문은 결과 집합 생성 때는 **선택** 문에 조인이 포함 되지 않았습니다는 ** UNION** 절 또는 **GROUP BY** 절이 없습니다; select 목록의 식이나 별칭을 사용 하는 모든 열와 바인딩되어 있지 않은 경우 및 **SQLBindCol**합니다.  
  
-   응용 프로그램을 위치 지정된 update 또는 delete 문이 준비를 수행 해야 하므로 호출한 후 **SQLFetch** 또는 **SQLFetchScroll**합니다. 문을 닫습니다 및 응용 프로그램 호출 하는 경우 직접 실행 하 고 준비 하기 위해 드라이버를 해당 문을 전송 하는 커서 라이브러리, 있지만 **SQLExecute**합니다.  
  
-   드라이버 하나의 활성 문만 지 원하는 경우에 결과의 나머지 설정 하 고 배치를 실행 하기 전에 캐시에서 현재 행 집합을 다음 다시 커서 라이브러리 인출 업데이트 또는 삭제 문의 합니다. 그런 다음 응용 프로그램 메타 데이터는 결과 집합에서 반환 하는 함수를 호출 하는 경우 (예를 들어 **SQLNumResultCols** 또는 **SQLDescribeCol**), 커서 라이브러리는 오류를 반환 합니다.  
  
-   위치 지정된 update 또는 delete 문이 업데이트를 수행할 때마다 자동으로 업데이트 하는 타임 스탬프 열을 포함 하는 테이블의 열에서 수행 하는 경우 모든 후속 위치 지정된 update 또는 delete 문을 못합니다 타임 스탬프 열이 바인딩된 합니다. 이 때문에 발생 검색 된 update 또는 delete 문이 커서 라이브러리 만들기는 업데이트할 행을 정확 하 게 식별 하지 않습니다. 타임 스탬프 열에 대 한 검색 결과 문의 값의 타임 스탬프 열 자동으로 업데이트 된 값을 일치 하지 않습니다.

