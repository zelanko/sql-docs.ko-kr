---
title: 변환기 사양 하위 키 | Microsoft Docs
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
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 163add6fac863912f05378f2e799596f3ad41533
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="translator-specification-subkeys"></a>변환기 사양 하위 키
ODBC 변환기 하위 키에 나열 된 각 변환기 자체의 하위 키를 있습니다. 이 하위 키는 ODBC 변환기 하위 키 아래에서 해당 값으로 동일한 이름을 있습니다. 이 하위 키 아래의 값 변환기 및 변환기 설치 Dll 및 사용 횟수의 전체 경로 나열합니다. 다음 표에 표시 된은 값의 형식입니다.  
  
|이름|데이터 형식|Data|  
|----------|---------------|----------|  
|변환기|REG_SZ|*변환기 DLL 경로*|  
|설치 프로그램|REG_SZ|*설치 프로그램 DLL 경로*|  
|UsageCount|REG_DWORD|*count*|  
  
 사용 횟수에 대 한 정보를 참조 하십시오. [사용 계산](../../../odbc/reference/install/usage-counting.md) 이 섹션의에서 앞부분입니다.  
  
 응용 프로그램 사용 횟수를 설정 해야 합니다. ODBC는이 개수를 유지 합니다.  
  
 예를 들어 코드 페이지 Microsoft Translator 번역 Mscpxl32.dll 변환기 설치 함수 같은 DLL에 있는 이라는 DLL 개이고 변환기가 세 번 설치 되었습니다. 코드 페이지 Microsoft Translator 하위 키 아래에 값은 다음과 같을 수 있습니다.  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
