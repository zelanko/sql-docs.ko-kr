---
title: 외부 조인 이스케이프 시퀀스 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37ce446328d263f492cdfd369f6e8f9f64fe6dfc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303614"
---
# <a name="outer-join-escape-sequence"></a>외부 조인 이스케이프 시퀀스
ODBC는 외부 조인에 이스케이프 시퀀스를 사용합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>설명  
 BNF 표기법에서 구문은 다음과 같습니다.  
  
 *ODBC 외부 조인-이스케이프::=*  
  
 *ODBC-esc-이니시에이터* oj *외부 조인 ODBC-esc-종단*  
  
 *외부 조인* ::= *테이블 이름* [*상관 관계 이름*] {왼쪽 &#124; 오른쪽 &#124; FULL}  
  
 외부 JOIN{*테이블 이름* *[상관 관계 이름]*&#124; *외부 조인*} ON  
  
 *검색-*  
  
 *조건*  
  
 *상관 관계 이름* ::= *사용자 정의 이름*  
  
 *ODBC-esc-이니시에이터* ::= {  
  
 *ODBC-esc-종결자* ::= }  
  
 이 명령문의 어떤 부분이 지원되는지 확인하려면 응용 프로그램에서 SQL_OJ_CAPABILITIES 정보 형식을 사용하여 **SQLGetInfo를** 호출합니다. 외부 조인의 경우 *search-조건은* 지정된 *테이블 이름*사이의 조인 조건만 포함해야 합니다.
