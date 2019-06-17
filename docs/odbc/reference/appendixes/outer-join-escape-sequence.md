---
title: 외부 조인 이스케이프 시퀀스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba08d33efca6fa90531f89bd57a307f42f343ebd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63018362"
---
# <a name="outer-join-escape-sequence"></a>외부 조인 이스케이프 시퀀스
ODBC는 외부 조인 이스케이프 시퀀스를 사용합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Remarks  
 BNF 표기법의 구문은 다음과 같습니다.  
  
 *ODBC 외부-조인-이스케이프* :: =  
  
 *ODBC esc 시작자* oj *외부 조인 ODBC esc 종결자*  
  
 *외부 조인* :: = *테이블 이름* [*상관 관계 이름*] {왼쪽 &#124; 오른쪽 &#124; 전체}  
  
 외부 조인 {*테이블 이름* [*상관 관계 이름*] &#124; *외부 조인*} ON  
  
 *search-*  
  
 *condition*  
  
 *correlation-name* ::= *user-defined-name*  
  
 *ODBC-esc-initiator* ::= {  
  
 *ODBC esc 종결자* :: =}  
  
 이 문은 부분 지를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** SQL_OJ_CAPABILITIES 정보 형식을 사용 하 여 합니다. 외부 조인을 *검색 조건을* 간에 지정 된 조인 조건에만 있어야 합니다. *테이블 이름*합니다.
