---
title: 드라이버의 종류 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304874"
---
# <a name="types-of-drivers"></a>드라이버 형식
ODBC 드라이버는 다음과 같이 분류할 수 있습니다.  
  
-   **32 비트 ODBC 2.**  
     ** _x_ 드라이버** A 32비트 드라이버:  
  
    -   ODBC *2.x* 함수만 내보전합니다.  
  
    -   동작 변경에 대한 ODBC *2.x* 동작을 나타낸다.  
  
-   **ISO 및 개방형 그룹 준수 드라이버** 32비트 드라이버:  
  
    -   오픈 그룹 또는 ISO CLI 문서에 설명된 모든 함수를 내보올수 있습니다. 여기에는 ODBC에서 더 이상 사용되지 않는 일부 기능이 포함됩니다.  
  
    -   동작 변경에 대한 ODBC 3.0 동작을 나타낸다.  
  
    -   반드시 ODBC 3.0 드라이버 관리자를 통해 이동 하지 않습니다.  
  
-   **ODBC 3.0 드라이버** 32비트 드라이버:  
  
    -   ODBC 3.0에 있는 함수에서 더 이상 사용되지 않는 함수를 뺀 함수만 내보전합니다.  
  
    -   SQL_ATTR_APP_ODBC_VERSION 환경 특성에 따라 동작 변경과 관련하여 ODBC *2.x* 동작 또는 ODBC 3.0 동작을 나타낼 수 있습니다.  
  
-   **ODBC 3.5 이상( 또는 그 이상) ANSI 드라이버** 32비트 드라이버:  
  
    -   ODBC 3.5에 있는 함수에서 더 이상 사용되지 않는 함수를 뺀 함수만 내보전합니다.  
  
    -   SQL_ATTR_APP_ODBC_VERSION 환경 특성에 따라 ODBC *2.x* 동작 또는 ODBC 3.0 동작 또는 동작 변경과 관련하여 ODBC 3.5 동작을 나타낼 수 있습니다.  
  
-   **ODBC 3.5(이상) 유니코드 드라이버** 32비트 드라이버:  
  
    -   ODBC 3.5 ANSI 드라이버의 모든 기능을 지원합니다.  
  
    -   모든 ODBC 문자열 API의 유니코드 버전을 내보올 수 있습니다.  
  
    -   데이터 원본에 유니코드 데이터를 저장하고 처리할 수 있습니다.  
  
> [!NOTE]  
>  16비트 ODBC 드라이버는 ODBC *3.x* 드라이버 관리자와 직접 작동하지 않습니다. 그러나 16비트 드라이버는 2.0 ODBC 드라이버 관리자와 함께 작업할 수 있으며, 이 관리자는 *3.x* 드라이버 관리자까지 이동합니다.
