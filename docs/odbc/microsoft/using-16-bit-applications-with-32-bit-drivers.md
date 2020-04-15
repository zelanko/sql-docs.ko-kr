---
title: 32비트 드라이버가 있는 16비트 애플리케이션 사용 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307634"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>32비트 드라이버와 16비트 애플리케이션 사용
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 대신 32비트 또는 64비트 드라이버 관리자를 사용합니다.  
  
 32비트 드라이버가 스레드를 만드는 Win32 API 함수를 명시적으로 호출하지 않는 한 Windows 기반 시스템에서 32비트 드라이버를 사용하여 16비트 응용 프로그램을 실행할 수 있습니다. Windows 의 Windows(WOW) 하위 시스템은 16비트 모드에서 응용 프로그램을 실행하고 운영 체제에 대한 16비트 호출을 해결합니다. ODBC tunking DLL은 응용 프로그램에서 32비트 드라이버로 16비트 호출을 해결합니다. 16비트 응용 프로그램은 Windows API를 사용하고 32비트 드라이버는 Win32 API를 사용합니다.  
  
## <a name="architecture"></a>Architecture  
 다음 그림에서는 16비트 응용 프로그램이 32비트 드라이버와 통신하는 방법을 보여 주어 도 있습니다. 16비트 드라이버 관리자와 32비트 드라이버 사이에는 16비트 ODBC 호출을 32비트 ODBC 호출로 변환하는 일반 DLL이 있습니다.  
  
 ![16개의&#45;비트 앱이 32개의 비트 드라이버와 통신하는 방법&#45;](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  16비트 응용 프로그램이 32비트 드라이버와 상호 작용할 때마다 32비트 드라이버 관리자는 항상 드라이버에서 지원하는 ODBC 버전으로 "2.0"을 반환합니다.  
  
## <a name="administration"></a>관리  
 ODBC 데이터 원본 관리자를 사용하여 32비트 드라이버의 데이터 원본을 관리할 수 있습니다. 마이크로소프트를 실행 하는 컴퓨터에서 ODBC 관리자를 엽니다® Windows® 2000, Windows 제어판을 열고 **관리 도구를**두 번 클릭 하 고 데이터 **소스 (ODBC)를**두 번 클릭 합니다. 마이크로 소프트 윈도우의 이전 버전을 실행하는 컴퓨터에서, 아이콘은 **32 비트 ODBC** 또는 단순히 ODBC 의 이름이 **지정됩니다**.  
  
 다음 그림에서는 16비트 응용 프로그램이 32비트 드라이버 설정 DLL을 호출하는 방법을 보여 주며 있습니다. 16비트 설치 프로그램 DLL과 32비트 드라이버 설치 DLL 사이에는 16비트 설치 프로그램 DLL 호출을 32비트 설치 관리자 DLL 호출로 변환하는 일반적인 Thunking DLL이 있습니다.  
  
 ![16&#45;비트 앱이 32 비트 드라이버 설정 DLL을 호출하는&#45;방법](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 Windows에서 Windows(16비트에서 32비트 톤으로) Ds32gt.dll이라는 추가 번킹 DLL은 32비트 설정 DLL을 통과한 16비트 인수 값을 16비트로 변환합니다.  
  
## <a name="components"></a>구성 요소  
 MDAC 2.8 SP1 SDK의 ODBC 구성 요소에는 32비트 드라이버로 16비트 응용 프로그램을 실행하기 위한 다음 파일이 포함되어 있습니다. 이러한 구성 요소는 \Redist 디렉터리에 있습니다.  
  
|파일 이름|설명|  
|---------------|-----------------|  
|Odbc16gt.dll|16비트 ODBC 일반 툰킹 DLL|  
|Odbc32gt.dll|32비트 ODBC 일반 툰킹 DLL|  
|Odbccp32.dll|32비트 설치 프로그램 DLL|  
|Odbcad32.exe|32비트 관리자 프로그램|  
|오드빈스트.hlp|설치 관리자 도움말 파일|  
|Ds16gt.dll|16비트 드라이버 설정 일반 툰킹 DLL|  
|Ctl3d32.dll|32비트 3차원 창 스타일 라이브러리|  
  
 또한 ODBC 3.51의 일부가 아닌 16비트 ODBC 2.10 드라이버 관리자와 함께 다음 파일이 필요하며 16비트 응용 프로그램과 함께 설치해야 합니다.  
  
|파일 이름|설명|  
|---------------|-----------------|  
|Odbc.dll|16비트 드라이버 관리자|  
|오드빈스트.dll|16비트 설치 관리자 DLL|  
|오드카드m.exe|16비트 ODBC 관리자 프로그램|
