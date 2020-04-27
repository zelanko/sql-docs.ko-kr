---
title: 검색 문 생성 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8b9a27aa9fc84aadc6659993de3e12e269631d2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284743"
---
# <a name="constructing-searched-statements"></a>검색된 문 생성
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 위치 지정 update 및 delete 문을 지원 하기 위해 커서 라이브러리는 위치 지정 문에서 검색 된 **update** 또는 **delete** 문을 생성 합니다. 데이터 블록에서 **SQLGetData** 호출을 지원 하기 위해 커서 라이브러리는 검색 된 **SELECT** 문을 생성 하 여 데이터의 현재 행을 포함 하는 결과 집합을 만듭니다. 이러한 각 문에서 **where** 절은 **sqlcolattribute**의 SQL_DESC_SEARCHABLE 필드 식별자에 대 한 SQL_PRED_SEARCHABLE 또는 SQL_PRED_BASIC를 반환 하는 각 바인딩된 열의 캐시에 저장 된 값을 열거 합니다.  
  
> [!CAUTION]  
>  현재 행을 식별 하기 위해 커서 라이브러리로 생성 된 **where** 절은 행을 식별 하거나 다른 행을 식별 하거나 둘 이상의 행을 식별 하는 데 실패할 수 있습니다.  
  
 위치 지정 update 또는 delete 문이 두 개 이상의 행에 영향을 주는 경우 커서 라이브러리는 커서가 위치한 행에 대해서만 행 상태 배열을 업데이트 하 고 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01001 (커서 작업 충돌)를 반환 합니다. 문이 행을 식별 하지 않으면 커서 라이브러리는 행 상태 배열을 업데이트 하지 않고 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01001 (커서 작업 충돌)를 반환 합니다. 응용 프로그램은 **Sqlrowcount** 를 호출 하 여 업데이트 되거나 삭제 된 행의 수를 확인할 수 있습니다.  
  
 **Sqlgetdata** 호출을 위해 커서를 배치 하는 데 사용 되는 **SELECT** 절이 둘 이상의 행을 식별 하는 경우 **sqlgetdata** 는 올바른 데이터를 반환 하지 않을 수 있습니다. 행을 식별 하지 않으면 **SQLGetData** SQL_NO_DATA 반환 합니다.  
  
 응용 프로그램이 다음 지침을 준수 하는 경우 데이터 원본에 중복 행이 포함 되어 있는 경우와 같이 커서 라이브러리에 의해 생성 된 **where** 절에서 현재 행을 고유 하 게 식별 해야 합니다.  
  
-   **행을 고유 하 게 식별 하는 열을 바인딩합니다.** 바인딩된 열이 행을 고유 하 게 식별 하지 않으면 커서 라이브러리에 의해 생성 된 **where** 절에서 두 개 이상의 행을 식별할 수 있습니다. 위치 지정 update 또는 delete 문에서 이러한 절을 지정 하면 둘 이상의 행이 업데이트 되거나 삭제 될 수 있습니다. **SQLGetData**호출에서 이러한 절은 드라이버가 잘못 된 행에 대 한 데이터를 반환할 수 있습니다. 고유 키의 모든 열을 바인딩하면 각 행이 고유 하 게 식별 됩니다.  
  
-   **잘림이 발생 하지 않을 정도로 많은 데이터 버퍼를 할당 합니다.** 커서 라이브러리의 캐시는 **SQLBindCol**을 사용 하 여 결과 집합에 바인딩된 행 집합 버퍼에 있는 값의 복사본입니다. 이러한 버퍼에 배치 될 때 데이터가 잘린 경우 캐시 에서도 잘립니다. 잘린 값에서 생성 된 **where** 절이 데이터 원본의 기본 행을 제대로 식별 하지 못할 수 있습니다.  
  
-   **이진 C 데이터에 null이 아닌 길이 버퍼를 지정 하십시오.** **SQLBindCol** 의 *StrLen_or_IndPtr* 인수가 null이 아닌 경우에만 커서 라이브러리에서 해당 캐시에 길이 버퍼를 할당 합니다. *TargetType* 인수가 SQL_C_BINARY 경우 커서 라이브러리에서 데이터의 **where** 절을 생성 하려면 이진 데이터의 길이가 필요 합니다. SQL_C_BINARY 열에 대 한 길이 버퍼가 없고 응용 프로그램이 **SQLGetData** 를 호출 하거나 위치 지정 update 또는 delete 문을 실행 하려고 시도 하면 커서 라이브러리는 SQL_ERROR 및 SQLSTATE SL014을 반환 합니다. 배치 된 요청은 실행 되었으며 일부 열 개수 필드는 버퍼링 되지 않았습니다.  
  
-   **Null을 허용 하는 열에 null이 아닌 길이 버퍼를 지정 하십시오.** **SQLBindCol** 의 *StrLen_or_IndPtr* 인수가 null이 아닌 경우에만 커서 라이브러리에서 해당 캐시에 길이 버퍼를 할당 합니다. SQL_NULL_DATA는 길이 버퍼에 저장 되므로 커서 라이브러리는 길이 버퍼가 지정 되지 않은 열이 null을 허용 하지 않는 것으로 가정 합니다. Nullable 열에 대해 length 열을 지정 하지 않으면 커서 라이브러리는 열에 대 한 데이터 값을 사용 하는 **where** 절을 생성 합니다. 이 절은 행을 올바르게 식별 하지 않습니다.
