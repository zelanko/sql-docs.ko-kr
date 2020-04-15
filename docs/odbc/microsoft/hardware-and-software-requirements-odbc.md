---
title: 하드웨어 및 소프트웨어 요구 사항(ODBC) | 마이크로 소프트 문서
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
ms.openlocfilehash: fe69775e379e9a9d661b4ddf81e577b738fcf34d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295243"
---
# <a name="hardware-and-software-requirements-odbc"></a>하드웨어 및 소프트웨어 요구 사항(ODBC)
이 항목에서는 ODBC 데스크톱 데이터베이스 드라이버 사용에 대한 요구 사항을 나열합니다.  
  
## <a name="hardware-requirements"></a>하드웨어 요구 사항  
 ODBC 데스크톱 데이터베이스 드라이버를 사용하려면 다음이 있어야 합니다.  
  
-   IBM과 호환되는 개인용 컴퓨터입니다.  
  
-   6MB의 여유 디스크 공간이 있는 하드 디스크입니다.  
  
-   최소 16MB의 랜덤 액세스 메모리(RAM).  
  
## <a name="software-requirements"></a>소프트웨어 요구 사항  
 ODBC 드라이버를 사용하여 데이터에 액세스하려면 다음이 있어야 합니다.  
  
-   ODBC 드라이버입니다.  
  
-   32비트 ODBC 드라이버 관리자, 버전 3.51 이상(Odbc32.dll).  
  
-   마이크로 소프트 윈도우 95 이상, 또는 윈도우 NT 4.0 또는 윈도우 2000.  
  
-   Microsoft ODBC 드라이버를 사용하는 응용 프로그램의 스택 크기는 20KB 이상입니다.  
  
 Microsoft Windows NT 4.0 또는 Windows 2000을 사용하는 경우 32비트 드라이버는 스레드에서 안전하지만 드라이버에 대한 액세스를 제어하는 전역 세마포를 사용해야만 사용할 수 있습니다. 드라이버의 동시 사용은 Windows NT에서 매우 제한됩니다. Jet ISAM 계층에 대한 모든 액세스는 Microsoft Jet 엔진을 사용하는 모든 응용 프로그램에 대해 단일 스레드로 연결됩니다.  
  
 마이크로소프트 윈도우 NT 4.0에서 Windows (WOW)에서 Windows에서 여러 16 비트 응용 프로그램을 실행할 때 응용 프로그램은 별도의 메모리 공간에서 실행해야합니다. (ODBC는 동일한 프로세스에서 여러 환경을 지원하지 않으므로 동일한 메모리 공간을 사용할 수 없습니다.) 별도의 메모리 공간에서 응용 프로그램을 실행하려면 프로그램 관리자에서 응용 프로그램의 아이콘을 선택하고 **파일** 메뉴를 열고 **속성을**클릭한 다음 **별도의 메모리 공간에서 실행을**클릭합니다.  
  
 Windows 95에서 16비트 응용 프로그램에서 이러한 드라이버를 사용하는 것은 지원되지 않습니다.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>드라이버별 하드웨어 및 소프트웨어 요구 사항  
  
-   MicrosoftAccess 및 dBASEdriver는 Autoexec.bat 또는 Config.sys 파일을 변경해야 할 수 있습니다.
