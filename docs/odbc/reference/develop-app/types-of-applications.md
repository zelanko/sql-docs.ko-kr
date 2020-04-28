---
title: 응용 프로그램 유형 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305534"
---
# <a name="types-of-applications"></a>애플리케이션 형식
ODBC 응용 프로그램은 다음과 같이 분류할 수 있습니다.  
  
-   **순수한 ODBC 2.**  
     ** _x_ 응용 프로그램** 은 다음을 수행 하는 32 비트 응용 프로그램입니다.  
  
    -   는 ODBC 2만 호출 합니다. *x* 함수 (ODBC 1.0 함수 **SQLSetParam**포함) 여기에는 ODBC 1이 포함 됩니다. 32 비트로 이식 된 *x* 응용 프로그램  
  
    -   ODBC 2가 필요 합니다. 동작 변경이 있는 기능의 *x* 동작입니다. 자세한 내용은 [동작 변경 내용](../../../odbc/reference/develop-app/behavioral-changes.md) 을 참조 하세요.  
  
    -   이 ODBC 3.5 헤더를 사용 하 여 다시 컴파일되지 않은 경우  
  
-   **순수한 ODBC 2.**  
     **_x_ 다시 컴파일된 응용 프로그램** 순수 ODBC 2 ODBCVER = 0x0250을 설정 하 여 ODBC 3.5 헤더 파일을 사용 하 여 다시 컴파일된 *x* 응용 프로그램입니다.  
  
-   **순수한 ODBC 2.**  
     **_x_ 유니코드 응용 프로그램** 순수 ODBC 2. 유니코드로 호환 되 고 SQL_WCHAR 데이터 형식을 사용 하는 *x* 다시 컴파일된 응용 프로그램입니다.  
  
-   **순수한 오픈 그룹 및 ISO**-**규격 ODBC 응용 프로그램** 은 다음을 수행 하는 32 비트 응용 프로그램입니다.  
  
    -   Open Group 또는 ISO CLI 표준에 정의 된 함수를 호출 합니다. 이러한 함수는 사용 되지 않는 3.0 함수를 포함할 수 있습니다.  
  
    -   는 유니코드 데이터 형식을 사용 하지 않습니다.  
  
    -   동작이 변경 된 기능에 대해 ODBC 3.0 동작이 필요 합니다.  
  
-   **순수 ODBC 3.0 응용 프로그램** 32 비트 응용 프로그램은 다음과 같습니다.  
  
    -   는 3.0 헤더로 컴파일됩니다.  
  
    -   는 더 이상 사용 되지 않는 ODBC 3.0 함수를 호출 합니다.  
  
    -   동작이 변경 된 기능에 대해 ODBC 3.0 동작이 필요 합니다.  
  
-   **순수 ODBC 3.5 응용 프로그램** 32 또는 64 비트 응용 프로그램:  
  
    -   유니코드 데이터 형식을 사용할 수 있습니다.  
  
    -   는 더 이상 사용 되지 않는 ODBC 3.5 함수를 호출 합니다.  
  
    -   동작이 변경 된 기능에 대해 ODBC 3.5 동작이 필요 합니다.  
  
-   **순수한 ODBC 3.8 이상 응용 프로그램** 다음을 수행 하는 32 비트 또는 64 비트 응용 프로그램입니다.  
  
    -   유니코드 데이터 형식을 사용할 수 있습니다.  
  
    -   는 더 이상 사용 되지 않는 ODBC 3.8 함수를 호출 합니다.  
  
    -   동작이 변경 된 기능에 대해 ODBC 3.8 동작이 필요 합니다.  
  
-   **바뀐 응용 프로그램** 32 또는 64 비트 응용 프로그램:  
  
    -   중복 된 기능의 새 동작을 구현 합니다.  
  
    -   는 조건부 코드 내 에서만 ODBC의 최신 버전에 있는 새로운 기능을 사용 합니다.  
  
    -   는 동작 변경 내용을 처리 하기 위해 제한 된 조건부 코드를 포함 하거나 이전 버전의 ODBC 응용 프로그램에 등록 했습니다.
