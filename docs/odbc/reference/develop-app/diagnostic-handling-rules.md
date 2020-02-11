---
title: 진단 처리 규칙 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 269e021d3fd4610c2fccda46bcd8ca160982543c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039921"
---
# <a name="diagnostic-handling-rules"></a>진단 처리 규칙
다음 규칙은 **SQLGetDiagRec** 및 **SQLGetDiagField**의 진단 처리를 제어 합니다.  
  
 모든 ODBC 구성 요소:  
  
-   다른 ODBC 구성 요소에서 받은 오류 또는 경고를 바꾸거나 변경 하거나 마스킹 해서는 안 됩니다.  
  
-   다른 ODBC 구성 요소에서 진단 메시지를 받을 때 추가 상태 레코드를 추가할 수 있습니다. 추가 된 레코드는 원래 메시지에 실제 정보 값을 추가 해야 합니다.  
  
 데이터 원본을 직접 인터페이스 하는 ODBC 구성 요소의 경우:  
  
-   는 공급 업체 식별자, 해당 구성 요소 식별자 및 데이터 원본의 식별자를 데이터 원본에서 받은 진단 메시지에 접두사로 붙여야 합니다.  
  
-   데이터 소스의 네이티브 오류 코드를 유지 해야 합니다.  
  
-   데이터 원본의 진단 메시지를 유지 해야 합니다.  
  
 데이터 원본에 관계 없이 오류 또는 경고를 생성 하는 ODBC 구성 요소:  
  
-   오류 또는 경고에 대 한 올바른 SQLSTATE를 제공 해야 합니다.  
  
-   진단 메시지의 텍스트를 생성 해야 합니다.  
  
-   는 해당 공급 업체 식별자와 해당 구성 요소 식별자를 진단 메시지에 접두사로 붙여야 합니다.  
  
-   사용할 수 있고 의미가 있는 경우 네이티브 오류 코드를 반환 해야 합니다.  
  
 드라이버 관리자와 상호 작용 하는 ODBC 구성 요소:  
  
-   **SQLGetDiagRec** 및 **SQLGetDiagField**의 출력 인수를 초기화 해야 합니다.  
  
-   는 해당 함수가 호출 될 때 **SQLGetDiagRec** 및 **SQLGetDiagField** 의 출력 인수로 진단 정보를 포맷 하 고 반환 해야 합니다.  
  
 드라이버 관리자 이외의 하나의 ODBC 구성 요소:  
  
-   기본 오류에 따라 SQLSTATE를 설정 해야 합니다. 게이트웨이를 사용 하지 않는 파일 기반 드라이버 및 DBMS 기반 드라이버의 경우 드라이버에서 SQLSTATE를 설정 해야 합니다. 게이트웨이를 사용 하는 DBMS 기반 드라이버의 경우 ODBC를 지 원하는 드라이버나 게이트웨이가 SQLSTATE를 설정할 수 있습니다.
