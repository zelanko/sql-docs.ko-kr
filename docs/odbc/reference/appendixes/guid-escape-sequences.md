---
title: "GUID 이스케이프 시퀀스 | Microsoft Docs"
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
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 46f759064bd986fe05aaa30ef6d13b198a84dcec
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="guid-escape-sequences"></a>GUID 이스케이프 시퀀스
ODBC는 GUID 리터럴에 대 한 이스케이프 시퀀스를 사용 합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>주의  
 BNF 표기법의 구문은 다음과 같습니다.  
  
 *ODBC guid 이스케이프* :: =  
     *ODBC esc 시작자 guid* '*guid 값*' *ODBC esc 종결자*  
  
 *ODBC esc 시작자* :: = {  
  
 *ODBC esc 종결자* :: =}  
  
 *guid 값* :: = *클록-낮은 값 guid 구분 기호 클록-중간-값 guid 구분 기호 중요 클록 guid 구분 기호 클록-seq 값 guid 구분 노드 값*  
  
 *guid 구분* :: =-  
  
 *클록 낮은 가치* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *클록-중간-값* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *중요 클록* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *클록-seq 값* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *클록-노드 값* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *hex_digit* :: 0 &#124; 1 &#124; = 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; &#124; &#124; &#124; D &#124; E &#124; F  
  
 GUID 리터럴 이스케이프 시퀀스는 GUID 데이터 형식의 데이터 원본에 의해 지원 되 면 지원 합니다. 응용 프로그램 호출 해야 **SQLGetTypeInfo** 에이 데이터 형식은 지원 되는지 확인 합니다.
