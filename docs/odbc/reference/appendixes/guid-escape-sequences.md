---
title: GUID 이스케이프 시퀀스 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44907bfbd884bf361ce5f2ab8b3f6d8a247aba44
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306974"
---
# <a name="guid-escape-sequences"></a>GUID 이스케이프 시퀀스
ODBC는 GUID 리터럴에 이스케이프 시퀀스를 사용합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>설명  
 BNF 표기법에서 구문은 다음과 같습니다.  
  
 *ODBC-guid-이스케이프* ::=  
     *ODBC-esc-이니시에이터 GUID* '*guid-값*' *ODBC-esc-종결자*  
  
 *ODBC-esc-이니시에이터* ::= {  
  
 *ODBC-esc-종결자* ::= }  
  
 *guid-값* ::= *클럭 저값 guid-value 시계-중간 값 guid-value 시계-높은 값 guid-구분기 클럭-seq-값 guid-구분 기호-값*  
  
 *guid 구분 기호* ::= -  
  
 *클럭 저값* ::= hex_digit hex_digit *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit* hex_digit.  
  
 *시계 중간 값* ::= *hex_digit hex_digit hex_digit hex_digit*  
  
 *클럭 고값* ::= hex_digit hex_digit hex_digit *hex_digit hex_digit hex_digit hex_digit*  
  
 *클럭-seq 값* ::= *hex_digit hex_digit hex_digit hex_digit*  
  
 *클럭 노드 값* ::hex_digit *hex_digit=* hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit.  
  
 *hex_digit* ::= 0 &#124; &#124; 0 &#124; 2 &#124; &#124; 3 &#124; 4 &#124; &#124; 6 &#124; &#124; 6 &#124; 8 &#124; 9 &#124; &#124; B &#124; C &#124; &#124; D &#124; &#124; E &#124; F를 &#124;.  
  
 GUID 데이터 형식이 데이터 원본에서 지원되는 경우 GUID 리터럴 이스케이프 시퀀스가 지원됩니다. 응용 프로그램은 **SQLGetTypeInfo를** 호출하여 이 데이터 형식이 지원되는지 확인해야 합니다.
