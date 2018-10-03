---
title: 32 비트 드라이버와 16 비트 응용 프로그램을 사용 하 여 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ebd6f25758f73e75fd96abb734bc7b0347d5ee0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47752931"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>32비트 드라이버와 16비트 응용 프로그램 사용
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 32 비트 또는 64 비트 드라이버 관리자를 대신 사용 합니다.  
  
 32 비트 드라이버 스레드를 만드는 Win32 API 함수를 명시적으로 호출 하지 않으며으로 Windows 기반 시스템에서 32 비트 드라이버와 16 비트 응용 프로그램을 실행할 수 있습니다. Windows (WOW) 하위 시스템에 Windows는 16 비트 모드에서 응용 프로그램을 실행 하 고 16 비트 운영 체제에 대 한 호출을 확인 합니다. ODBC 썽킹 32 비트 드라이버 응용 프로그램에서 Dll 해결 16 비트 호출 합니다. 16 비트 응용 프로그램에는 Windows API를 사용 하 고 32 비트 드라이버 Win32 API를 사용 합니다.  
  
## <a name="architecture"></a>Architecture  
 16 비트 응용 프로그램을 표시 하는 다음 그림에서는 32 비트 드라이버와 통신 합니다. 16 비트 드라이버 관리자와 32 비트 드라이버 사이의 32 비트 ODBC 호출을 16 비트 ODBC 호출을 변환 하는 Dll 썽킹 제네릭입니다.  
  
 ![어떻게 16&#45;32 비트 앱 통신&#45;비트 드라이버만](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  16 비트 응용 프로그램을 32 비트 드라이버와 상호 작용을 언제 든 지 32 비트 드라이버 관리자는 항상 "2.0" 버전의 ODBC 드라이버에서 지 원하는 반환 합니다.  
  
## <a name="administration"></a>관리  
 ODBC 데이터 원본 관리자를 사용 하 여 32 비트 드라이버에 대 한 데이터 원본을 관리할 수 있습니다. Microsoft® Windows® 2000을 실행 하는 컴퓨터에서 ODBC 관리자를 열려면 Windows 제어판을 열고, 두 번 클릭 **관리 도구**를 차례로 클릭 한 다음 **데이터 원본 (ODBC)** 합니다. 이전 버전의 Microsoft Windows를 실행 하는 컴퓨터에서 아이콘 이름은 **32 비트 ODBC** 또는 단순히 **ODBC**합니다.  
  
 다음 그림에서는 16 비트 응용 프로그램을 32 비트 드라이버 설치 DLL을 호출 하는 방법을 보여 줍니다. 16 비트 설치 관리자 DLL 사이의 32 비트 드라이버 설치 DLL에는 32 비트 설치 관리자 DLL 호출에 16 비트 설치 관리자 DLL 호출을 변환 하는 제네릭 썽킹 DLL입니다.  
  
 ![16 하는 방법&#45;는 32 비트 앱이 호출&#45;비트 드라이버 설치 DLL](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 (32 비트를 16 비트 썽킹) Windows에서 Windows, DLL Ds32gt.dll 변환 32 비트 설치 프로그램을 통해 전달 된 16 비트 인수 값 이라는 추가 썽킹 DLL 16 비트를 백업 합니다.  
  
## <a name="components"></a>구성 요소  
 MDAC 2.8 SP1 SDK의 ODBC 구성 요소에는 32 비트 드라이버와 16 비트 응용 프로그램을 실행 하기 위한 다음 파일이 포함 됩니다. 이러한 구성 요소는 \Redist 디렉터리에 있습니다.  
  
|파일 이름 |Description|  
|---------------|-----------------|  
|Odbc16gt.dll|16 비트 ODBC 제네릭 썽킹 DLL|  
|Odbc32gt.dll|32 비트 ODBC 제네릭 썽킹 DLL|  
|Odbccp32.dll|32 비트 설치 관리자 DLL|  
|Odbcad32.exe|32 비트 관리자 프로그램|  
|Odbcinst.hlp|설치 관리자 도움말 파일|  
|Ds16gt.dll|16 비트 드라이버 설치 DLL 썽킹 제네릭|  
|Ctl3d32.dll|32 비트 3 차원 창 스타일 라이브러리|  
  
 또한의 일부분이 아닌 ODBC 3.51에 16 비트 ODBC 2.10 드라이버 관리자와 함께 다음 파일에 필요한 및 16 비트 응용 프로그램을 사용 하 여 설치 해야 합니다.  
  
|파일 이름 |Description|  
|---------------|-----------------|  
|Odbc.dll|16 비트 드라이버 관리자입니다.|  
|경우|16 비트 설치 관리자 DLL|  
|Odbcadm.exe|16 비트 ODBC 관리자 프로그램|
