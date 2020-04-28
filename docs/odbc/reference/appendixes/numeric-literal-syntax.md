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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e035e3ec53c5b5494c029d6840b9f5c836821209
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299863"
---
# <a name="numeric-literal-syntax"></a>숫자 리터럴 구문
ODBC의 숫자 리터럴에는 다음 구문이 사용 됩니다.  
  
 *숫자-리터럴* :: = *부호 있는 숫자 리터럴 &#124; 부호 없는 숫자* 리터럴  
  
 *부호 있는 숫자-리터럴* :: = [*부호*] *부호 없는 숫자 리터럴*  
  
 *부호 없는 숫자* 리터럴:: = *정확한 숫자 리터럴 &#124; 근사 숫자 리터럴*  
  
 *exact-numeric-literal* :: = *unsigned-integer* [*period*[*unsigned-integer*]] *&#124;period unsigned-integer*  
  
 *sign* :: = *더하기 기호 &#124; 빼기 기호*  
  
 *근사 숫자 리터럴* :: =가 수 *E 지* 수  
  
 가 *중::* = *정확한 숫자 리터럴*  
  
 *지수가* :: = *signed-integer*  
  
 *signed-integer* :: = [*sign*] *unsigned-integer*  
  
 *unsigned-integer* :: = *digit* ...  
  
 *더하기 기호* :: =*+*  
  
 *빼기 기호* :: =-  
  
 *digit* :: = 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 0  
  
 *period* :: =
