---
title: 외부 조인 이스케이프 시퀀스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af6a98b3e1a7848fa242dfceb890c472e1d16f74
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="outer-join-escape-sequence"></a>외부 조인 이스케이프 시퀀스
ODBC는 외부 조인에 대 한 이스케이프 시퀀스를 사용 합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>주의  
 BNF 표기법의 구문은 다음과 같습니다.  
  
 *ODBC 외부-조인-이스케이프* :: =  
  
 *ODBC esc 시작자* oj *외부 조인 ODBC esc 종결자*  
  
 *외부 조인* :: = *테이블 이름* [*상관 관계 이름*] {왼쪽 &#124; 오른쪽 &#124; 전체}  
  
 외부 조인 {*테이블 이름* [*상관 관계 이름*] &#124; *외부 조인*} ON  
  
 *검색-*  
  
 *조건*  
  
 *상관 관계 이름* :: = *사용자 정의 이름*  
  
 *ODBC esc 시작자* :: = {  
  
 *ODBC esc 종결자* :: =}  
  
 이 문의 부분 사용할 수를 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_OJ_CAPABILITIES 정보 유형을 사용 합니다. 외부 조인에 대 한 *검색 조건* 간에 지정 된 조인 조건에만 있어야 합니다. *테이블 이름*합니다.
