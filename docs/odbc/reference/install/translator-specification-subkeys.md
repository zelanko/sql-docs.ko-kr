---
title: Translator 지정 하위 키 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ad21943c5313edcb09aba88d45ea21132aa9757f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296043"
---
# <a name="translator-specification-subkeys"></a>변환기 사양 서브 키
ODBC 번역기 하위 키에 나열 된 각 번역기에는 자체의 하위 키가 있습니다. 이 하위 키는 ODBC 번역기 하위 키 아래에 있는 해당 값과 동일한 이름을 갖습니다. 이 하위 키 아래에 있는 값에는 변환기 및 번역기 설치 Dll의 전체 경로와 사용 횟수가 나열 됩니다. 값의 형식은 다음 표에 나와 있습니다.  
  
|속성|데이터 형식|데이터|  
|----------|---------------|----------|  
|변환기|REG_SZ|*translator-DLL 경로*|  
|설치 프로그램|REG_SZ|*설치 프로그램-DLL-경로*|  
|UsageCount|REG_DWORD|*count*|  
  
 사용 횟수에 대 한 자세한 내용은이 섹션의 앞부분에 나오는 [사용량 계산](../../../odbc/reference/install/usage-counting.md) 을 참조 하세요.  
  
 응용 프로그램은 사용 횟수를 설정 하면 안 됩니다. ODBC는이 수를 유지 합니다.  
  
 예를 들어 Microsoft 코드 페이지 변환기에 Mscpxl32 라는 번역 DLL이 있고 변환기 설치 기능이 동일한 DLL에 있으며 변환기가 3 번 설치 되어 있다고 가정 합니다. Microsoft 코드 페이지 변환기 하위 키 아래에 있는 값은 다음과 같을 수 있습니다.  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
