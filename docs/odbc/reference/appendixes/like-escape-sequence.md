---
title: LIKE 이스케이프 시퀀스 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 517c21f7b64fa7ceb662af9839a9fed1a1e6eff6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304924"
---
# <a name="like-escape-sequence"></a>LIKE 이스케이프 시퀀스
ODBC는 LIKE 절에 대한 이스케이프 시퀀스를 사용합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>설명  
 BNF 표기법에서 구문은 다음과 같습니다.  
  
 *ODBC와 같은 이스케이프* ::=  
  
 *ODBC-esc-이니시에이터* 탈출 '*이스케이프 문자*' *ODBC-esc-종기*  
  
 *이스케이프 문자* ::= *문자*  
  
 *ODBC-esc-이니시에이터* ::= {  
  
 *ODBC-esc-종결자* ::= }  
  
 드라이버가 LIKE 이스케이프 시퀀스를 지원하는지 확인하려면 응용 프로그램에서 SQL_LIKE_ESCAPE_CLAUSE 정보 형식을 사용하여 **SQLGetInfo를** 호출할 수 있습니다.
