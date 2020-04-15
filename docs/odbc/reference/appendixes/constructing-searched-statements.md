---
title: 검색된 명령문 생성 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284743"
---
# <a name="constructing-searched-statements"></a>검색된 문 생성
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 위치 업데이트 및 삭제 문을 지원하기 위해 커서 라이브러리는 위치 된 명령문에서 검색된 **UPDATE** 또는 **DELETE** 문을 생성합니다. 데이터 블록에서 **SQLGetData** 호출을 지원하기 위해 커서 라이브러리는 검색된 **SELECT** 문을 생성하여 현재 데이터 행을 포함하는 결과 집합을 만듭니다. 이러한 각 명령문에서 **WHERE** 절은 **SQLColAttribute에서**SQL_DESC_SEARCHABLE 필드 식별자에 대한 SQL_PRED_SEARCHABLE 또는 SQL_PRED_BASIC 반환하는 각 바인딩된 열에 대해 캐시에 저장된 값을 열거합니다.  
  
> [!CAUTION]  
>  현재 행을 식별하기 위해 커서 라이브러리에서 생성한 **WHERE** 절은 행을 식별하거나 다른 행을 식별하거나 두 개 이상의 행을 식별하지 못할 수 있습니다.  
  
 위치 업데이트 또는 delete 문이 두 개 이상의 행에 영향을 주는 경우 커서 라이브러리는 커서가 배치된 행에 대해서만 행 상태 배열을 업데이트하고 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01001(커서 작업 충돌)을 반환합니다. 명령문이 행을 식별하지 않으면 커서 라이브러리는 행 상태 배열을 업데이트하지 않고 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01001(커서 작업 충돌)을 반환합니다. 응용 프로그램은 **SQLRowCount를** 호출하여 업데이트되거나 삭제된 행 수를 확인할 수 있습니다.  
  
 **SQLGetData** 호출에 대 한 cursor를 배치 하는 데 사용 하는 **SELECT** 절이 두 개 이상의 행을 식별 하는 경우 **SQLGetData** 올바른 데이터를 반환 보장 되지 않습니다. 행을 식별하지 않으면 **SQLGetData가** SQL_NO_DATA 반환합니다.  
  
 응용 프로그램이 다음 지침을 준수하는 경우 데이터 원본에 중복 행이 포함된 경우와 같이 불가능한 경우를 제외하고 커서 라이브러리에서 생성한 **WHERE** 절은 현재 행을 고유하게 식별해야 합니다.  
  
-   **행을 고유하게 식별하는 열을 바인딩합니다.** 바인딩된 열이 행을 고유하게 식별하지 않는 경우 커서 라이브러리에서 생성한 **WHERE** 절은 두 개 이상의 행을 식별할 수 있습니다. 위치 가 있는 업데이트 또는 delete 문에서 이러한 절로 인해 두 개 이상의 행이 업데이트되거나 삭제될 수 있습니다. **SQLGetData를**호출할 때 이러한 절로 인해 드라이버가 잘못된 행에 대한 데이터를 반환할 수 있습니다. 고유한 키에 있는 모든 열을 바인딩하면 각 행이 고유하게 식별됩니다.  
  
-   **잘림이 발생하지 않을 만큼 큰 데이터 버퍼를 할당합니다.** 커서 라이브러리의 캐시는 **SQLBindCol로**결과 집합에 바인딩된 행 집합 버퍼의 값의 복사본입니다. 데이터가 이러한 버퍼에 배치될 때 잘린 경우 캐시에서도 잘립니다. 잘린 값으로 구성된 **WHERE** 절은 데이터 원본의 기본 행을 올바르게 식별하지 못할 수 있습니다.  
  
-   **이진 C 데이터에 대해 null이 아닌 길이 버퍼를 지정합니다.** 커서 라이브러리는 **SQLBindCol의** *StrLen_or_IndPtr* 인수가 null이 아닌 경우에만 캐시에 길이 버퍼를 할당합니다. *TargetType* 인수가 SQL_C_BINARY 커서 라이브러리는 데이터에서 **WHERE** 절을 생성하기 위해 이진 데이터의 길이가 필요합니다. SQL_C_BINARY 열에 대한 길이 버퍼가 없고 응용 프로그램에서 **SQLGetData를** 호출하거나 위치 업데이트 또는 삭제 문을 실행하려고 하면 커서 라이브러리가 SQL_ERROR 및 SQLSTATE SL014를 반환합니다(위치 지정 요청이 실행되었으며 모든 열 개 수 필드가 버퍼링되지 않음).  
  
-   **null able 열에 대해 null이 아닌 길이 버퍼를 지정합니다.** 커서 라이브러리는 **SQLBindCol의** *StrLen_or_IndPtr* 인수가 null이 아닌 경우에만 캐시에 길이 버퍼를 할당합니다. SQL_NULL_DATA 길이 버퍼에 저장되므로 커서 라이브러리는 길이 버퍼가 지정되지 않은 모든 열이 null이 아닌 것으로 가정합니다. nullable 열에 대해 길이 열을 지정하지 않으면 커서 라이브러리는 열에 대한 데이터 값을 사용하는 **WHERE** 절을 생성합니다. 이 절은 행을 올바르게 식별하지 않습니다.
