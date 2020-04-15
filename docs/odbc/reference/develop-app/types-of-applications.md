---
title: 응용 프로그램의 종류 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], application types
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application upgrades [ODBC], application types
- application compatibility issues [ODBC]
ms.assetid: d346a64e-a32c-4153-a40f-5b53c2f57ef2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f14326c9cec1eb89e431154c91b680e4688fcdfa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305534"
---
# <a name="types-of-applications"></a>애플리케이션 형식
ODBC 응용 프로그램은 다음과 같이 분류할 수 있습니다.  
  
-   **순수 ODBC 2.**  
     ** _x_ 응용 프로그램** A 32 비트 응용 프로그램:  
  
    -   ODBC 2만 호출합니다. *x* 함수(ODBC 1.0 함수 **SQLSetParam**포함). 여기에는 ODBC 1이 포함됩니다. *32비트로* 포팅된 x 응용 프로그램입니다.  
  
    -   ODBC 2를 기대합니다. *동작* 변경이 있는 기능에 대한 x 동작입니다. (자세한 내용은 [행동 변경](../../../odbc/reference/develop-app/behavioral-changes.md) 사항을 참조하십시오.)  
  
    -   ODBC 3.5 헤더로 다시 컴파일되지 않았습니다.  
  
-   **순수 ODBC 2.**  
     **_x_ 다시 컴파일 된 응용 프로그램** 순수 ODBC 2. ODBC3.5 헤더 파일을 사용하여 다시 컴파일된 *x* 응용 프로그램은 ODBCVER=0x0250을 설정합니다.  
  
-   **순수 ODBC 2.**  
     **_x_ 유니코드 응용 프로그램** 순수 ODBC 2. *유니코드를* 준수하고 SQL_WCHAR 데이터 형식을 사용하는 x 다시 컴파일된 응용 프로그램입니다.  
  
-   **순수 오픈 그룹 및 ISO**-**준수 ODBC 응용 프로그램** 32 비트 응용 프로그램:  
  
    -   오픈 그룹 또는 ISO CLI 표준에 정의된 함수를 호출합니다. 이러한 함수에는 더 이상 사용되지 않습니다 3.0 함수가 포함될 수 있습니다.  
  
    -   유니코드 데이터 형식을 사용하지 않습니다.  
  
    -   동작 이 변경된 기능에 대해 ODBC 3.0 동작을 예상합니다.  
  
-   **순수 ODBC 3.0 애플리케이션** 다음과 같은 32비트 응용 프로그램입니다.  
  
    -   3.0 헤더로 컴파일됩니다.  
  
    -   더 이상 사용되지 않는 함수를 포함하여 모든 ODBC 3.0 함수를 호출합니다.  
  
    -   동작 이 변경된 기능에 대해 ODBC 3.0 동작을 예상합니다.  
  
-   **순수 ODBC 3.5 애플리케이션** 32 비트 또는 64 비트 응용 프로그램:  
  
    -   유니코드 데이터 형식을 사용할 수 있습니다.  
  
    -   더 이상 사용되지 않는 함수를 포함하여 모든 ODBC 3.5 함수를 호출합니다.  
  
    -   동작 변경이 있는 기능에 대해 ODBC 3.5 동작을 예상합니다.  
  
-   **순수 ODBC 3.8(이상) 응용 프로그램** 32비트 또는 64비트 응용 프로그램:  
  
    -   유니코드 데이터 형식을 사용할 수 있습니다.  
  
    -   더 이상 사용되지 않는 함수를 포함하여 모든 ODBC 3.8 함수를 호출합니다.  
  
    -   동작 변경이 있는 기능에 대해 ODBC 3.8 동작을 예상합니다.  
  
-   **대체된 응용 프로그램** 32 비트 또는 64 비트 응용 프로그램:  
  
    -   중복된 기능에 대한 새 동작을 구현합니다.  
  
    -   ODBC의 이후 버전에서 만 조건부 코드 내에서 새로운 기능을 사용합니다.  
  
    -   동작 변경을 처리하기 위한 조건부 코드가 제한되어 있거나 ODBC 응용 프로그램의 이전 버전으로 등록되었습니다.
