---
title: DBMS 기반 드라이버 진단 예 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e688fff2771a14d85a659ae7c69d6a515ce88f8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dbms-based-driver-diagnostic-example"></a>DBMS 기반 드라이버 진단 예제
DBMS 기반 드라이버 DBMS에 요청을 보내고 드라이버 관리자를 통해 응용 프로그램에 정보를 반환 합니다. 형식 및에 대 한 인수를 반환 합니다. 드라이버가 드라이버 관리자와 교류 하는 구성 요소 이므로 **SQLGetDiagRec**합니다.  
  
 예를 들어 SQL/Services, Microsoft 드라이버를 Oracle Rdb 된 잘못 된 커서 이름을 발견 했습니다.를 사용 하는 경우 다음 값에서 반환할 수 있습니다 **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 드라이버에서 오류가 발생 있으므로 접두사에 추가 진단 메시지 ([Microsoft]) 공급 업체 및 드라이버 ([ODBC Rdb 드라이버]).  
  
 드라이버 수 형식과에서 다음 값을 반환 DBMS 직원 테이블을 찾을 수 없는, 경우 **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 데이터 원본에 오류가 발생 드라이버 진단 메시지에 데이터 원본 식별자 ([Rdb])에 대 한 접두사를 추가 합니다. 드라이버는 데이터 원본과 역시 주는 구성 요소, 때문에 진단 메시지를 해당 공급 업체 ([Microsoft]) 및 식별자 ([ODBC Rdb 드라이버])에 대 한 접두사를 추가 합니다.
