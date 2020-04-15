---
title: 번역기 사양 하위 키 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296043"
---
# <a name="translator-specification-subkeys"></a>변환기 사양 서브 키
ODBC 번역기 하위 키에 나열된 각 번역기에는 자체 하위 키가 있습니다. 이 하위 키의 이름은 ODBC 번역기 하위 키 아래의 해당 값과 동일합니다. 이 하위 키 아래의 값에는 번역기 및 번역기 설정 DLL의 전체 경로와 사용 횟수가 나열됩니다. 값의 형식은 다음 표에 나와 있습니다.  
  
|속성|데이터 형식|데이터|  
|----------|---------------|----------|  
|변환기|REG_SZ|*번역기-DLL 경로*|  
|설치 프로그램|REG_SZ|*설정 DLL 경로*|  
|사용량 계산|REG_DWORD|*count*|  
  
 사용량 수에 대한 자세한 내용은 이 섹션의 앞에서 [사용 수를](../../../odbc/reference/install/usage-counting.md) 확인합니다.  
  
 응용 프로그램은 사용 수를 설정해서는 안 됩니다. ODBC는 이 수를 유지합니다.  
  
 예를 들어 Microsoft 코드 페이지 번역기에 Mscpxl32.dll이라는 번역 DLL이 있고, 번역기 설치 기능이 동일한 DLL에 있고, 번역기가 세 번 설치되었다고 가정해 보겠습니다. Microsoft 코드 페이지 번역기 하위 키 아래의 값은 다음과 같습니다.  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
