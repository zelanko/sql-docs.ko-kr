---
title: ANSI 명령 설정 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97269642b4147b966fdd71003f5f81ebe7905282
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300913"
---
# <a name="set-ansi-command"></a>SET ANSI 명령
Visual FoxPro SQL 명령에서 = 연산자로 서로 다른 길이의 문자열 간의 비교가 어떻게 이루어지는지 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 켜기  
 (드라이버에 대 한 기본값; Visual FoxPro에 대 한 기본값은 꺼져 있습니다.) 더 긴 문자열의 길이와 동일하게 만드는 데 필요한 공백으로 짧은 문자열을 패드합니다. 그런 다음 두 문자열은 전체 길이에 대한 문자의 문자를 비교합니다. 이 비교를 고려하십시오.  
  
```  
'Tommy' = 'Tom'  
```  
  
 결과는 False(. F.) SET ANSI가 켜지면 패딩을 할 때 '톰'이 '톰'이 되고 문자열 '톰'과 '토미'가 캐릭터의 캐릭터와 일치하지 않기 때문입니다.  
  
 == 연산자는 Visual FoxPro SQL 명령에서 비교를 위해 이 메서드를 사용합니다.  
  
 OFF  
 짧은 문자열이 공백으로 패딩되지 않도록 지정합니다. 두 문자열은 짧은 문자열의 끝에 도달할 때까지 문자에 대 한 문자를 비교 합니다. 이 비교를 고려하십시오.  
  
```  
'Tommy' = 'Tom'  
```  
  
 결과는 True(. T.) 설정 ANSI가 꺼져있을 때, 비교는 '톰'후 중지하기 때문에.  
  
## <a name="remarks"></a>설명  
 SET ANSI는 SQL 문자열 비교가 이루어질 때 두 문자열의 짧은 두 개의 문자열이 공백으로 패딩되는지 여부를 결정합니다. SET ANSI는 == 연산자에 영향을 주지 않습니다. == 연산을 사용할 때 더 짧은 문자열은 항상 비교를 위해 공백으로 패딩됩니다.  
  
## <a name="string-order"></a>문자열 순서  
 SQL 명령에서 비교에서 두 문자열의 왼쪽에서 오른쪽 순서는 = 또는 == 연산자의 한쪽에서 다른 쪽으로 문자열을 전환하는 것은 비교 결과에 영향을 주지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [선택 - SQL 명령](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT 명령](../../odbc/microsoft/set-exact-command.md)
