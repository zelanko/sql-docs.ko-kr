---
title: SET ANSI 명령 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5af98bd8f16d7278b932ad89f1c81c58ddb1fb54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127861"
---
# <a name="set-ansi-command"></a>SET ANSI 명령
길이가 다른 문자열을 비교 하는 방법을 사용 하 여 결정 됩니다는 = Visual FoxPro SQL 명령에는 연산자입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 ON  
 (드라이버에 대 한 기본; Visual FoxPro에 대 한 기본값은 OFF입니다.) 패드에 있는 공백 사용 하 여 더 짧은 문자열이 하는 데 필요한 있도록 길수록 같음 문자열의 길이입니다. 두 문자열를 해당 전체 길이 대 한 문자에 대 한 문자를 비교 합니다. 이 비교를 것이 좋습니다.  
  
```  
'Tommy' = 'Tom'  
```  
  
 결과 False (합니다. 6.) ANSI 설정 이므로 경우에 채워질 때 'Tom'가 'Tom' 및 'Tom' 및 'Tommy' 문자열 문자에 대 한 문자 일치 하지 않습니다.  
  
 연산자는이 메서드를 비교 Visual FoxPro SQL 명령에 = =.  
  
 OFF  
 더 짧은 문자열이 공백으로 채워지지 않습니다 지정 합니다. 두 문자열을 비교 짧은 문자열의 끝에 도달할 때까지 문자에 대 한 문자입니다. 이 비교를 것이 좋습니다.  
  
```  
'Tommy' = 'Tom'  
```  
  
 결과 True (합니다. T.)의 경우 ANSI 설정 꺼져 있으므로 비교를 'Tom' 후 중지 합니다.  
  
## <a name="remarks"></a>Remarks  
 ANSI 설정 여부를 두 문자열 중 짧은 공백으로 SQL 문자열 비교를 수행 하는 경우를 결정 합니다. ANSI 설정에 없는 영향을 주지는 = = 연산자; 사용 하는 경우는 = = 연산자, 더 짧은 문자열에는 항상 비교에 사용할 만큼 공백으로 채워집니다.  
  
## <a name="string-order"></a>문자열 순서  
 SQL 명령에서 왼쪽에서 오른쪽 비교에서 두 문자열의 순서가 irrelevantswitching =의 한 쪽에서 문자열 = = 또는 다른 연산자 비교의 결과 영향을 주지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SELECT-SQL 명령](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT 명령](../../odbc/microsoft/set-exact-command.md)
