---
title: 게이트웨이 진단 예 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], examples
- gateway diagnostic [ODBC]
- error messages [ODBC], diagnostic messages
ms.assetid: e0695fac-4593-4b3d-8675-cb8f73dab966
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b18fd78be7be2eb79316339cbdf3d315deb194fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305574"
---
# <a name="gateways-diagnostic-example"></a>게이트웨이 진단 예제
게이트웨이 아키텍처에서 드라이버는 ODBC를 지원하는 게이트웨이로 요청을 보냅니다. 게이트웨이는 요청을 DBMS로 보냅니다. 드라이버 관리자와 인터페이스하는 구성 요소이기 때문에 드라이버는 **SQLGetDiagRec**에 대한 인수를 서식화하고 반환합니다.  
  
 예를 들어 오라클이 Microsoft 오픈 데이터 서비스에서 Rdb에 대한 게이트웨이를 기반으로 하고 Rdb이 EMPLOYEE 테이블을 찾을 수 없는 경우 게이트웨이는 다음 진단 메시지를 생성할 수 있습니다.  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 데이터 원본에서 오류가 발생했기 때문에 게이트웨이는 데이터 원본 식별자([Rdb])에 대한 접두사를 진단 메시지에 추가했습니다. 게이트웨이는 데이터 원본과 인터페이스한 구성 요소이기 때문에 공급업체(DEC]) 및 식별자([ODS 게이트웨이])에 대한 접두사를 진단 메시지에 추가했습니다. 또한 진단 메시지의 시작 부분에 SQLSTATE 값과 Rdb 오류 코드를 추가했습니다. 이렇게 하면 자체 메시지 구조의 의미 체계를 보존하고 ODBC 진단 정보를 드라이버에 계속 제공할 수 있습니다. 드라이버는 게이트웨이에서 오류 문에 연결된 오류 정보를 구문 분석합니다.  
  
 게이트웨이 드라이버는 드라이버 관리자와 인터페이스하는 구성 요소이므로 이전 진단 메시지를 사용하여 **SQLGetDiagRec에서**다음 값을 서식 을 지정하고 반환합니다.  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
