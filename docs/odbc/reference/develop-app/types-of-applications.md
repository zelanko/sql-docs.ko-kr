---
title: 응용 프로그램 유형의 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e46075e55aa14784e967b3620de5855a47c4bd6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47676621"
---
# <a name="types-of-applications"></a>응용 프로그램 형식
ODBC 응용 프로그램은 다음과 같이 분류할 수 있습니다.  
  
-   **순수 ODBC 2입니다.**  
     ***x* 응용 프로그램** 32 비트 응용 프로그램입니다.  
  
    -   ODBC 2를 호출합니다. *x* 함수 (ODBC 1.0 함수를 포함 하 여 **SQLSetParam**). 여기에 ODBC 1이 포함 됩니다. *x* 응용 프로그램을 32 비트로 이식 되었습니다.  
  
    -   ODBC 2는 필요합니다. *x* 동작 변경 내용 했던 기능에 대 한 동작입니다. (참조 [동작 변경 내용](../../../odbc/reference/develop-app/behavioral-changes.md) 자세한.)  
  
    -   컴파일되지 않은 ODBC 3.5 헤더를 사용 하 여 합니다.  
  
-   **순수 ODBC 2입니다.**  
     ***x* 응용 프로그램 다시 컴파일할** 순수 ODBC 2. *x* 다시 컴파일 했음을 ODBC 3.5 헤더 파일을 사용 하는 응용 프로그램 = 0x0250 ODBCVER를 설정 합니다.  
  
-   **순수 ODBC 2입니다.**  
     ***x* 유니코드 응용 프로그램** 순수 ODBC 2. *x* 유니코드 규격이 고 SQL_WCHAR 데이터 형식을 사용 하는 응용 프로그램을 다시 컴파일됩니다.  
  
-   **순수 Open Group 및 ISO**–**호환 ODBC 응용 프로그램** 32 비트 응용 프로그램입니다.  
  
    -   Open Group 또는 ISO CLI 표준에 정의 된 함수를 호출 합니다. (이러한 함수에 사용 되지 않는 3.0 함수를 포함할 수 있습니다.)  
  
    -   유니코드 데이터 형식을 사용 하지 않습니다.  
  
    -   동작 변경 내용 했던 기능에 대 한 ODBC 3.0 동작을 예상 합니다.  
  
-   **순수 ODBC 3.0 응용 프로그램** 32 비트 응용 프로그램입니다.  
  
    -   3.0 헤더를 사용 하 여 컴파일됩니다.  
  
    -   포함 되지 않은 모든 ODBC 3.0 함수를 호출 합니다.  
  
    -   동작 변경 내용 했던 기능에 대 한 ODBC 3.0 동작을 예상 합니다.  
  
-   **순수 ODBC 3.5 응용 프로그램** 32 또는 64 비트 응용 프로그램입니다.  
  
    -   유니코드 데이터 형식을 사용할 수 있습니다.  
  
    -   포함 되지 않은 모든 ODBC 3.5 함수를 호출 합니다.  
  
    -   동작 변경 내용 했던 기능에 대 한 ODBC 3.5 동작을 예상 합니다.  
  
-   **순수 ODBC 3.8 이상에 응용 프로그램** 32 비트 또는 64 비트 응용 프로그램입니다.  
  
    -   유니코드 데이터 형식을 사용할 수 있습니다.  
  
    -   포함 되지 않은 모든 ODBC 3.8 함수를 호출 합니다.  
  
    -   동작 변경 내용 했던 기능에 대 한 ODBC 3.8 동작을 예상 합니다.  
  
-   **응용 프로그램 대체** 32 또는 64 비트 응용 프로그램입니다.  
  
    -   중복 된 기능에 대 한 새 동작을 구현 합니다.  
  
    -   조건부 코드 에서만 ODBC의 이후 버전에서 새로운 기능을 사용합니다.  
  
    -   제한적으로 조건부 처리 하는 코드 동작 변경 내용 또는 이전 버전의 ODBC 응용 프로그램에 등록 되어 있습니다.
