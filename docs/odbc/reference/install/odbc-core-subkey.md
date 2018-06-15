---
title: ODBC 핵심 하위 키 | Microsoft Docs
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
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f05e36c59d674104dead92ecd7da63f5fb58588a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916068"
---
# <a name="odbc-core-subkey"></a>ODBC 핵심 하위 키
ODBC 핵심 하위 키 아래에 있는 값의 핵심 구성 요소 (드라이버 관리자, 커서 라이브러리, DLL, 설치 관리자 및 등)에 대 한 사용 개수를 제공합니다. 이 값의 형식은 다음 표에 표시 됩니다.  
  
|이름|데이터 형식|Data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*count*|  
  
 예를 들어 세 개의 서로 다른 응용 프로그램 및 두 명의 서로 다른 드라이버 설치 프로그램에서 ODBC 핵심 구성 요소가 설치 되었습니다. ODBC 핵심 하위 키 아래에 있는 값이 합니다.  
  
```  
UsageCount : REG_DWORD : 0x5  
```
