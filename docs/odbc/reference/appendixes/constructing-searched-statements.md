---
title: "문을 검색 구성 | Microsoft Docs"
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
- searched statements [ODBC]
- ODBC cursor library [ODBC], statement processing
- ODBC cursor library [ODBC], searched statements
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- cursor library [ODBC], searched statements
- SQL statements [ODBC], searched statements
ms.assetid: e429254c-c43f-4fbf-98b2-5f1ed53501ff
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 90464acc97539252ae24aa6f959c16f58465d715
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="constructing-searched-statements"></a>문을 검색 구성
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 커서 라이브러리 구문을 검색 하 여 위치 지정된 업데이트를 지원 및 delete 문, **업데이트** 또는 **삭제** 위치 지정 문에서 문입니다. 에 대 한 호출을 지원 하기 위해 **SQLGetData** 커서 라이브러리를 데이터 블록에는 검색 결과 생성 **선택** 문의 결과 만들 데이터의 현재 행을 포함 하는 집합이 있습니다. 다음이 문 중 각는 **여기서** 절에 SQL_DESC_SEARCHABLE 필드 식별자 SQL_PRED_SEARCHABLE 또는 SQL_PRED_BASIC 반환 바인딩된 각 열에 대 한 캐시에 저장 된 값을 열거  **SQLColAttribute**합니다.  
  
> [!CAUTION]  
>  **여기서** 절 현재 행을 식별 하는 커서 라이브러리에서 생성 된 모든 행을 식별 하 고, 다른 행을 식별 또는 둘 이상의 행을 식별 되지 않을 수 있습니다.  
  
 위치 지정된 update 또는 delete 문이 둘 이상의 행에 영향을 커서 라이브러리에 커서가 배치 되 고 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01001 (커서 작업 충돌)를 반환 하는 행에 대해서만 행 상태 배열이 업데이트 합니다. 문이 행을 식별 하지 않으면, 커서 라이브러리 행 상태 배열이 업데이트 되지 않으며 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01001 (커서 작업 충돌)를 반환 합니다. 응용 프로그램에서 호출할 수 **SQLRowCount** 업데이트 되거나 삭제 된 행 수를 결정 합니다.  
  
 경우는 **선택** 절에 대 한 호출에 대 한 커서를 배치 하는 데도 **SQLGetData** 둘 이상의 행을 식별 **SQLGetData** 올바른 데이터를 반환 하는 보장 되지 않습니다. 모든 행을 식별 하지 못할 경우 **SQLGetData** SQL_NO_DATA를 반환 합니다.  
  
 다음 지침을 따르면 응용 프로그램의 **여기서** 절 커서 라이브러리에서 생성 된 데이터 원본에 중복을 포함 하는 경우와 같은 수 없는 경우를 제외 하 고 현재 행을 고유 하 게 식별 해야 행 수입니다.  
  
-   **행을 고유 하 게 식별 하는 열을 바인딩하십시오.** 바인딩된 열이 행에 고유 하 게 나타내지 않으면는 **여기서** 커서 라이브러리에서 생성 한 절 하나 이상의 행을 식별할 수 있습니다. 위치 지정된 update 또는 delete 문에 절을 둘 이상의 행을 업데이트 하거나 삭제할 발생할 수 있습니다. 에 대 한 호출에서 **SQLGetData**, 이와 같은 절에 잘못 된 행에 대 한 데이터를 반환 하는 드라이버 발생할 수 있습니다. 고유 키의 모든 열을 바인딩 각 행은 고유 하 게 식별 하도록 보장 합니다.  
  
-   **잘림을 방지 하는 데이터 버퍼 충분히 할당 합니다.** 커서 라이브러리의 캐시는 결과 집합에 바인딩된 행 집합 버퍼에 있는 값의 복사본 **SQLBindCol**합니다. 이러한 버퍼에 배치 된 경우 데이터가 잘리면 캐시에 잘릴 수도 있습니다. A **여기서** 절 잘린된 값에서 생성 된 데이터 원본에 기본 행을 올바르게 식별 되지 수도 있습니다.  
  
-   **이진 C 데이터에 null이 아닌 길이 버퍼를 지정 합니다.** 경우에만 해당 캐시에 길이 버퍼를 할당 하는 커서 라이브러리는 *StrLen_or_IndPtr* 인수에 **SQLBindCol** null입니다. 때는 *TargetType* 인수는 SQL_C_BINARY, 커서 라이브러리를 생성 하는 이진 데이터의 길이 필요는 **여기서** 데이터에서 절. SQL_C_BINARY 열 및 응용 프로그램 호출에 대 한 길이 버퍼가 없는 경우 **SQLGetData** 위치 지정된 업데이트 실행 또는 delete 문의 SQL_ERROR 및 SQLSTATE SL014 커서 라이브러리 반환을 시도 하거나 (한 위치 지정 요청을 실행 및 열 개수 필드 중 일부만 버퍼링 된).  
  
-   **Null 허용 열에 대 한 null이 아닌 길이 버퍼를 지정 합니다.** 경우에만 해당 캐시에 길이 버퍼를 할당 하는 커서 라이브러리는 *StrLen_or_IndPtr* 인수에 **SQLBindCol** null입니다. SQL_NULL_DATA 길이 버퍼에 저장 되므로, 커서 라이브러리는 버퍼 길이 없음에 대 한 지정 된 모든 열은 null을 허용 하지 가정 합니다. 커서 라이브러리 생성에 대해 null 허용 열 길이 열이 지정 하는 경우는 **여기서** 열에 대 한 데이터 값을 사용 하는 절. 이 절은 행을 올바르게 식별 되지 않습니다.

