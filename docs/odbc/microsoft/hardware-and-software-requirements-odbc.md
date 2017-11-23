---
title: "하드웨어 및 소프트웨어 요구 사항 (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hardware requirements [ODBC], desktop database drivers
- software requirements [ODBC], desktop database drivers
- system requirements [ODBC], desktop database drivers
- requirements [ODBC], desktop database drivers
ms.assetid: 6df2e9cd-de10-4629-97bd-32f2782616c7
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b9b4ec33220da4395f2bad0de29fb9ec1be1ffa9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="hardware-and-software-requirements-odbc"></a>하드웨어 및 소프트웨어 요구 사항 (ODBC)
이 항목에서는 ODBC 데스크톱 데이터베이스 드라이버를 사용 하기 위한 요구 사항을 나열 합니다.  
  
## <a name="hardware-requirements"></a>하드웨어 요구 사항  
 ODBC 데스크톱 데이터베이스 드라이버를 사용 하려면 다음이 있어야 합니다.  
  
-   IBM 호환 개인용 컴퓨터입니다.  
  
-   6MB의 여유 디스크 공간이 있는 하드 디스크.  
  
-   이상 16MB의 임의-access RAM.  
  
## <a name="software-requirements"></a>소프트웨어 요구 사항  
 ODBC 드라이버를 사용 하 여 데이터에 액세스 하려면 다음이 있어야 합니다.  
  
-   ODBC 드라이버입니다.  
  
-   32 비트 ODBC 드라이버 관리자, 버전 3.51 또는 이후 (Odbc32.dll).  
  
-   Microsoft Windows 95 이상 또는 Windows NT 4.0 또는 Windows 2000입니다.  
  
-   Microsoft ODBC 드라이버를 사용 하 여 응용 프로그램에 대 한 20 KB 최소한의 스택 크기입니다.  
  
 Microsoft Windows NT 4.0 또는 Windows 2000을 사용할 때 스레드로부터 안전 하지만 드라이버에 액세스를 제어 하는 전역 세마포 사용 하 여 32 비트 드라이버는 합니다. 드라이버의 동시 사용은 매우 제한 된 Windows nt 합니다. Microsoft Jet 엔진을 사용 하 여 모든 응용 프로그램에 대 한 단일 스레드 Jet ISAM 계층에 대 한 모든 액세스가 됩니다.  
  
 를 Windows에서 Windows (WOW) Microsoft Windows NT 4.0에서 여러 개의 16 비트 응용 프로그램을 실행 하는 경우 응용 프로그램은 서로 다른 메모리 공간에서 실행 되어야 합니다. (동일한 메모리 공간 ODBC가 동일한 프로세스에서 여러 환경을 지원 하지 않으므로 사용할 수 없습니다.) 응용 프로그램을 별도 메모리 공간에서를 실행 하려면 응용 프로그램의 아이콘에는 프로그램 관리자를 선택 열기는 **파일** 메뉴를 클릭 **속성**, 클릭 하 고 **별도 메모리에서 실행 공간**합니다.  
  
 Windows 95에서 16 비트 응용 프로그램에서 이들이 드라이버를 사용 하는 지원 되지 않습니다.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>드라이버 관련 하드웨어 및 소프트웨어 요구 사항  
  
-   MicrosoftAccess 및 dBASEdrivers Autoexec.bat 또는 Config.sys 파일의 변경 내용이 필요할 수 있습니다.
