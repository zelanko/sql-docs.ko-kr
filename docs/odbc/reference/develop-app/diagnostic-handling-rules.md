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
manager: craigg
ms.openlocfilehash: 9f59953dee77453bb8b453a40a36d17e865a1fe5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63034930"
---
# <a name="diagnostic-handling-rules"></a>진단 처리 규칙
다음 규칙에 따라 진단 처리 **SQLGetDiagRec** 하 고 **SQLGetDiagField**합니다.  
  
 모든 ODBC 구성 요소:  
  
-   해야 하지 대체, 변경 또는 오류 또는 경고를 다른 ODBC 구성 요소에서 받은 마스크 합니다.  
  
-   다른 ODBC 구성 요소에서 진단 메시지를 받을 때 추가 상태 레코드를 추가할 수 있습니다. 추가 된 레코드는 원본 메시지에 실제 정보 값을 추가 해야 합니다.  
  
 Odbc 구성 요소는 데이터 원본을 직접 인터페이스:  
  
-   해당 공급 업체 id, 해당 구성 요소 식별자 및 진단 데이터 원본에서 수신한 메시지에 대 한 데이터 원본의 식별자를 접두사로 해야 합니다.  
  
-   데이터 원본의 원시 오류 코드를 유지 해야 합니다.  
  
-   데이터 원본의 진단 메시지를 유지 해야 합니다.  
  
 오류 또는 데이터 원본에 관계 없이 경고를 생성 하는 모든 ODBC 구성 요소:  
  
-   오류 또는 경고에 대 한 올바른 SQLSTATE를 제공 해야 합니다.  
  
-   진단 메시지의 텍스트를 생성 해야 합니다.  
  
-   해당 공급 업체 id 및 해당 구성 요소 식별자 진단 메시지를 붙여야 합니다.  
  
-   사용 가능 하 고 의미 있는 경우에 원시 오류 코드를 반환 해야 합니다.  
  
 ODBC 구성 요소에 대 한 드라이버 관리자를 사용 하 여 인터페이스입니다.  
  
-   출력 인수를 초기화 해야 합니다 **SQLGetDiagRec** 하 고 **SQLGetDiagField**합니다.  
  
-   형식과의 출력 인수로 진단 정보를 반환 해야 합니다 **SQLGetDiagRec** 하 고 **SQLGetDiagField** 해당 함수가 호출 될 때입니다.  
  
 하나의 ODBC 구성 요소 이외의 드라이버 관리자:  
  
-   기본 오류에 따라 SQLSTATE를 설정 해야 합니다. 파일 기반 드라이버와 게이트웨이 사용 하지 않는 DBMS 기반 드라이버에 대 한 드라이버는 SQLSTATE를 설정 해야 합니다. 게이트웨이 사용 하는 DBMS 기반 드라이버, 드라이버 또는 게이트웨이 지 원하는 ODBC SQLSTATE를 설정할 수 있습니다.
