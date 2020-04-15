---
title: 진단 처리 규칙 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], diagnostic handling rules
- SQLGetDiagRec function [ODBC], diagnostic handling rules
- diagnostic information [ODBC], SqlGetDiagRec
ms.assetid: 74387c3a-d6b3-4c35-b209-b9612602b20a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9f7f9d19a5a369e9da0efbc0d62f8e556b0597c1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305844"
---
# <a name="diagnostic-handling-rules"></a>진단 처리 규칙
다음 규칙은 **SQLGetDiagRec** 및 **SQLGetDiagField의**진단 처리를 제어합니다.  
  
 모든 ODBC 구성 요소의 경우:  
  
-   다른 ODBC 구성 요소에서 받은 오류 또는 경고를 교체, 변경 또는 마스킹해서는 안 됩니다.  
  
-   다른 ODBC 구성 요소에서 진단 메시지를 받을 때 추가 상태 레코드를 추가할 수 있습니다. 추가된 레코드는 원본 메시지에 실제 정보 값을 추가해야 합니다.  
  
 데이터 원본을 직접 인터페이스하는 ODBC 구성 요소의 경우:  
  
-   공급업체 식별자, 구성 요소 식별자 및 데이터 원본의 식별자를 데이터 원본에서 받는 진단 메시지에 접두사를 해야 합니다.  
  
-   데이터 원본의 기본 오류 코드를 보존해야 합니다.  
  
-   데이터 원본의 진단 메시지를 보존해야 합니다.  
  
 데이터 원본과 무관하여 오류 또는 경고를 생성하는 ODBC 구성 요소의 경우:  
  
-   오류 또는 경고에 대해 올바른 SQLSTATE를 제공해야 합니다.  
  
-   진단 메시지의 텍스트를 생성해야 합니다.  
  
-   공급업체 식별자와 해당 구성 요소 식별자를 진단 메시지에 접두사로 고정해야 합니다.  
  
-   사용 가능하고 의미 있는 경우 기본 오류 코드를 반환해야 합니다.  
  
 드라이버 관리자와 인터페이스하는 ODBC 구성 요소의 경우:  
  
-   **SQLGetDiagRec** 및 **SQLGetDiagField의**출력 인수를 초기화해야 합니다.  
  
-   해당 함수가 호출될 때 진단 정보를 **SQLGetDiagRec** 및 **SQLGetDiagField의** 출력 인수로 서식을 지정하고 반환해야 합니다.  
  
 드라이버 관리자 이외의 하나의 ODBC 구성 요소의 경우:  
  
-   기본 오류에 따라 SQLSTATE를 설정해야 합니다. 게이트웨이를 사용하지 않는 파일 기반 드라이버 및 DBMS 기반 드라이버의 경우 드라이버는 SQLSTATE를 설정해야 합니다. 게이트웨이를 사용하는 DBMS 기반 드라이버의 경우 ODBC를 지원하는 드라이버 또는 게이트웨이가 SQLSTATE를 설정할 수 있습니다.
