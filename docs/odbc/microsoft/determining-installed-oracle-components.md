---
title: 설치 된 Oracle 구성 요소 결정 | Microsoft Docs
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
ms.openlocfilehash: 0567e38d34b9400dcaf6b170d821aa0e5fd0e263
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68079007"
---
# <a name="determining-installed-oracle-components"></a>설치된 Oracle 구성 요소 확인
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 시스템 및 해당 버전에 설치 된 Oracle 구성 요소를 확인 하려면 Oracle 홈 디렉터리 아래의 \Orainst 디렉터리로 이동 합니다. 다음 텍스트 파일 중 하나를 엽니다. Nt .rgs, Win95 또는 Win98.  
  
 파일 형식은 다음과 유사 합니다.  
  
```  
0 ntinstall     all    "orainst"  "3.3.1.0.0C"  "Oracle Installer"  
20 w32tcp80     adp80  "tcp80"    "8.0.5.0.0"   "Oracle TCP/IP Pro"  
23 w32nmp80     adp80  "nmp80"    "8.0.5.0.0"   "Oracle Named Pipe"  
26 w32util80    all    "util80"   "8.0.5.0.0"   "Oracle8 Utilities"  
34 w32rsf80     all    "rsf80"    "8.0.5.0.0"   "Required Support"  
47 w32netclt80  net80  "netc80"   "8.0.5.0.0"   "Oracle Net8 Client"  
69 w32plus80    all    "plus80"   "8.0.5.0.0"   "SQL*Plus"  
```  
  
 .Rgs 파일에는 각 구성 요소에 대 한 설치 정보 및 설명도 포함 됩니다.
