---
title: 32 비트 드라이버에서 16 비트 응용 프로그램 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c919ed8c3f3791720d67ebdcbf5cfbdbea2a0455
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307634"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>32비트 드라이버와 16비트 애플리케이션 사용
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 대신 32 비트 또는 64 비트 드라이버 관리자를 사용 하십시오.  
  
 32 비트 드라이버가 스레드를 만드는 Win32 API 함수를 명시적으로 호출 하지 않는 한 Windows 기반 시스템에서 32 비트 드라이버를 사용 하 여 16 비트 응용 프로그램을 실행할 수 있습니다. WOW (Windows on Windows) 하위 시스템은 응용 프로그램을 16 비트 모드로 실행 하 고 운영 체제에 대 한 16 비트 호출을 확인 합니다. ODBC 썽킹 Dll은 응용 프로그램에서 32 비트 드라이버로 16 비트 호출을 해결 합니다. 16 비트 응용 프로그램은 Windows API를 사용 하 고 32 비트 드라이버는 Win32 API을 사용 합니다.  
  
## <a name="architecture"></a>Architecture  
 다음 그림에서는 16 비트 응용 프로그램이 32 비트 드라이버와 통신 하는 방법을 보여 줍니다. 16 비트 드라이버 관리자와 32 비트 드라이버 사이에는 16 비트 ODBC 호출을 32 비트 ODBC 호출로 변환 하는 일반 썽킹 Dll이 있습니다.  
  
 ![16&#45;비트 앱이 32&#45;비트 드라이버와 통신 하는 방법](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  16 비트 응용 프로그램이 32 비트 드라이버와 상호 작용 하는 경우 언제 든 지 32 비트 드라이버 관리자는 드라이버에서 지 원하는 ODBC 버전으로 "2.0"를 반환 합니다.  
  
## <a name="administration"></a>관리  
 ODBC 데이터 원본 관리자를 사용 하 여 32 비트 드라이버용 데이터 원본을 관리할 수 있습니다. Microsoft® Windows® 2000를 실행 하는 컴퓨터에서 ODBC 관리자를 열려면 Windows 제어판을 열고 **관리 도구**를 두 번 클릭 한 다음 **데이터 원본 (odbc)** 을 두 번 클릭 합니다. 이전 버전의 Microsoft Windows를 실행 하는 컴퓨터에서는 아이콘 이름이 **32 비트 odbc** 또는 간단히 **odbc**로 지정 됩니다.  
  
 다음 그림에서는 16 비트 응용 프로그램이 32 비트 드라이버 설치 DLL을 호출 하는 방법을 보여 줍니다. 16 비트 설치 관리자 dll과 32 비트 드라이버 설치 DLL 사이에는 16 비트 설치 관리자 DLL 호출을 32 비트 설치 관리자 DLL 호출로 변환 하는 일반 썽킹 DLL이 있습니다.  
  
 ![16&#45;비트 앱이 32&#45;비트 드라이버 설치 DLL을 호출 하는 방법](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 Windows의 Windows (16 비트-32 비트 썽킹)에서 Ds32gt 이라는 추가 썽킹 DLL은 32 비트 설치 DLL을 통해 전달 된 16 비트 인수 값을 다시 16 비트로 변환 합니다.  
  
## <a name="components"></a>구성 요소  
 MDAC 2.8 SP1 SDK의 ODBC 구성 요소에는 32 비트 드라이버를 사용 하 여 16 비트 응용 프로그램을 실행 하기 위한 다음 파일이 포함 되어 있습니다. 이러한 구성 요소는 \Redist 디렉터리에 있습니다.  
  
|파일 이름|Description|  
|---------------|-----------------|  
|Odbc16gt|16 비트 ODBC 제네릭 썽킹 DLL|  
|Odbc32gt|32 비트 ODBC 제네릭 썽킹 DLL|  
|Odbccp32|32 비트 설치 관리자 DLL|  
|Odbcad32.exe|32 비트 관리자 프로그램|  
|Odbcinst.ini|설치 관리자 도움말 파일|  
|Ds16gt|16 비트 드라이버 설치 일반 썽킹 DLL|  
|Ctl3d32|32 비트 3 차원 창 스타일 라이브러리|  
  
 또한 ODBC 3.51에 포함 되지 않은 16 비트 ODBC 2.10 드라이버 관리자와 함께 다음 파일은에 필요 하며, 16 비트 응용 프로그램과 함께 설치 해야 합니다.  
  
|파일 이름|Description|  
|---------------|-----------------|  
|Odbc .dll|16 비트 드라이버 관리자|  
|Odbcinst.ini|16 비트 설치 관리자 DLL|  
|Odbcadm|16 비트 ODBC 관리자 프로그램|
