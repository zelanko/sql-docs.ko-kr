---
title: ODBC 핵심 하위 키 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c95c4e28a5f32131307daeaa61e214af887b577
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63069704"
---
# <a name="odbc-core-subkey"></a>ODBC 핵심 하위 키
ODBC 핵심 하위 키 아래에 값을 핵심 구성 요소 (드라이버 관리자, 커서 라이브러리, 설치 관리자 DLL 및 등)에 대 한 사용 횟수를 제공합니다. 이 값의 형식이 다음 표에 표시 됩니다.  
  
|이름|데이터 형식|data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*count*|  
  
 예를 들어, 세 가지 응용 프로그램 및 두 명의 다른 드라이버에 대 한 설치 프로그램에서 ODBC 핵심 구성 요소 설치 ODBC 핵심 하위 키 아래에 값을 다음과 같습니다.  
  
```  
UsageCount : REG_DWORD : 0x5  
```
