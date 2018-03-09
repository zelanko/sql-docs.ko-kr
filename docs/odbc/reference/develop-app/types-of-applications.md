---
title: "응용 프로그램의 종류 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading applications [ODBC], application types
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application upgrades [ODBC], application types
- application compatibility issues [ODBC]
ms.assetid: d346a64e-a32c-4153-a40f-5b53c2f57ef2
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4c84327d23fba9b97bb34ff290eff06704e586df
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="types-of-applications"></a>응용 프로그램의 종류
ODBC 응용 프로그램을 다음과 같이 분류할 수 있습니다.  
  
-   **순수 ODBC 2입니다.**  
     ***x* 응용 프로그램** 32 비트 응용 프로그램입니다.  
  
    -   ODBC 2를 호출합니다. *x* 함수 (ODBC 1.0 함수를 포함 하 여 **SQLSetParam**). 여기에 ODBC 1 포함 됩니다. *x* 응용 프로그램을 32 비트 이식 되었습니다.  
  
    -   ODBC 2는 필요합니다. *x* 동작이 변경 된 기능에 대 한 동작입니다. (참조 [변경 된 동작](../../../odbc/reference/develop-app/behavioral-changes.md) 자세한 정보에 대 한 합니다.)  
  
    -   컴파일되지 않은 ODBC 3.5 헤더와 함께 합니다.  
  
-   **순수 ODBC 2입니다.**  
     ***x* 다시 컴파일된 응용 프로그램** 순수 ODBC 2. *x* ODBC 3.5 헤더 파일을 사용 하 여 컴파일한 응용 프로그램 = 0x0250 ODBCVER를 설정 하 여 합니다.  
  
-   **순수 ODBC 2입니다.**  
     ***x* 유니코드 응용 프로그램** 순수 ODBC 2. *x* 는 유니코드 규격이 고 SQL_WCHAR 데이터 형식을 사용 하 여 응용 프로그램을 다시 컴파일됩니다.  
  
-   **순수 Open 그룹 및 ISO**–**호환 ODBC 응용 프로그램** 32 비트 응용 프로그램입니다.  
  
    -   Open Group 또는 CLI ISO 표준에 정의 된 함수를 호출 합니다. (이러한 함수에 사용 되지 않는 3.0 함수를 포함할 수 있습니다.)  
  
    -   유니코드 데이터 형식을 사용 하지 않습니다.  
  
    -   변경 된 동작 적이 있는 기능에 대 한 동작 ODBC 3.0이 필요 합니다.  
  
-   **순수 ODBC 3.0 응용 프로그램** 32 비트 응용 프로그램입니다.  
  
    -   3.0 헤더로 컴파일됩니다.  
  
    -   수를 포함 하 여 사용 되지 않습니다. 모든 ODBC 3.0 함수를 호출 합니다.  
  
    -   변경 된 동작 적이 있는 기능에 대 한 동작 ODBC 3.0이 필요 합니다.  
  
-   **순수 ODBC 3.5 응용 프로그램** 32 또는 64 비트 응용 프로그램입니다.  
  
    -   유니코드 데이터 형식을 사용할 수 있습니다.  
  
    -   수를 포함 하 여 사용 되지 않습니다. 모든 ODBC 3.5 함수를 호출 합니다.  
  
    -   변경 된 동작 적이 있는 기능에 대 한 ODBC 3.5 동작이 필요 합니다.  
  
-   **순수 ODBC 3.8 (또는 이상) 응용 프로그램** 32 비트 또는 64 비트 응용 프로그램입니다.  
  
    -   유니코드 데이터 형식을 사용할 수 있습니다.  
  
    -   수를 포함 하 여 사용 되지 않습니다. 모든 ODBC 3.8 함수를 호출 합니다.  
  
    -   변경 된 동작 적이 있는 기능에 대 한 ODBC 3.8 동작이 필요 합니다.  
  
-   **응용 프로그램을 교체** 32 또는 64 비트 응용 프로그램입니다.  
  
    -   중복 된 기능에 대 한 새 동작을 구현 합니다.  
  
    -   조건부 코드 내 에서만 ODBC의 최신 버전에서 새로운 기능을 사용합니다.  
  
    -   제한적으로 조건부 처리 하는 코드 변경 된 동작 또는 ODBC 응용 프로그램의 이전 버전 되도록 등록 되어 있습니다.
