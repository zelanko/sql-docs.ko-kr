---
title: 게이트웨이 진단 예제 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f4e17074616111ee93ce87c04036d1fc3fd48dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63062421"
---
# <a name="gateways-diagnostic-example"></a>게이트웨이 진단 예제
게이트웨이 아키텍처를 드라이버는 ODBC를 지 원하는 게이트웨이에 요청을 보냅니다. 게이트웨이 DBMS에 요청을 보냅니다. 드라이버 형식 및에 대 한 인수를 반환 합니다. 드라이버 관리자와 인터페이스 하는 구성 요소 이므로 **SQLGetDiagRec**합니다.  
  
 예를 들어, Oracle Rdb 게이트웨이 Microsoft 개방형 Data Services 및 Rdb 직원 테이블을 찾을 수 없습니다 경우에 따라 게이트웨이 진단이 메시지를 생성할 수 있습니다.  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 데이터 소스의 오류 때문 게이트웨이 진단 메시지에 데이터 원본 식별자 ([Rdb])에 대 한 접두사를 추가 합니다. 게이트웨이가 데이터 원본과 되는 구성 요소를 때문에 진단 메시지를 해당 공급 업체 ([DEC]) 및 식별자 ([ODS 게이트웨이])에 대 한 접두사를 추가 합니다. 또한 진단 메시지의 시작 부분에 SQLSTATE 값 및 Rdb 오류 코드를 추가 합니다. 이 메시지 구조 자체의 의미 체계를 유지 하 고 여전히 드라이버는 ODBC 진단 정보를 제공 하도록 허용 합니다. 드라이버 오류 문이 게이트웨이에서 연결 오류 정보를 구문 분석 합니다.  
  
 위의 진단 메시지 서식을 지정 하 고 다음 값이 반환 사용 됩니다 게이트웨이 드라이버를 드라이버 관리자와 인터페이스 하는 구성 요소 이므로 **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
