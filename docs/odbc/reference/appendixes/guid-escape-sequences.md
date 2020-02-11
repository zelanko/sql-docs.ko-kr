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
ms.openlocfilehash: a74ed9d4dfe0afb8bf59abb11220a0677d000bfb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67947590"
---
# <a name="guid-escape-sequences"></a>GUID 이스케이프 시퀀스
ODBC는 GUID 리터럴에 이스케이프 시퀀스를 사용 합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>설명  
 BNF 표기법에서 구문은 다음과 같습니다.  
  
 *ODBC-guid-이스케이프* :: =  
     *ODBC-esc-초기자 guid* '*guid-값*' *ODBC-esc-종결자*  
  
 *ODBC-esc-시작자* :: = {  
  
 *ODBC-esc-종결자* :: =}  
  
 *guid-value* :: = *클록-낮은 값 guid-구분 기호-중간 값 guid-구분 기호-값 guid-구분 기호-시퀀스-값 guid-구분 기호 노드-값*  
  
 *guid-구분 기호* :: =-  
  
 *클록-낮은 값* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *클록-중간 값* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-high value* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-seq-value* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *클록 노드-value* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit* hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit  
  
 *hex_digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; &#124; B &#124; C &#124; D &#124; E &#124; F  
  
 Guid 리터럴 이스케이프 시퀀스는 GUID 데이터 형식이 데이터 원본에서 지원 되는 경우에 지원 됩니다. 응용 프로그램은 **SQLGetTypeInfo** 를 호출 하 여이 데이터 형식이 지원 되는지 여부를 확인 해야 합니다.
