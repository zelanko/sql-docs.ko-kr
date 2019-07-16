---
title: 숫자 리터럴 구문 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC literals [ODBC], numeric
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: fb17498d-4f1d-4b3d-b33d-1e62c7d3c32d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9daa81e2e0c2e927ee7407d4a00d5d48c333bd54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990721"
---
# <a name="numeric-literal-syntax"></a>숫자 리터럴 구문
ODBC의 숫자 리터럴에 대 한 구문을 사용 됩니다.  
  
 *숫자 리터럴을* :: = *서명-숫자-리터럴 &#124; 부호 없는 숫자-리터럴*  
  
 *signed-numeric-literal* ::= [*sign*] *unsigned-numeric-literal*  
  
 *부호 없는 숫자-리터럴* :: = *정확한 숫자-리터럴 &#124; 대략적인 숫자-리터럴*  
  
 *정확한 숫자-리터럴* :: = *부호 없는 정수* [*기간*[*부호 없는 정수*]]  *&#124;기간 부호 없는 정수*  
  
 *sign* :: = *더하기 &#124; 빼기 기호*  
  
 *대략적인 숫자-리터럴* :: = *E가 지 수*  
  
 *가 수* :: = *정확한 숫자-리터럴*  
  
 *exponent* ::= *signed-integer*  
  
 *signed-integer* ::= [*sign*] *unsigned-integer*  
  
 *unsigned-integer* ::= *digit...*  
  
 *plus-sign* ::= *+*  
  
 *minus-sign* ::= -  
  
 *digit* ::= 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *기간* :: =.
