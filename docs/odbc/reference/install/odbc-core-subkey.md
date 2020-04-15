---
title: ODBC 코어 서브키 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9e6bfcf3c1efa87076e6d3e27a438cde6f794157
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304060"
---
# <a name="odbc-core-subkey"></a>ODBC 핵심 하위 키
ODBC Core 하위 키 아래의 값은 핵심 구성 요소(드라이버 관리자, 커서 라이브러리, 설치 관리자 DLL 등)에 대한 사용 수를 제공합니다. 이 값의 형식은 다음 표에 나와 있습니다.  
  
|속성|데이터 형식|데이터|  
|----------|---------------|----------|  
|사용량 계산|REG_DWORD|*count*|  
  
 예를 들어, ODBC 코어 구성 요소가 세 가지 다른 응용 프로그램과 두 개의 서로 다른 드라이버에 대한 설치 프로그램에 의해 설치되었다고 가정합니다. ODBC 코어 하위 키 아래의 값은 다음과 같은 것입니다.  
  
```  
UsageCount : REG_DWORD : 0x5  
```
