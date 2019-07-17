---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c09ddcac1409da08fedeaf946ac7fb9f6ef668e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952449"
---
# <a name="hardware-and-software-requirements-odbc"></a>하드웨어 및 소프트웨어 요구 사항(ODBC)
이 항목에서는 ODBC 데스크톱 데이터베이스 드라이버를 사용 하 여 요구 사항을 나열 합니다.  
  
## <a name="hardware-requirements"></a>하드웨어 요구 사항  
 ODBC 데스크톱 데이터베이스 드라이버를 사용 하려면 다음이 있어야 합니다.  
  
-   IBM 호환 개인용 컴퓨터입니다.  
  
-   6 MB의 사용 가능한 디스크 공간을 사용 하 여 하드 디스크입니다.  
  
-   16MB 이상의 random access memory (RAM)입니다.  
  
## <a name="software-requirements"></a>소프트웨어 요구 사항  
 ODBC 드라이버를 사용 하 여 데이터에 액세스 하려면 있어야 합니다.  
  
-   ODBC 드라이버입니다.  
  
-   32 비트 ODBC 드라이버 관리자, 버전 3.51 또는 이후 (Odbc32.dll).  
  
-   Microsoft Windows 95 이상 또는 Windows NT 4.0 또는 Windows 2000입니다.  
  
-   적어도 20kb 기반 Microsoft ODBC driver를 사용 하 여 응용 프로그램에 대 한 스택 크기입니다.  
  
 Microsoft Windows NT 4.0 또는 Windows 2000을 사용 하는 경우 32 비트 드라이버는 스레드로부터 안전 하지만 드라이버 액세스를 제어 하는 전역 세마포를 사용 하 여만 합니다. 드라이버 동시 사용은 매우 제한 된 Windows NT에서. Microsoft Jet 엔진을 사용 하 여 모든 응용 프로그램에 대 한 단일 스레드 Jet ISAM 계층에 대 한 모든 액세스가 됩니다.  
  
 Windows에서 Windows (WOW)에서 Microsoft Windows NT 4.0에서 여러 개의 16 비트 응용 프로그램을 실행 하는 경우 응용 프로그램을 별도 메모리 공간에서 실행 되어야 합니다. (동일한 메모리 공간 ODBC 동일한 프로세스에서 여러 환경을 지원 하지 않으므로 사용할 수 없습니다.) 별도 메모리 공간에서 응용 프로그램을 실행 하려면 아이콘을 선택 응용 프로그램의 프로그램 관리자에서 엽니다는 **파일** 메뉴를 클릭 **속성**를 클릭 하 고 **별도 메모리에서 실행 공간**입니다.  
  
 Windows 95에서 16 비트 응용 프로그램에서 이러한 드라이버를 사용 하 여 지원 되지 않습니다.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>드라이버 관련 하드웨어 및 소프트웨어 요구 사항  
  
-   DBASEdrivers 고 MicrosoftAccess Autoexec.bat 또는 Config.sys 파일에서 변경 해야 합니다.
