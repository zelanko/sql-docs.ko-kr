---
title: 검색 된 문 생성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- searched statements [ODBC]
- ODBC cursor library [ODBC], statement processing
- ODBC cursor library [ODBC], searched statements
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- cursor library [ODBC], searched statements
- SQL statements [ODBC], searched statements
ms.assetid: e429254c-c43f-4fbf-98b2-5f1ed53501ff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c8f24fe59da1377ea42900a8f1f0b89eb97125f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019174"
---
# <a name="constructing-searched-statements"></a>검색된 문 생성
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 구문을 커서 라이브러리를 검색 하 여 위치 지정된 업데이트를 지원 하 고 delete 문을 **업데이트할** 또는 **삭제** 배치 문에서 문입니다. 호출을 지원 하기 **SQLGetData** 데이터의 블록에서 커서 라이브러리를 검색 생성 **선택** 데이터의 현재 행이 포함 된 결과 만들려면 문을 설정 합니다. 다음이 문 중 각 합니다 **여기서** SQL_PRED_SEARCHABLE 또는 SQL_PRED_BASIC SQL_DESC_SEARCHABLE 필드 식별자에 대 한 반환 하는 바인딩된 각 열에 대 한 캐시에 저장 된 값을 열거 하는 절  **SQLColAttribute**합니다.  
  
> [!CAUTION]  
>  합니다 **여기서** 절 현재 행을 식별 하려면 커서 라이브러리에 의해 생성 된 모든 행을 식별 하 고, 다른 행을 식별 또는 둘 이상의 행을 식별 하지 못할 수 있습니다.  
  
 위치 지정된 update 또는 delete 문이 둘 이상의 행에 영향을 커서 라이브러리는 커서가 배치 되 고 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01001 (커서 작업이 충돌)를 반환 하는 행에 대해서만 행 상태 배열이 업데이트 됩니다. 문이 행을 식별 하지 않으면, 커서 라이브러리는 행 상태 배열이 업데이트 하지 않습니다 하 고 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01001 (커서 작업이 충돌)를 반환 합니다. 응용 프로그램에서 호출할 수 있습니다 **SQLRowCount** 업데이트 되거나 삭제 된 행의 수를 결정 합니다.  
  
 경우는 **선택** 절에 대 한 호출에 대 한 커서를 배치 하는 데 **SQLGetData** 둘 이상의 행을 식별 **SQLGetData** 올바른 데이터를 반환 하도록 보장 되지 않습니다. 모든 행을 식별 하지 못하면 **SQLGetData** SQL_NO_DATA를 반환 합니다.  
  
 다음 지침을 따르면 응용 프로그램을 **여기서** 커서 라이브러리에 의해 생성 된 절이 없는 경우 데이터 원본 복제본을 포함 하는 경우 등과 같은 가능한 제외 하 고 현재 행을 고유 하 게 식별 해야 행 수입니다.  
  
-   **행을 고유 하 게 식별 하는 열을 바인딩하십시오.** 바인딩된 열이 행에 고유 하 게 나타내지 않으면 합니다 **여기서** 절 커서 라이브러리에 의해 생성 된 둘 이상의 행을 식별할 수 있습니다. 위치 지정된 업데이트 또는 delete 문에 절을 둘 이상의 행을 업데이트 하거나 삭제할 발생할 수 있습니다. 에 대 한 호출에서 **SQLGetData**, 절을 잘못 된 행에 대 한 데이터를 반환 하는 드라이버를 발생할 수 있습니다. 고유 키의 모든 열 바인딩 각 행은 고유 하 게 식별 하는 작업을 보장 합니다.  
  
-   **잘림을 방지 하는 데이터 버퍼 충분히 할당 합니다.** 커서 라이브러리 캐시 결과 집합으로 바인딩된 행 집합 버퍼에 있는 값의 복사본 인 **SQLBindCol**합니다. 이러한 버퍼에 배치 되는 경우 데이터가 잘리면 캐시에도 잘리게 됩니다. A **여기서** 절 잘린된 값에서 생성 된 데이터 소스의 기본 행을 올바르게 식별할 수 있습니다.  
  
-   **이진 C 데이터에 대해 null이 아닌 길이 버퍼를 지정 합니다.** 커서 라이브러리는 경우에만 해당 캐시에 길이 버퍼를 할당 합니다 *StrLen_or_IndPtr* 에서 인수 **SQLBindCol** null이 아닌 합니다. 경우는 *TargetType* 인수가 SQL_C_BINARY 이면 커서 라이브러리를 사용 하는 데 이진 데이터의 길이 필요로 **여기서** 데이터로 절. SQL_C_BINARY 열 및 응용 프로그램 호출에 대 한 없습니다 길이 버퍼 인지 **SQLGetData** 위치 지정된 업데이트 실행 또는 delete 문의 SQL_ERROR 및 SQLSTATE SL014 커서 라이브러리 반환 하려고 하거나 (을 위치 지정 요청을 발행 및 모든 열 수가 필드가 버퍼링 된).  
  
-   **Null 허용 열에 대 한 null이 아닌 길이 버퍼를 지정 합니다.** 커서 라이브러리는 경우에만 해당 캐시에 길이 버퍼를 할당 합니다 *StrLen_or_IndPtr* 에서 인수 **SQLBindCol** null이 아닌 합니다. SQL_NULL_DATA에 길이 버퍼에 저장 되므로 커서 라이브러리는 버퍼 길이 없음에 대 한 지정 된 열 nullable이 아닌 이라고 가정 합니다. 커서 라이브러리를 생성 하는 길이 열은 null 허용 열에 대 한 지정 된 경우는 **여기서** 열의 데이터 값을 사용 하는 절. 이 절은 행을 올바르게 식별 하지 않습니다.
