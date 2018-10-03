---
title: 32 비트 드라이버를 사용 하 여 32 비트 응용 프로그램을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c4f0b21bba9e56cad076ae08f5a561cc972d2ff
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696341"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>32비트 드라이버와 32비트 응용 프로그램 사용
32 비트 드라이버를 사용 하 여 32 비트 응용 프로그램을 실행할 수 있습니다. 32 비트 응용 프로그램 및 32 비트 드라이버 Win32® API를 사용합니다.  
  
## <a name="architecture"></a>Architecture  
 32 비트 응용 프로그램을 표시 하는 다음 그림에서는 32 비트 드라이버와 통신 합니다. 응용 프로그램에 32 비트 드라이버를 호출 하는 32 비트 드라이버 관리자를 호출 합니다.  
  
 ![어떻게 32&#45;32 비트 앱 통신&#45;비트 드라이버만](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  Windows Nt/windows 2000에서 DLL의 32 비트 썽킹 설치 관리자를 사용 하지 마세요. 32 비트 설치 관리자 DLL 파일 이름이 같은 이지만 다른 DLL입니다.  
  
## <a name="administration"></a>관리  
 ODBC 데이터 원본 관리자를 사용 하 여 32 비트 드라이버에 대 한 데이터 원본을 관리할 수 있습니다. Windows 2000을 실행 하는 컴퓨터에서 ODBC 관리자를 열려면 Windows 제어판을 열고, 두 번 클릭 **관리 도구**를 차례로 클릭 한 다음 **데이터 원본 (ODBC)** 합니다. 이전 버전의 Microsoft Windows를 실행 하는 컴퓨터에서 아이콘 이름은 **32 비트 ODBC** 또는 단순히 **ODBC**합니다.  
  
## <a name="components"></a>구성 요소  
 ODBC 구성 요소에는 32 비트 드라이버를 사용 하 여 32 비트 응용 프로그램을 실행 하기 위한 다음 파일이 포함 됩니다. 이러한 구성 요소는 \Redist 디렉터리에 있습니다.  
  
|파일 이름 |Description|  
|---------------|-----------------|  
|Odbc32.dll|32 비트 드라이버 관리자입니다.|  
|Odbccp32.dll|32 비트 설치 관리자 DLL|  
|Odbcad32.exe|32 비트 ODBC 관리자 프로그램|  
|Odbcinst.hlp|설치 관리자 도움말 파일|  
|Msvcrt40.dll|C 런타임 라이브러리|
