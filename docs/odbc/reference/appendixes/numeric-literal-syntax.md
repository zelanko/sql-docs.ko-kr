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
manager: craigg
ms.openlocfilehash: 18b1c144e84bf0be5aaeb68b66660f7bc7865ade
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181285"
---
# <a name="numeric-literal-syntax"></a>숫자 리터럴 구문
ODBC의 숫자 리터럴에 대 한 구문을 사용 됩니다.  
  
 *숫자 리터럴을* :: = *서명-숫자-리터럴 &#124; 부호 없는 숫자-리터럴*  
  
 *signed-numeric-literal* ::= [*sign*] *unsigned-numeric-literal*  
  
 *부호 없는 숫자-리터럴* :: = *정확한 숫자-리터럴 &#124; 대략적인 숫자-리터럴*  
  
 *exact-numeric-literal* ::= *unsigned-integer* [*period*[*unsigned-integer*]] *&#124;period unsigned-integer*  
  
 *sign* :: = *더하기 &#124; 빼기 기호*  
  
 *대략적인 숫자-리터럴* :: = *E가 지 수*  
  
 *mantissa* ::= *exact-numeric-literal*  
  
 *exponent* ::= *signed-integer*  
  
 *signed-integer* ::= [*sign*] *unsigned-integer*  
  
 *unsigned-integer* ::= *digit...*  
  
 *plus-sign* ::= *+*  
  
 *minus-sign* ::= -  
  
 *digit* ::= 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *period* ::= .
