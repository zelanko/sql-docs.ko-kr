---
title: SET EXACT 명령 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 686ecc89f44bac4b219b760e55160f451a15c503
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997730"
---
# <a name="set-exact-command"></a>SET EXACT 명령
서로 다른 길이의 두 문자열을 비교 하는 것에 대 한 규칙을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 ON  
 식은 동등한 것으로 문자에 대 한 문자 일치 하도록 지정 합니다. 비교 식의 후행 공백이 무시 됩니다. 비교에 대 한 긴 식의 길이 맞게 공백 오른쪽의 두 식 중 더 짧은 채워지고 채워집니다.  
  
 OFF  
 (기본값) 해당 일에 식 일치 해야 한다는 문자에 대 한 문자 오른쪽에 있는 식의 끝에 도달할 때까지 지정 합니다.  
  
## <a name="remarks"></a>설명  
 두 문자열 길이가 같은 경우에 설정을 정확 하 게 설정 효과가 없습니다.  
  
## <a name="string-comparisons"></a>문자열 비교  
 Visual FoxPro 같은지 테스트 하는 두 관계형 연산자를 포함 합니다.  
  
 = 연산자 같은 형식의 두 값 간의 비교를 수행 합니다. 이 연산자는 문자, 숫자, 날짜 및 논리 데이터를 비교 하는 데 적합 합니다.  
  
 그러나 사용 하 여 문자 식을 비교할 때의 = 연산자를 예상 대로 결과가 정확 하 게 되지 않을 수 있습니다. 문자 식 비교는 왼쪽에서 오른쪽 식 중 하나를 오른쪽에 있는 식의 끝까지 다른과 같지 않습니다 때까지 문자에 대 한 문자는 = 연산자 (SET 정확한 OFF)에 도달할 때 두 식의 종료 될 때까지 또는 (정확한 설정 켜기)에 도달 했습니다.  
  
 = = 연산자 문자 데이터의 정확한 비교를 필요할 때 사용할 수 있습니다. 두 문자 식으로 비교 하는 경우는 = = 연산자의 양쪽에 있는 식의 = = 연산자에는 정확히 같은 문자를 같은 공백을 포함 하 여 포함 해야 합니다. 사용 하 여 문자열을 비교 하면 정확한 설정 설정이 무시 됩니다 = =.  
  
 다음 표에서 연산자의 선택 및 설정을 정확 하 게 설정 비교에 영향을 보여 줍니다. (밑줄 빈 공간을 나타냅니다.)  
  
|비교|= OFF 정확 합니다.|= 정확한 ON|= = 정확한 ON or OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|일치|일치|일치|  
|"ab" = "abc"|일치 하는 항목이 없습니다|일치 하는 항목이 없습니다|일치 하는 항목이 없습니다|  
|"abc" = "ab"|일치|일치 하는 항목이 없습니다|일치 하는 항목이 없습니다|  
|"abc" = "ab_"|일치 하는 항목이 없습니다|일치 하는 항목이 없습니다|일치 하는 항목이 없습니다|  
|"ab" = "ab_"|일치 하는 항목이 없습니다|일치|일치 하는 항목이 없습니다|  
|"ab_" = "ab"|일치|일치|일치 하는 항목이 없습니다|  
|"" = "ab"|일치 하는 항목이 없습니다|일치 하는 항목이 없습니다|일치 하는 항목이 없습니다|  
|"ab" = ""|일치|일치 하는 항목이 없습니다|일치 하는 항목이 없습니다|  
|"__" = ""|일치|일치|일치 하는 항목이 없습니다|  
|"" = "___"|일치 하는 항목이 없습니다|일치|일치 하는 항목이 없습니다|  
|TRIM("___") = ""|일치|일치|일치|  
|"" = TRIM("___")|일치|일치|일치|  
  
## <a name="see-also"></a>관련 항목  
 [SET ANSI 명령](../../odbc/microsoft/set-ansi-command.md)
