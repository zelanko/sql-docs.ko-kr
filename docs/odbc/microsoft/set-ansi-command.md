---
title: SET ANSI 명령을 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5946efa397fa6bde8c52ad69925a96f2e33f7dd4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904328"
---
# <a name="set-ansi-command"></a>SET ANSI 명령
길이가 다른 문자열 간의 비교를 적용 하는 방법을 결정은 = Visual FoxPro SQL 명령에는 연산자입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 ON  
 (드라이버에 대 한 기본, Visual FoxPro에 대 한 기본값은 OFF) 패드에 있는 공백 사용 하 여 더 짧은 문자열에 필요한 오래 같음 문자열의 길이가 만듭니다. 두 문자열의 전체 길이 대 한 문자에 대 한 비교 된 문자 수입니다. 이 비교를 고려 합니다.  
  
```  
'Tommy' = 'Tom'  
```  
  
 결과 False (합니다. 6.) 경우 ANSI 설정 되므로,이 패딩 'Tom' 'Tom' 되 고 'Tom' 및 'Tommy' 문자열 문자에 대 한 문자 일치 하지 않습니다.  
  
 Visual FoxPro SQL 명령에서 비교에이 메서드를 사용 하 여 연산자를 = = 합니다.  
  
 OFF  
 더 짧은 문자열이 공백으로 채워지지 않습니다 지정 합니다. 두 개의 문자열 비교 짧은 문자열의 끝에 도달할 때까지 문자에 대 한 문자입니다. 이 비교를 고려 합니다.  
  
```  
'Tommy' = 'Tom'  
```  
  
 결과 True (합니다. 화)의 경우 ANSI 설정 되지 않고, 때문에 비교 'Tom' 후 중지 됩니다.  
  
## <a name="remarks"></a>주의  
 ANSI 설정 여부를 두 문자열 중 짧은 부분이 빈칸으로 SQL 문자열 비교를 수행 하는 경우를 결정 합니다. ANSI 설정에 영향을 주지 않습니다에 = = 연산자; 사용 하는 경우는 = = 연산자, 짧은 문자열에는 항상 비교에 대 한 만큼 공백으로 채워집니다.  
  
## <a name="string-order"></a>문자열 순서  
 SQL 명령에서 왼쪽에서 오른쪽 비교에서 두 문자열의 순서가 irrelevantswitching =의 한 쪽에서 문자열 또는 = = 연산자를 다른 비교 결과 영향을 주지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 명령 선택](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT 명령](../../odbc/microsoft/set-exact-command.md)
