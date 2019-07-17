---
title: ODBC 변환기 하위 키 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- subkeys [ODBC], translator subkey
- registry entries for components [ODBC], translator subkey
ms.assetid: 6b170f1f-e263-4aac-9d49-8d0ca0470ca2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d26f2d33d81e08cfe4bddff9b2260bd2f098f00
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093939"
---
# <a name="odbc-translators-subkey"></a>ODBC 변환기 하위 키
ODBC 변환기 하위 키 아래에서 값을 설치 하는 변환기를 나열합니다. 이러한 값의 형식은 다음 표에 표시 됩니다.  
  
|이름|데이터 형식|data|  
|----------|---------------|----------|  
|*translator-desc*|REG_SZ|**설치**|  
  
 합니다 *translator desc* 이름은 translator 개발자가 정의 됩니다.  
  
 예를 들어, 사용자가 설치 된 Microsoft® 코드 페이지 Translator 및 사용자 지정 ASCII EBCDIC 변환기에 대 한 합니다. ODBC 변환기 하위 키 아래의 값은 다음과 같을 수 있습니다.  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
