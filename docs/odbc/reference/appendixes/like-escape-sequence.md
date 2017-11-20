---
title: "이스케이프 시퀀스와 같은 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 678f2f8f720823ef5658ba7ee1e1391bbebc1c50
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="like-escape-sequence"></a>이스케이프 시퀀스와 같은
ODBC는 LIKE 절에 대 한 이스케이프 시퀀스를 사용 합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>주의  
 BNF 표기법의 구문은 다음과 같습니다.  
  
 *ODBC like 이스케이프* :: =  
  
 *ODBC esc 시작자* 이스케이프 '*이스케이프 문자*' *ODBC esc 종결자*  
  
 *이스케이프 문자* :: = *문자*  
  
 *ODBC esc 시작자* :: = {  
  
 *ODBC esc 종결자* :: =}  
  
 드라이버는 LIKE 이스케이프를 지원 하는지 확인 하는 응용 프로그램에서 호출할 수 시퀀스 **SQLGetInfo** SQL_LIKE_ESCAPE_CLAUSE 정보 형식과 합니다.

