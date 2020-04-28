---
title: 드라이버 유형 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de6d8e1473f127d28c69969e0fc298afd69d3023
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304874"
---
# <a name="types-of-drivers"></a>드라이버 형식
ODBC 드라이버는 다음과 같이 분류할 수 있습니다.  
  
-   **32 비트 ODBC 2.**  
     ** _x_ driver** A 32 비트 드라이버는 다음과 같습니다.  
  
    -   ODBC 2.x 함수만 *내보냅니다.*  
  
    -   동작 변경에 대 *한 ODBC 2.x* 동작을 보여 주는 것입니다.  
  
-   **ISO 및 오픈 그룹 호환 드라이버** 32 비트 드라이버는 다음과 같습니다.  
  
    -   Open Group 또는 ISO CLI 문서에 설명 된 모든 함수를 내보냅니다. 여기에는 ODBC에서 더 이상 사용 되지 않는 함수가 포함 됩니다.  
  
    -   동작 변경에 대 한 ODBC 3.0 동작을 보여 주는 것입니다.  
  
    -   는 ODBC 3.0 드라이버 관리자를 반드시 수행 해야 하는 것은 아닙니다.  
  
-   **ODBC 3.0 드라이버** 32 비트 드라이버는 다음과 같습니다.  
  
    -   ODBC 3.0에서 사용 되지 않는 함수를 제외한 함수만 내보냅니다.  
  
    -   는 SQL_ATTR_APP_ODBC_VERSION 환경 특성에 따라 동작 변경에 대해 ODBC 2.x 동작 또는 ODBC 3.0 동작을 적용할 *수 있습니다.*  
  
-   **ODBC 3.5 이상 ANSI 드라이버** 32 비트 드라이버는 다음과 같습니다.  
  
    -   ODBC 3.5에서 사용 되지 않는 함수를 제외한 함수만 내보냅니다.  
  
    -   는 SQL_ATTR_APP_ODBC_VERSION 환경 특성을 기반으로 하 여 동작 변경에 대해 odbc 2.x 동작 또는 ODBC 3.0 동작 또는 ODBC 3.5 동작을 적용할 *수 있습니다.*  
  
-   **ODBC 3.5 이상 유니코드 드라이버** 32 비트 드라이버는 다음과 같습니다.  
  
    -   는 ODBC 3.5 ANSI 드라이버의 모든 기능을 지원 합니다.  
  
    -   모든 ODBC 문자열 Api의 유니코드 버전을 내보냅니다.  
  
    -   는 데이터 원본에 유니코드 데이터를 저장 하 고 처리할 수 있습니다.  
  
> [!NOTE]  
>  16 비트 ODBC 드라이버는 ODBC *3.X 드라이버 관리자* 에서 직접 작동 하지 않습니다. 그러나 16 비트 드라이버는 2.0 ODBC 드라이버 관리자와 함께 작동할 수 있으며, 그 후에는 *3. x* 드라이버 관리자의 썽크를 사용 합니다.
