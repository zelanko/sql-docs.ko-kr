---
title: 스칼라 기능 이스케이프 시퀀스 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8347b8e6f0fab6dffc5295fb3b8260a6a56ed123
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305076"
---
# <a name="scalar-function-escape-sequence"></a>스칼라 함수 이스케이프 시퀀스
ODBC는 스칼라 함수에 이스케이프 시퀀스를 사용합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>설명  
 BNF 표기법에서 구문은 다음과 같습니다.  
  
 *ODBC-스칼라 함수-이스케이프::=*  
  
 *ODBC-esc-이니시에이터* fn *스칼라 기능 ODBC-esc-터미네이터*  
  
 *스칼라 함수* ::= *함수 이름* *(인수 목록)*  
  
 (비 터미널 *함수 이름* 및 함수 *이름* *(인수 목록)에*대 한 정의 [부록 E: 스칼라 함수의](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)스칼라 함수 목록에서 파생 됩니다.)  
  
 *ODBC-esc-이니시에이터* ::= {  
  
 *ODBC-esc-종결자* ::= }  
  
 데이터 원본이 프로시저를 지원하고 드라이버가 ODBC 프로시저 호출 구문을 지원하는지 여부를 확인하려면 응용 프로그램이 **SQLGetInfo**를 호출할 수 있습니다. 자세한 내용은 [부록 E: 스칼라 함수 를](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)참조하십시오.
