---
title: DBMS 기반 드라이버 진단 예제 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0485ecf720cb84580c17c77b31fc6816de2e679a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641033"
---
# <a name="dbms-based-driver-diagnostic-example"></a>DBMS 기반 드라이버 진단 예제
DBMS 기반 드라이버는 DBMS에 요청을 보내고 및 드라이버 관리자를 통해 응용 프로그램에 정보를 반환 합니다. 형식 및에 대 한 인수를 반환 합니다. 드라이버가 드라이버 관리자와 인터페이스 하는 구성 요소 이므로 **SQLGetDiagRec**합니다.  
  
 예를 들어, Oracle Rdb를 잘못 된 커서 이름을 발견 했습니다.에 대 한 SQL/Services, Microsoft 드라이버를 사용 하는 경우에서 다음 값을 반환할 수 있습니다 **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 드라이버에서 오류가 발생이 접두사에 추가 진단 메시지 ([Microsoft]) 공급 업체 및 드라이버 ([ODBC Rdb 드라이버]).  
  
 드라이버 수 형식과에서 같은 값을 반환할 DBMS 직원 테이블을 찾을 수 없습니다, 하는 경우 **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 데이터 소스의 오류 때문 드라이버 진단 메시지에 데이터 원본 식별자 ([Rdb])에 대 한 접두사를 추가 합니다. 드라이버는 데이터 원본과 되는 구성 요소, 때문에 진단 메시지를 해당 공급 업체 ([Microsoft]) 및 식별자 ([ODBC Rdb 드라이버])에 대 한 접두사를 추가 합니다.
