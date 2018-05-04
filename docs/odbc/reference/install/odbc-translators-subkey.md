---
title: ODBC 변환기가 하위 키 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- subkeys [ODBC], translator subkey
- registry entries for components [ODBC], translator subkey
ms.assetid: 6b170f1f-e263-4aac-9d49-8d0ca0470ca2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a6c59901d3e784f1ab845da595c84a4e74a0129
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-translators-subkey"></a>ODBC 변환기가 하위 키
설치 된 변환기가 ODBC 변환기 하위 키 아래 값을 나열합니다. 이러한 값의 서식은 다음 표에 표시 됩니다.  
  
|이름|데이터 형식|Data|  
|----------|---------------|----------|  
|*변환기 desc*|REG_SZ|**설치**|  
  
 *변환기 desc* 변환기 개발자 이름이 정의 됩니다.  
  
 예를 들어 사용자가 설치는 Microsoft® 코드 페이지 변환기 및 사용자 지정 ASCII EBCDIC 변환기를 가정 합니다. ODBC 변환기 하위 키 아래에 값은 다음과 같을 수 있습니다.  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
