---
description: DBMS 기반 드라이버 진단 예제
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5425afb18a5582a840966798ea7a7209dba7e1e6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424745"
---
# <a name="dbms-based-driver-diagnostic-example"></a>DBMS 기반 드라이버 진단 예제
DBMS 기반 드라이버는 DBMS로 요청을 보내고 드라이버 관리자를 통해 응용 프로그램에 정보를 반환 합니다. 드라이버는 드라이버 관리자와 상호 작용 하는 구성 요소 이므로 **SQLGetDiagRec**에 대 한 인수를 포맷 하 고 반환 합니다.  
  
 예를 들어, SQL/Services를 사용 하 여 Oracle Rdb 용 Microsoft 드라이버에서 잘못 된 커서 이름을 발견 한 경우 **SQLGetDiagRec**에서 다음 값을 반환할 수 있습니다.  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 드라이버에서 오류가 발생 했기 때문에 공급 업체 ([Microsoft]) 및 드라이버 ([ODBC Rdb 드라이버])에 대 한 진단 메시지에 접두사를 추가 했습니다.  
  
 DBMS에서 EMPLOYEE 테이블을 찾을 수 없는 경우 드라이버는 **SQLGetDiagRec**에서 다음 값을 서식 지정 하 고 반환할 수 있습니다.  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 데이터 원본에서 오류가 발생 했기 때문에 드라이버에서 진단 메시지에 데이터 원본 식별자 ([Rdb])에 대 한 접두사를 추가 했습니다. 드라이버는 데이터 원본에 되 된 구성 요소 이므로 해당 공급 업체 ([Microsoft]) 및 식별자 ([ODBC Rdb 드라이버])에 대 한 접두사를 진단 메시지에 추가 했습니다.
