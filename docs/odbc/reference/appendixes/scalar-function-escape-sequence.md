---
title: "스칼라 함수 이스케이프 시퀀스 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ca49a0f372ef192336318fc2af3135adf4c37d1e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="scalar-function-escape-sequence"></a>스칼라 함수 이스케이프 시퀀스
ODBC 스칼라 함수에 대 한 이스케이프 시퀀스를 사용 합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>주의  
 BNF 표기법의 구문은 다음과 같습니다.  
  
 *ODBC 스칼라-함수 이스케이프* :: =  
  
 *ODBC esc 시작자* fn *스칼라 함수 ODBC esc 종결자*  
  
 *스칼라 함수* :: = *함수 이름* (*인수 목록*)  
  
 (비 단말에 대 한 정의 *함수 이름* 및 *함수 이름* (*인수 목록*) 스칼라 함수에서의 목록에서 파생 [ 부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *ODBC esc 시작자* :: = {  
  
 *ODBC esc 종결자* :: =}  
  
 드라이버는 ODBC 프로시저 호출 구문 지원를 데이터 소스는 프로시저를 지원 하는지 여부를 확인 하려면 응용 프로그램이 호출할 수 **SQLGetInfo**합니다. 자세한 내용은 참조 [부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)합니다.
