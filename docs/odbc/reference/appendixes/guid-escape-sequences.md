---
title: GUID 이스케이프 시퀀스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf41671abc6393a18fad06e1debd297fed1f04c5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654985"
---
# <a name="guid-escape-sequences"></a>GUID 이스케이프 시퀀스
ODBC는 GUID 리터럴의 이스케이프 시퀀스를 사용합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>Remarks  
 BNF 표기법의 구문은 다음과 같습니다.  
  
 *ODBC guid 이스케이프* :: =  
     *ODBC esc 시작자 guid* '*guid 값*' *ODBC esc 종결자*  
  
 *ODBC esc 시작자* :: = {  
  
 *ODBC esc 종결자* :: =}  
  
 *guid 값* :: = *클록-낮은 값 guid 구분 기호 값-중간-클록 guid 구분 기호 클록 높은 가치의 guid 구분 기호 클록-seq 값 guid 구분 기호 노드 값*  
  
 *guid 구분 기호* :: =-  
  
 *클록 낮은 가치의* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *시계-중간 값* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *클록 높은 가치의* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *시계-seq 값* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *시계-노드-값* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *hex_digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; 는 &#124; B &#124; C &#124; D &#124; 전자 &#124; F  
  
 GUID 리터럴 이스케이프 시퀀스는 GUID 데이터 형식의 데이터 원본에서 지원 되는 경우 사용할 수 있습니다. 응용 프로그램에서 호출 해야 **SQLGetTypeInfo** 이 데이터 형식은 지원 되는지 여부를 확인 하려면.
