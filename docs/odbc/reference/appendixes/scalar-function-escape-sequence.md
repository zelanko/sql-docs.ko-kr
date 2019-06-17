---
title: 스칼라 함수 이스케이프 시퀀스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0913458d683d7641145b262552e147033dbfc054
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63032845"
---
# <a name="scalar-function-escape-sequence"></a>스칼라 함수 이스케이프 시퀀스
ODBC 스칼라 함수에 대 한 이스케이프 시퀀스를 사용합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>Remarks  
 BNF 표기법의 구문은 다음과 같습니다.  
  
 *ODBC-scalar-function-escape* ::=  
  
 *ODBC esc 시작자* fn *스칼라 함수 ODBC esc 종결자*  
  
 *스칼라 함수* :: = *함수 이름* (*인수 목록*)  
  
 (비 단말은에 대 한 정의 *함수 이름* 및 *함수 이름* (*인수 목록*)의 스칼라 함수 목록에서 파생 된 [ 부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *ODBC-esc-initiator* ::= {  
  
 *ODBC esc 종결자* :: =}  
  
 드라이버는 ODBC 프로시저 호출 구문 지원를 데이터 소스는 프로시저를 지원 하는지 여부를 확인 하려면 응용 프로그램이 호출할 수 있습니다 **SQLGetInfo**합니다. 자세한 내용은 참조 하세요. [부록 e: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)합니다.
