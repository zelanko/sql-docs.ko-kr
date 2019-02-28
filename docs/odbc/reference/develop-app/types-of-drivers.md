---
title: 드라이버 종류 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
ms.assetid: 864c53c1-b68a-48b6-b6bc-5ecb520bb9dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 445fe3a0b87e6ad8e35dbc585981d874f8e357bf
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256958"
---
# <a name="types-of-drivers"></a>드라이버 형식
ODBC 드라이버는 다음과 같이 분류할 수 있습니다.  
  
-   **32 비트 ODBC 2입니다.**  
     **_x_ 드라이버** 32 비트 드라이버입니다.  
  
    -   ODBC 2만 내보냅니다 *.x* 함수입니다.  
  
    -   ODBC 2를 보여 줍니다.*x* 동작 변경 내용에 대 한 동작입니다.  
  
-   **ISO 및 열린 그룹 규격 드라이버** 32 비트 드라이버입니다.  
  
    -   Open Group 또는 ISO CLI 문서에 나와 있는 모든 함수를 내보냅니다. ODBC에서 사용 되지 않는 함수 중 일부를이 포함 됩니다.  
  
    -   동작 변경 내용에 대 한 ODBC 3.0 동작을 보여 줍니다.  
  
    -   ODBC 3.0 드라이버 관리자를 통해 반드시 이동 하지 않습니다.  
  
-   **ODBC 3.0 드라이버** 32 비트 드라이버입니다.  
  
    -   ODBC 3.0에서 뺀 값에 있는 함수만을 내보냅니다 함수를 사용 되지 않습니다.  
  
    -   ODBC 2를 나타내는 수 있습니다.*x* SQL_ATTR_APP_ODBC_VERSION 환경 특성을 기반으로 동작 또는 동작 변경 내용에 대해 ODBC 3.0 동작 합니다.  
  
-   **ODBC 3.5 (또는 이후 버전) ANSI 드라이버** 32 비트 드라이버입니다.  
  
    -   빼기 ODBC 3.5에 있는 함수만을 내보냅니다 함수를 사용 되지 않습니다.  
  
    -   ODBC 2를 나타내는 수 있습니다. *x* SQL_ATTR_APP_ODBC_VERSION 환경 특성을 기반으로 동작 또는 ODBC 3.0 동작 또는 동작 변경 내용에 대해 ODBC 3.5 동작 합니다.  
  
-   **ODBC 3.5 (또는 이상) 유니코드 드라이버** 32 비트 드라이버입니다.  
  
    -   ODBC 3.5 ANSI 드라이버의 모든 기능을 지원합니다.  
  
    -   모든 ODBC 문자열 Api의 유니코드 버전을 내보냅니다.  
  
    -   저장 하 고 데이터 원본에 유니코드 데이터를 처리할 수 있습니다.  
  
> [!NOTE]  
>  16 비트 ODBC 드라이버는 ODBC 3와 직접 작동 하지 않습니다. *x* 드라이버 관리자입니다. 그러나 이후에 3까지 썽크를 2.0 ODBC 드라이버 관리자를 사용 하 여 작동 하는 16 비트 드라이버에 대 한 가능한 것입니다. *x* 드라이버 관리자입니다.
