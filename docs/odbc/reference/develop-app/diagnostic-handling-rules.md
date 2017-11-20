---
title: "규칙 처리 진단 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], diagnostic handling rules
- SQLGetDiagRec function [ODBC], diagnostic handling rules
- diagnostic information [ODBC], SqlGetDiagRec
ms.assetid: 74387c3a-d6b3-4c35-b209-b9612602b20a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7cfd05e9c41fee1e0a753e2c4e4fa4f86db641b3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="diagnostic-handling-rules"></a>진단 처리 규칙
다음 규칙에 따라 진단 처리 **SQLGetDiagRec** 및 **SQLGetDiagField**합니다.  
  
 모든 ODBC 구성 요소:  
  
-   해야 하지 대체, 변경 또는 오류 또는 경고를 다른 ODBC 구성 요소에서 받은 마스크입니다.  
  
-   다른 ODBC 구성 요소에서 진단 메시지를 받을 때 추가 상태 레코드를 추가할 수 있습니다. 추가 된 레코드를 원본 메시지 실제 정보 값을 추가 해야 합니다.  
  
 ODBC에 대 한 구성 요소는 데이터 원본을 직접 인터페이스:  
  
-   해당 공급 업체 식별자, 해당 구성 요소 식별자 및 데이터 원본에서 받은 진단 메시지를 데이터 원본 식별자를 접두사로 지정 해야 합니다.  
  
-   데이터 원본의 원시 오류 코드를 유지 해야 합니다.  
  
-   데이터 원본의 진단 메시지를 유지 해야 합니다.  
  
 오류 또는 데이터 원본에 관계 없이 경고 항목을 생성 하는 ODBC 구성 요소:  
  
-   오류 또는 경고에 대 한 올바른 SQLSTATE를 제공 해야 합니다.  
  
-   진단 메시지의 텍스트를 생성 해야 합니다.  
  
-   해당 공급 업체 식별자 및 진단 메시지에 해당 구성 요소 식별자를 접두사로 지정 해야 합니다.  
  
-   사용 가능 하 고 의미 있는 경우 원시 오류 코드를 반환 해야 합니다.  
  
 ODBC 구성 요소에 대 한 드라이버 관리자와 교류 하 합니다.  
  
-   출력 인수를 초기화 해야 **SQLGetDiagRec** 및 **SQLGetDiagField**합니다.  
  
-   서식을 지정 하 고의 출력 인수로 진단 정보를 반환 해야 **SQLGetDiagRec** 및 **SQLGetDiagField** 해당 함수가 호출 될 때입니다.  
  
 ODBC 구성 요소를 하나 드라이버 관리자 이외의에 대 한:  
  
-   원시 오류에 따라 SQLSTATE를 설정 해야 합니다. 파일 기반 드라이버 및 게이트웨이 사용 하지 않는 DBMS 기반 드라이버에 대 한 드라이버는 SQLSTATE를 설정 해야 합니다. 게이트웨이 사용 하는 DBMS 기반 드라이버, 드라이버 또는 ODBC를 지 원하는 게이트웨이 SQLSTATE를 설정할 수 있습니다.

