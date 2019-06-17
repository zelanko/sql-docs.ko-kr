---
title: LIKE 이스케이프 시퀀스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65447904f32b7e0457ed807f18e942b334ddc236
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188797"
---
# <a name="like-escape-sequence"></a>LIKE 이스케이프 시퀀스
ODBC는 LIKE 절에 대 한 이스케이프 시퀀스를 사용합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Remarks  
 BNF 표기법의 구문은 다음과 같습니다.  
  
 *ODBC-like-escape* ::=  
  
 *ODBC esc 시작자* 이스케이프 '*이스케이프 문자*' *ODBC esc 종결자*  
  
 *escape-character* ::= *character*  
  
 *ODBC-esc-initiator* ::= {  
  
 *ODBC esc 종결자* :: =}  
  
 드라이버는 LIKE 이스케이프를 지원 하는지 확인할 응용 프로그램에서 호출할 수 시퀀스 **SQLGetInfo** SQL_LIKE_ESCAPE_CLAUSE 정보 형식을 사용 하 여 합니다.
