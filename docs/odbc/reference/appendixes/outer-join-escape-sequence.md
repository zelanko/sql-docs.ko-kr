---
title: "외부 조인 이스케이프 시퀀스 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d208b7de815f090e5f61d3d807912c53c4253e31
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

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
  
 OUTER JOIN {*테이블 이름* [*상관 관계 이름*] &#124; *외부 조인*} ON  
  
 *검색-*  
  
 *조건*  
  
 *상관 관계 이름* :: = *사용자 정의 이름*  
  
 *ODBC esc 시작자* :: = {  
  
 *ODBC esc 종결자* :: =}  
  
 이 문의 부분 사용할 수를 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_OJ_CAPABILITIES 정보 유형을 사용 합니다. 외부 조인에 대 한 *검색 조건* 간에 지정 된 조인 조건에만 있어야 합니다. *테이블 이름*합니다.

