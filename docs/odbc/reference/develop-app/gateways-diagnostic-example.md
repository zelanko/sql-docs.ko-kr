---
title: "게이트웨이 진단 예 | Microsoft Docs"
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
- diagnostic information [ODBC], examples
- gateway diagnostic [ODBC]
- error messages [ODBC], diagnostic messages
ms.assetid: e0695fac-4593-4b3d-8675-cb8f73dab966
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f31f5f97bafc7cd53972f83fa39ac10ea2554de5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="gateways-diagnostic-example"></a>게이트웨이 진단 예제
게이트웨이 아키텍처는 드라이버는 ODBC를 지 원하는 게이트웨이에 요청을 보냅니다. 게이트웨이 DBMS에는 요청을 보냅니다. 드라이버 관리자와 교류 하는 구성 요소 이므로 드라이버 포맷 하 고 반환에 대 한 인수 **SQLGetDiagRec**합니다.  
  
 예를 들어 Oracle 게이트웨이 Rdb Microsoft 개방형 데이터 서비스 및 기반 Rdb 직원 테이블을 찾을 수 하는 경우, 게이트웨이 진단이 메시지를 생성할 수 있습니다.  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 데이터 원본에 오류가 발생 게이트웨이 진단 메시지에 데이터 원본 식별자 ([Rdb])에 대 한 접두사를 추가 합니다. 게이트웨이 데이터 원본과 역시 주는 구성 요소, 때문에 진단 메시지를 해당 공급 업체 ([DEC]) 및 식별자 ([ODS 게이트웨이])에 대 한 접두사를 추가 합니다. 또한 진단 메시지의 시작 부분에는 SQLSTATE 값과 Rdb 오류 코드 추가. 이 허용 하는 자체 메시지 구조의 의미 체계를 보존 하 고 여전히 드라이버는 ODBC 진단 정보를 제공 합니다. 드라이버는 게이트웨이에 의해 error 문을에 연결 된 오류 정보를 구문 분석 합니다.  
  
 게이트웨이 드라이버가 드라이버 관리자와 교류 하는 구성 요소 이므로 사용 한다는 이전 진단 메시지에 서식을 지정 하 고 다음 값이 반환 **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```

