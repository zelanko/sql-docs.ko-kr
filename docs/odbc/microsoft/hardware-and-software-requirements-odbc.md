---
description: 하드웨어 및 소프트웨어 요구 사항(ODBC)
title: 하드웨어 및 소프트웨어 요구 사항 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- hardware requirements [ODBC], desktop database drivers
- software requirements [ODBC], desktop database drivers
- system requirements [ODBC], desktop database drivers
- requirements [ODBC], desktop database drivers
ms.assetid: 6df2e9cd-de10-4629-97bd-32f2782616c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0f88c8877161122c11fb65bcdb62fd4e7b684c3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412489"
---
# <a name="hardware-and-software-requirements-odbc"></a>하드웨어 및 소프트웨어 요구 사항(ODBC)
이 항목에서는 ODBC 데스크톱 데이터베이스 드라이버를 사용 하기 위한 요구 사항을 나열 합니다.  
  
## <a name="hardware-requirements"></a>하드웨어 요구 사항  
 ODBC 데스크톱 데이터베이스 드라이버를 사용 하려면 다음이 있어야 합니다.  
  
-   IBM 호환 개인용 컴퓨터  
  
-   사용 가능한 디스크 공간이 6mb 인 하드 디스크  
  
-   16mb 이상의 RAM (임의 액세스 메모리).  
  
## <a name="software-requirements"></a>소프트웨어 요구 사항  
 ODBC 드라이버를 사용 하 여 데이터에 액세스 하려면 다음이 있어야 합니다.  
  
-   ODBC 드라이버입니다.  
  
-   32 비트 ODBC 드라이버 관리자, 버전 3.51 이상 (Odbc32.dll)  
  
-   Microsoft Windows 95 이상 또는 Windows NT 4.0 또는 Windows 2000.  
  
-   Microsoft ODBC 드라이버를 사용 하는 응용 프로그램에 대해 최소 20KB의 스택 크기입니다.  
  
 Microsoft Windows NT 4.0 또는 Windows 2000을 사용 하는 경우 32 비트 드라이버는 스레드로부터 안전 하지만 드라이버에 대 한 액세스를 제어 하는 전역 세마포를 사용 하는 경우에만 사용 됩니다. 드라이버의 동시 사용은 Windows NT에서 매우 제한적입니다. Jet ISAM 계층에 대 한 모든 액세스는 Microsoft Jet 엔진을 사용 하는 모든 응용 프로그램에 대 한 단일 스레드입니다.  
  
 Microsoft Windows NT 4.0의 WOW (Windows on Windows)에서 여러 16 비트 응용 프로그램을 실행 하는 경우 응용 프로그램을 별도의 메모리 공간에서 실행 해야 합니다. ODBC는 동일한 프로세스에서 여러 환경을 지원 하지 않으므로 동일한 메모리 공간을 사용할 수 없습니다. 별도의 메모리 공간에서 응용 프로그램을 실행 하려면 프로그램 관리자에서 응용 프로그램 아이콘을 선택 하 고, **파일** 메뉴를 열고, **속성**을 클릭 한 다음 **별도의 메모리 공간에서 실행**을 클릭 합니다.  
  
 Windows 95의 16 비트 응용 프로그램에서 이러한 드라이버를 사용 하는 것은 지원 되지 않습니다.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>드라이버 특정 하드웨어 및 소프트웨어 요구 사항  
  
-   MicrosoftAccess 및 드라이버는 Autoexec.bat 또는 Config.sys 파일을 변경 해야 할 수 있습니다.
