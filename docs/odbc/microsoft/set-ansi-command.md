---
title: ANSI 명령 설정 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300913"
---
# <a name="set-ansi-command"></a>SET ANSI 명령
Visual FoxPro SQL 명령의 = 연산자를 사용 하 여 길이가 다른 문자열을 비교 하는 방법을 결정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 켜기  
 (드라이버의 기본값입니다. Visual FoxPro의 기본값은 OFF입니다.) 더 긴 문자열의 길이와 동일 하 게 만드는 데 필요한 공백을 사용 하 여 짧은 문자열을 채웁니다. 그러면 두 문자열은 전체 길이에 대 한 문자의 문자를 비교 합니다. 다음 비교를 참조 하세요.  
  
```  
'Tommy' = 'Tom'  
```  
  
 결과는 False입니다 (. F.)로 설정 된 경우에는가 채워질 때 ' Tom '이 ' e s '가 되 고 ' Tom ' 및 ' Tommy ' 문자열이 문자에 대 한 문자와 일치 하지 않기 때문에 SET ANSI가 on입니다.  
  
 = = 연산자는이 메서드를 사용 하 여 Visual FoxPro SQL 명령에서 비교 합니다.  
  
 OFF  
 짧은 문자열이 공백으로 채워지지 않도록 지정 합니다. 두 문자열은 짧은 문자열의 끝에 도달할 때까지 문자에 대 한 문자를 비교 합니다. 다음 비교를 참조 하세요.  
  
```  
'Tommy' = 'Tom'  
```  
  
 결과는 True입니다. T.)로 설정 하면 ' Tom ' 후 비교가 중지 되기 때문에 ANSI가 off로 설정 됩니다.  
  
## <a name="remarks"></a>설명  
 SET ANSI는 SQL 문자열 비교가 수행 될 때 두 문자열 중 짧은 것이 공백을 사용 하 여 채워져 있는지 여부를 확인 합니다. SET ANSI는 = = 연산자에 영향을 주지 않습니다. = = 연산자를 사용 하는 경우에는 비교를 위해 짧은 문자열이 항상 공백으로 채워집니다.  
  
## <a name="string-order"></a>문자열 순서  
 SQL 명령에서 비교 시 두 문자열의 왼쪽에서 오른쪽으로의 순서는 = 또는 = = 연산자의 한 쪽에서 다른 쪽으로의 문자열 irrelevantswitching 비교 결과에 영향을 주지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SELECT-SQL 명령](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT 명령](../../odbc/microsoft/set-exact-command.md)
