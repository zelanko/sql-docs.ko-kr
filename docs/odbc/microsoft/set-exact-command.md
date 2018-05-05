---
title: SET 정확한 명령을 | Microsoft Docs
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
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6f5576ec5a1275914ee0558cf3fcd151ee3c3cc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="set-exact-command"></a>SET 정확한 명령
길이가 다른 두 개의 문자열 비교에 대 한 규칙을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 ON  
 식에 문자를 해당 하는 것에 대 한 문자 일치 해야 한다는 것을 지정 합니다. 비교 식의 모든 후행 공백은 무시 됩니다. 비교에 대 한 긴 식의 길이 일치 하도록 빈칸으로 오른쪽에는 두 식 중 짧은 채워지고 채워집니다.  
  
 OFF  
 (기본값)입니다. 동일 하려면 식을 일치 해야 한다는 문자에 대 한 문자 오른쪽 식의 끝에 도달할 때까지 지정 합니다.  
  
## <a name="remarks"></a>주의  
 두 문자열이 동일한 길이 경우에 설정을 정확 하 게 설정 효과가 없습니다.  
  
## <a name="string-comparisons"></a>문자열 비교  
 Visual FoxPro 같은지 테스트 하는 두 명의 관계형 연산자에 있습니다.  
  
 = 연산자 같은 형식의 두 값 간의 비교를 수행 합니다. 이 연산자는 문자, 숫자, 날짜 및 논리 데이터를 비교 하는 데 적합 합니다.  
  
 그러나와 문자 식을 비교할 때의 = 연산자를 예상 대로 결과가 정확 하 게 되지 않을 수 있습니다. 문자 식을 비교 하 여 왼쪽에서 오른쪽 식 중 하나이 아니라면 다른의 오른쪽에 있는 식의 끝까지 될 때까지 문자에 대 한 문자는 = 연산자 (설정 정확한 OFF)에 도달 하면 두 식의 끝이 될 때까지 또는 (정확한 설정 ON)에 도달 했습니다.  
  
 = = 연산자 문자 데이터를 정확 하 게 비교 필요할 때 사용할 수 있습니다. 두 문자 식과 비교 하는 경우는 = = 연산자의 양쪽 모두에 있는 식의 = = 연산자는 정확 하 게 같은 문자를 같은 빈 셀을 포함 하 여 포함 해야 합니다. 사용 하 여 문자열을 비교 하는 정확한 설정 설정이 무시 됩니다 = = 합니다.  
  
 다음 표에서 연산자의 선택 및 설정을 정확 하 게 설정 비교에 영향을 보여 줍니다. (밑줄 빈 공간을 나타냅니다.)  
  
|비교|= 정확 하 게 해제|= 정확한 ON|= = 정확한 ON 또는 OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|일치 하는 항목|일치 하는 항목|일치 하는 항목|  
|"ab" = "abc"|일치 없음|일치 없음|일치 없음|  
|"abc" = "ab"|일치 하는 항목|일치 없음|일치 없음|  
|"abc" = "ab_"|일치 없음|일치 없음|일치 없음|  
|"ab" = "ab_"|일치 없음|일치 하는 항목|일치 없음|  
|"ab_" = "ab"|일치 하는 항목|일치 하는 항목|일치 없음|  
|"" = "ab"|일치 없음|일치 없음|일치 없음|  
|"ab" = ""|일치 하는 항목|일치 없음|일치 없음|  
|"__" = ""|일치 하는 항목|일치 하는 항목|일치 없음|  
|"" = "___"|일치 없음|일치 하는 항목|일치 없음|  
|TRIM("___") = ""|일치 하는 항목|일치 하는 항목|일치 하는 항목|  
|"" TRIM("___") =|일치 하는 항목|일치 하는 항목|일치 하는 항목|  
  
## <a name="see-also"></a>관련 항목:  
 [SET ANSI 명령](../../odbc/microsoft/set-ansi-command.md)
