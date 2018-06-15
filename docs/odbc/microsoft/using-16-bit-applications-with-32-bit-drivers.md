---
title: 16 비트 응용 프로그램을 사용 하 여 32 비트 드라이버와 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8be9b55137ebbfd0da4a4194b3f29ea57fb89d5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32905488"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>32 비트 드라이버와 16 비트 응용 프로그램을 사용 하 여
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 32 비트 또는 64 비트 드라이버 관리자를 대신 사용 합니다.  
  
 32 비트 드라이버 스레드를 만드는 Win32 API 함수를 명시적으로 호출 하지 않으며으로 Windows 기반 시스템에서 32 비트 드라이버와 16 비트 응용 프로그램을 실행할 수 있습니다. Windows on Windows (WOW) 하위 시스템 16 비트 모드에서 응용 프로그램을 실행 하 고 16 비트 운영 체제 호출을 해결 합니다. ODBC 응용 프로그램을 32 비트 드라이버에서 Dll 해결 16 비트 호출 썽킹 합니다. Windows API를 사용 하는 16 비트 응용 프로그램 및 32 비트 드라이버 Win32 API를 사용 합니다.  
  
## <a name="architecture"></a>Architecture  
 다음 그림과 방법을 16 비트 응용 프로그램을 32 비트 드라이버와 통신 합니다. 32 비트 드라이버와 16 비트 드라이버 관리자는 32 비트 ODBC 호출을 16 비트 ODBC 호출을 변환 하는 Dll 썽킹 제네릭입니다.  
  
 ![어떻게 16&#45;비트 응용 프로그램은 32 통신할&#45;비트 드라이버](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  16 비트 응용 프로그램을 32 비트 드라이버와 상호 작용을 언제 든 지 32 비트 드라이버 관리자는 항상 "2.0" ODBC의 버전으로 드라이버에서 지 원하는 반환 합니다.  
  
## <a name="administration"></a>관리  
 ODBC 데이터 원본 관리자를 사용 하 여 32 비트 드라이버에 대 한 데이터 원본을 관리할 수 있습니다. Microsoft® Windows® 2000을 실행 하는 컴퓨터에서 ODBC 관리자를 열려면 Windows 제어판을 열고, 두 번 클릭 **관리 도구**를 두 번 클릭 하 고 **데이터 원본 (ODBC)** 합니다. 이전 버전의 Microsoft Windows를 실행 하는 컴퓨터에 있는 아이콘 라는 **32 비트 ODBC** 또는 단순히 **ODBC**합니다.  
  
 다음은 16 비트 응용 프로그램을 32 비트 드라이버 설치 DLL을 호출 하는 방법입니다. 16 비트 설치 관리자 DLL 사이의 32 비트 드라이버 설치 DLL은 제네릭 썽킹 DLL DLL 호출을 32 비트 설치 관리자 DLL 호출 16 비트 설치 관리자 변환입니다.  
  
 ![방법를 16&#45;32를 호출 하는 비트 앱&#45;비트 드라이버 설치 DLL](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 (32 비트를 16 비트 썽킹) Windows에서 Windows에서 DLL 32 비트 설치 프로그램을 통해 전달 된 16 비트 인수 값 Ds32gt.dll 변환 추가 썽킹 DLL은 16 비트를 백업 합니다.  
  
## <a name="components"></a>Components  
 MDAC 2.8 s p 1 SDK의 ODBC 구성 요소는 32 비트 드라이버와 16 비트 응용 프로그램을 실행 하기 위한 다음 파일을 포함 합니다. 이러한 구성 요소는 \Redist 디렉터리에 있습니다.  
  
|파일 이름|Description|  
|---------------|-----------------|  
|Odbc16gt.dll|16 비트 ODBC 제네릭 썽킹 DLL|  
|Odbc32gt.dll|32 비트 ODBC 제네릭 썽킹 DLL|  
|Odbccp32.dll|32 비트 설치 관리자 DLL|  
|Odbcad32.exe|32 비트 관리자 프로그램|  
|Odbcinst.hlp|설치 관리자 도움말 파일|  
|Ds16gt.dll|16 비트 드라이버 설치 DLL 썽킹 제네릭|  
|Ctl3d32.dll|32 비트 3 차원 창 스타일 라이브러리|  
  
 또한 ODBC 3.51에 속하지 않은는 16 비트 ODBC 2.10 드라이버 관리자와 함께 다음 파일에 필요한 16 비트 응용 프로그램과 함께 설치 해야 합니다.  
  
|파일 이름|Description|  
|---------------|-----------------|  
|Odbc.dll|16 비트 드라이버 관리자|  
|Odbcinst.dll|16 비트 설치 관리자 DLL|  
|Odbcadm.exe|16 비트 ODBC 관리자 프로그램|
