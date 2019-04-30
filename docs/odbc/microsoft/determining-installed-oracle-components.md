---
title: 설치 된 Oracle 구성 요소 확인 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], determining installed components
ms.assetid: 3b018f6a-9db0-4aa1-8ec4-afc5f76d7cad
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7de783ae116a61aaa4c8801ca132127352020161
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240275"
---
# <a name="determining-installed-oracle-components"></a>설치된 Oracle 구성 요소 확인
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 시스템 (및 해당 버전)에 설치 된 Oracle 구성 요소를 확인 하려면 Oracle 홈 디렉터리 아래의 \Orainst 디렉터리로 이동 합니다. 다음 텍스트 파일 중 하나를 엽니다. Nt.rgs, Win95.rgs, 또는 Win98.rgs 합니다.  
  
 파일 형식은 다음과 비슷합니다.  
  
```  
0 ntinstall     all    "orainst"  "3.3.1.0.0C"  "Oracle Installer"  
20 w32tcp80     adp80  "tcp80"    "8.0.5.0.0"   "Oracle TCP/IP Pro"  
23 w32nmp80     adp80  "nmp80"    "8.0.5.0.0"   "Oracle Named Pipe"  
26 w32util80    all    "util80"   "8.0.5.0.0"   "Oracle8 Utilities"  
34 w32rsf80     all    "rsf80"    "8.0.5.0.0"   "Required Support"  
47 w32netclt80  net80  "netc80"   "8.0.5.0.0"   "Oracle Net8 Client"  
69 w32plus80    all    "plus80"   "8.0.5.0.0"   "SQL*Plus"  
```  
  
 .Rgs 파일 설치 정보 및 각 구성 요소의 설명을 포함 합니다.
