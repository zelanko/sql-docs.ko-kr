---
title: 게이트웨이 진단 예 | Microsoft Docs
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
ms.openlocfilehash: 50476cb92d477bb9a72ac8d4311d24572b0368e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069679"
---
# <a name="gateways-diagnostic-example"></a>게이트웨이 진단 예제
게이트웨이 아키텍처에서 드라이버는 ODBC를 지 원하는 게이트웨이로 요청을 보냅니다. 게이트웨이에서 DBMS로 요청을 보냅니다. 드라이버 관리자와 상호 작용 하는 구성 요소 이므로 드라이버는 **SQLGetDiagRec**에 대 한 인수를 포맷 하 고 반환 합니다.  
  
 예를 들어 Microsoft Open Data Services에서 Rdb에 대 한 게이트웨이 기반 Oracle을 사용 하는 경우 Rdb에서 테이블을 찾을 수 없는 경우 게이트웨이에서이 진단 메시지를 생성할 수 있습니다.  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 데이터 원본에서 오류가 발생 했으므로 게이트웨이에서 데이터 원본 식별자 ([Rdb])에 대 한 접두사를 진단 메시지에 추가 했습니다. 게이트웨이는 데이터 원본으로 되 하는 구성 요소 이기 때문에 해당 공급 업체 ([DEC]) 및 식별자 ([ODS Gateway])에 대 한 접두사를 진단 메시지에 추가 했습니다. 또한 SQLSTATE 값 및 Rdb 오류 코드를 진단 메시지의 시작 부분에 추가 했습니다. 이를 통해 자체 메시지 구조의 의미 체계를 유지 하 고 드라이버에 ODBC 진단 정보를 제공할 수 있습니다. 드라이버는 게이트웨이에서 오류 문에 연결 된 오류 정보를 구문 분석 합니다.  
  
 게이트웨이 드라이버는 드라이버 관리자와 상호 작용 하는 구성 요소 이므로 앞의 진단 메시지를 사용 하 여 **SQLGetDiagRec**에서 다음 값의 형식을 지정 하 고 반환 합니다.  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
