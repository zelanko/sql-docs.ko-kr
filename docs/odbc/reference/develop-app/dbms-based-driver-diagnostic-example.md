---
title: DBMS 기반 드라이버 진단 예제 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 117f43548d2b57233dea6f7423e6bad67b6233b0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304354"
---
# <a name="dbms-based-driver-diagnostic-example"></a>DBMS 기반 드라이버 진단 예제
DBMS 기반 드라이버는 DBMS에 요청을 보내고 드라이버 관리자를 통해 응용 프로그램에 정보를 반환합니다. 드라이버는 드라이버 관리자와 인터페이스하는 구성 요소이므로 **SQLGetDiagRec**에 대한 인수를 서식을 지정하고 반환합니다.  
  
 예를 들어 Oracle Rdb의 Microsoft 드라이버인 SQL/Services를 사용하여 잘못된 커서 이름이 발생한 경우 **SQLGetDiagRec에서**다음 값을 반환할 수 있습니다.  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 드라이버에서 오류가 발생했기 때문에 공급업체([Microsoft]))와 드라이버([ODBC Rdb 드라이버])에 대한 진단 메시지에 접두사를 추가했습니다.  
  
 DBMS가 EMPLOYEE 테이블을 찾을 수 없는 경우 드라이버는 **SQLGetDiagRec에서**다음 값을 서식 을 지정하고 반환할 수 있습니다.  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 데이터 원본에서 오류가 발생했기 때문에 드라이버는 진단 메시지에 데이터 원본 식별자([Rdb])에 대한 접두사를 추가했습니다. 드라이버는 데이터 원본과 인터페이스하는 구성 요소이기 때문에 진단 메시지에 공급업체([Microsoft]))와 식별자([ODBC Rdb Driver])에 대한 접두사를 추가했습니다.
