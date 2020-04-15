---
title: 인터벌 리터럴 구문 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], interval
- interval literals [ODBC]
- ODBC literals [ODBC], interval
ms.assetid: 2f2d22c1-51d6-4055-9f5a-53bc31e9fea0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3387b07a8e769206a6a495addff4287000691fec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290573"
---
# <a name="interval-literal-syntax"></a>간격 리터럴 구문
다음 구문은 ODBC의 간격 리터럴에 사용됩니다.  
  
 *간격 리터럴 ::= INTERVAL* [+*&#124;-] * *간격 문자열 간격 한정자*  
  
 *간격 문자열* ::= *견적* { *연도 리터럴* &#124; *일시간 리터럴* } *견적*  
  
 *연도별 리터럴* ::= *년 가치* &#124;*[연도 값* -] 월 *값*  
  
 *일 시간 리터럴* ::= *일 시간 간격* &#124; 시간 *간격*  
  
 *일 간격* ::= *일 값* *[시간 값* [: 분*값*[:*초 값]]*  
  
 *시간 간격* ::= *시간 값* [:*분 값* [:*초 값]*  
  
 &#124; *분 값* [: 초*값]*  
  
 &#124; *초 값*  
  
 *연도 값* ::= *날짜 시간 값*  
  
 *월 값* ::= *날짜 시간 값*  
  
 *일 값* ::= *날짜 시간 값*  
  
 *시간 값* ::= *날짜 시간 값*  
  
 *분 값* ::= *날짜 시간 값*  
  
 *초 값* ::= *초 정수 값* [.] *초 분수*] ]  
  
 *초-정수 값* ::= *서명되지 않은 정수*  
  
 *초 분수* ::= *서명되지 않은 정수*  
  
 *날짜 시간 값* ::= *서명되지 않은 정수*  
  
 *간격 한정자* ::= *시작 필드* TO *끝 필드* &#124; 단일 날짜 *시간 필드*  
  
 *시작 필드* ::= *비두번째 날짜 타임 필드* [(간격 선행 필드*정밀도)]*  
  
 *끝 필드* ::= *비두번째 날짜 타임 필드* &#124; SECOND[(간격-분수*초-정밀도)]*  
  
 *단일 날짜 시간 필드* ::= *비두번째 날짜 타임 필드* [(간격-선행 필드*정밀도)]*&#124; SECOND[(간격*선행 필드 정밀도](간격-선행 필드 정밀도* [,*간격-분수 초-정밀도)]*  
  
 *날짜 시간 필드* ::= *두 번째 가 아닌 날짜 시간 필드* &#124; 두 번째  
  
 *비 두 번째 날짜 시간 필드* ::= 연도 &#124; 달 &#124; 일 &#124; &#124; 분  
  
 *간격-분수 초-정밀도* ::= *서명되지 않은 정수*  
  
 *간격 선도 필드 정밀도* ::= *서명되지 않은 정수*  
  
 *인용문* ::= '  
  
 *서명되지 않은 정수* ::= *숫자...*
