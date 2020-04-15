---
title: ODBC 번역기 서브키 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 617416adfcddfbf041c48acbf83cb9589e34ae27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296223"
---
# <a name="odbc-translators-subkey"></a>ODBC 변환기 하위 키
ODBC 번역기 하위 키 아래의 값은 설치된 번역기를 나열합니다. 이러한 값의 형식은 다음 표에 나와 있습니다.  
  
|속성|데이터 형식|데이터|  
|----------|---------------|----------|  
|*번역가 -desc*|REG_SZ|**설치**|  
  
 *번역기-desc* 이름은 번역기 개발자가 정의합니다.  
  
 예를 들어 사용자가 Microsoft® 코드 페이지 번역기및 EBCDIC 번역기에 사용자 지정 ASCII를 설치했다고 가정합니다. ODBC 번역기 하위 키 아래의 값은 다음과 같습니다.  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
