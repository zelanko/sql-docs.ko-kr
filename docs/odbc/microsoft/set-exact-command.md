---
description: SET EXACT 명령
title: 정확한 명령 설정 | Microsoft Docs
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
ms.openlocfilehash: 6bae23ef0677061f92d0466564619e85d4ae1630
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466365"
---
# <a name="set-exact-command"></a>SET EXACT 명령
길이가 다른 두 문자열을 비교 하는 규칙을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>인수  
 켜기  
 식이 문자에 해당 하는 문자를 일치 시켜야 함을 지정 합니다. 식의 후행 공백은 비교 시 무시 됩니다. 비교를 위해 두 식 중 짧은 값은 더 긴 식의 길이와 일치 하는 공백이 있는 오른쪽에 채워집니다.  
  
 OFF  
 (기본값) 오른쪽에 있는 식의 끝에 도달할 때까지 식이 문자에 대 한 문자와 일치 해야 함을 지정 합니다.  
  
## <a name="remarks"></a>설명  
 두 문자열의 길이가 모두 같으면 정확한 설정 설정이 적용 되지 않습니다.  
  
## <a name="string-comparisons"></a>문자열 비교  
 Visual FoxPro에는 같은지 테스트 하는 두 개의 관계형 연산자가 있습니다.  
  
 = 연산자는 동일한 형식의 두 값을 비교 합니다. 이 연산자는 문자, 숫자, 날짜 및 논리적 데이터를 비교 하는 데 적합 합니다.  
  
 그러나 문자 식을 = 연산자와 비교할 때 결과가 정확 하지 않을 수 있습니다. 식의 오른쪽에 있는 식의 끝에 도달 하거나 (정확히 OFF 설정) 두 식의 끝에 도달할 때까지 (EXACT 설정) 문자 식은 왼쪽에서 오른쪽으로 문자에 대 한 문자를 비교 합니다.  
  
 = = 연산자는 문자 데이터의 정확한 비교가 필요한 경우에 사용할 수 있습니다. 두 문자 식을 = = 연산자와 비교 하는 경우 = = 연산자의 양쪽에 있는 식은 같은 문자 (공백 포함)를 포함 하 여 동일 하 게 간주 되어야 합니다. = =를 사용 하 여 문자열을 비교할 때는 정확한 설정 설정이 무시 됩니다.  
  
 다음 표에서는 선택한 연산자와 설정 정확한 설정이 비교에 미치는 영향을 보여 줍니다. 밑줄은 공백을 나타냅니다.  
  
|비교|= 정확히 꺼짐|= EXACT|= = 정확히 설정 또는 해제|  
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
|TRIM ("___") = ""|일치|일치|일치|  
|"" = TRIM ("___")|일치|일치|일치|  
  
## <a name="see-also"></a>관련 항목  
 [SET ANSI 명령](../../odbc/microsoft/set-ansi-command.md)
