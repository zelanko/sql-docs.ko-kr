---
title: ODBC 번역기 하위 키 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093939"
---
# <a name="odbc-translators-subkey"></a>ODBC 변환기 하위 키
ODBC 번역기 하위 키 아래에 있는 값에는 설치 된 번역기가 나열 됩니다. 이러한 값의 형식은 다음 표에 나와 있습니다.  
  
|속성|데이터 형식|data|  
|----------|---------------|----------|  
|*번역기-desc*|REG_SZ|**설치한**|  
  
 *변환기-desc* 이름은 translator 개발자에 의해 정의 됩니다.  
  
 예를 들어 사용자가 Microsoft® 코드 페이지 변환기와 사용자 지정 ASCII to EBCDIC 번역기를 설치 했다고 가정 합니다. ODBC 번역기 하위 키 아래에 있는 값은 다음과 같을 수 있습니다.  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
