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
ms.openlocfilehash: 576fe7268ccf71a8c926f6b1124ebbf8a8c711b0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100639"
---
# <a name="outer-join-escape-sequence"></a>외부 조인 이스케이프 시퀀스
ODBC는 외부 조인에 대 한 이스케이프 시퀀스를 사용 합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>설명  
 BNF 표기법에서 구문은 다음과 같습니다.  
  
 *ODBC 외부 조인-이스케이프* :: =  
  
 *Odbc-esc-개시자* oj *외부 조인 odbc-esc-종결자*  
  
 *outer join* :: = *table-name* [*상관 관계-NAME*] {LEFT &#124; RIGHT &#124; FULL}  
  
 외부 조인 {*테이블 이름* [*상관 관계-이름*] &#124; *outer*join} ON  
  
 *조건을*  
  
 *조건*  
  
 *상관 관계-이름* :: = *사용자 정의-이름*  
  
 *ODBC-esc-시작자* :: = {  
  
 *ODBC-esc-종결자* :: =}  
  
 이 문의 어떤 부분이 지원 되는지 확인 하기 위해 응용 프로그램은 SQL_OJ_CAPABILITIES 정보 형식으로 **SQLGetInfo** 를 호출 합니다. 외부 조인의 경우 *검색 조건은* 지정 된 *테이블 이름*사이의 조인 조건만 포함 해야 합니다.
