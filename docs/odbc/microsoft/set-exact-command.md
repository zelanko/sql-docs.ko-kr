---
title: 정확한 명령 설정 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e754fff35b6b948ac63d19361067b2d65a07fdd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300873"
---
# <a name="set-exact-command"></a>SET EXACT 명령
서로 다른 길이의 두 문자열을 비교하기 위한 규칙을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 켜기  
 표현식이 문자와 일치해야 문자가 같도록 지정합니다. 비교를 위해 식의 후행 공백은 무시됩니다. 비교를 위해 두 식의 짧은 것은 더 긴 표현식의 길이와 일치하도록 공백으로 오른쪽에 패딩됩니다.  
  
 OFF  
 (기본값)을 사용합니다. 동등한 표현식은 오른쪽의 식끝에 도달할 때까지 문자와 일치해야 함을 지정합니다.  
  
## <a name="remarks"></a>설명  
 두 문자열의 길이가 같은 경우 정확한 SET 설정은 영향을 주지 않습니다.  
  
## <a name="string-comparisons"></a>문자열 비교  
 Visual FoxPro에는 같음을 테스트하는 두 개의 관계형 연산자가 있습니다.  
  
 = 연산자는 동일한 형식의 두 값 간의 비교를 수행합니다. 이 연산자는 문자, 숫자, 날짜 및 논리 데이터를 비교하는 데 적합합니다.  
  
 그러나 문자 식을 = 연산자와 비교할 때 결과가 예상과 다를 수 있습니다. 문자 표현식은 왼쪽에서 오른쪽으로 문자문자를 비교하며, 식 중 하나가 다른 표현식과 같지 않을 때까지, = 연산자의 오른쪽에 있는 식의 끝에 도달(SET EXACT OFF)될 때까지 또는 두 식의 끝에 도달할 때까지(정확한 ON SET)가 됩니다.  
  
 == 연산자는 문자 데이터를 정확하게 비교해야 하는 경우에 사용할 수 있습니다. 두 문자 식을 == 연산자와 비교하는 경우 == 연산자의 양쪽에 있는 표현식은 공백을 포함하여 정확히 동일한 문자를 포함해야 동일하다고 간주됩니다. ==를 사용하여 문자 문자열을 비교할 때 정확한 설정 설정은 무시됩니다.  
  
 다음 표에서는 연산자와 SET EXACT 설정의 선택이 비교에 미치는 영향을 보여 주며, (밑줄은 빈 공간을 나타냅니다.)  
  
|비교|= 정확한 꺼져|= 정확한 에|== 정확한 켜기 또는 끄기|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|일치|일치|일치|  
|"ab" = "abc"|일치 없음|일치 없음|일치 없음|  
|"abc" = "ab"|일치|일치 없음|일치 없음|  
|"abc" = "ab_"|일치 없음|일치 없음|일치 없음|  
|"ab" = "ab_"|일치 없음|일치|일치 없음|  
|"ab_" = "ab"|일치|일치|일치 없음|  
|"" = "ab"|일치 없음|일치 없음|일치 없음|  
|"ab" = ""|일치|일치 없음|일치 없음|  
|"__" = ""|일치|일치|일치 없음|  
|"" = "___"|일치 없음|일치|일치 없음|  
|트림("___") = ""|일치|일치|일치|  
|"" = 트림("___")|일치|일치|일치|  
  
## <a name="see-also"></a>참고 항목  
 [SET ANSI 명령](../../odbc/microsoft/set-ansi-command.md)
