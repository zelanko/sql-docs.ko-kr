---
title: 드라이버 버전 체계 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], versions
ms.assetid: e4a8d9d7-8aba-48ab-8be6-1a6129adfb8f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1151f1ce5c1c8644c448555e25a03a0b455e1a9d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="driver-version-scheme"></a>드라이버 버전 체계
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 다음 표에서 Microsoft ODBC Driver for Oracle의 릴리스 버전을 모두 나열합니다.  
  
|드라이버 버전|빌드 번호|가용성 기록|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual c + + 4.2 및 Visual Basic 5.0, Enterprise Edition|  
|2.0|2.73.7269|Visual Studio 97와 MDAC 1.5 a|  
|2.0 업데이트|2.73.7283.01|IIS 4.0|  
|2.0 업데이트|2.73.7283.03|MDAC 1.5b 및 1.5 c|  
|2.0 업데이트|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|Visual Studio 6.0 및 MDAC 2.0|  
|2.5 업데이트|2.573.3513|SQL Server 7.0<br /><br /> SQL Server 6.5 SP5|  
  
 빌드 2.00.6235 (버전 1)는 Microsoft ODBC Driver for Oracle의 첫 번째 릴리스에서 했습니다. 첫 번째 버전의 릴리스 이후 새 명명 규칙이 적용 됩니다.  
  
 예를 들어 2.73.7283.03 다음 다른 구성으로 나눌 수 있습니다.  
  
-   2 = 버전 번호입니다.  
  
-   73 = 드라이버 디자인 된 Oracle 서버 버전입니다.  
  
-   7283.03 = 드라이버의 빌드 번호입니다.  
  
> [!NOTE]  
>  와 2.573.2973 릴리스, 명명 규칙을 유발 하 고 일부 혼란이 2.573 2.73 보다 이전 버전은 있지만 빌드 번호의 각 섹션은 개별적으로 고려해 야 합니다. 573 번호 보다 큰 경우 73, 최신 버전 이므로 또한 "2.5" 드라이버의 버전 번호를 나타냅니다.
