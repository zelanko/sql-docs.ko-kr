---
description: 32비트 드라이버와 32비트 애플리케이션 사용
title: 32 비트 드라이버에서 32 비트 응용 프로그램 사용 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69005071c83047471e76f38160265bc35cdccd4b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471367"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>32비트 드라이버와 32비트 애플리케이션 사용
32 비트 드라이버를 사용 하 여 32 비트 응용 프로그램을 실행할 수 있습니다. 32 비트 응용 프로그램 및 32 비트 드라이버는 Win32® API를 사용 합니다.  
  
## <a name="architecture"></a>Architecture  
 다음 그림에서는 32 비트 응용 프로그램이 32 비트 드라이버와 통신 하는 방법을 보여 줍니다. 응용 프로그램은 32 비트 드라이버를 호출 하는 32 비트 드라이버 관리자를 호출 합니다.  
  
 ![32&#45;비트 앱이 32&#45;비트 드라이버와 통신 하는 방법](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  Windows nt/Windows 2000에서 32 비트 썽킹 설치 관리자 DLL을 사용 하지 마십시오. 32 비트 설치 관리자 DLL과 파일 이름이 동일 하지만 DLL은 다른 DLL입니다.  
  
## <a name="administration"></a>관리  
 ODBC 데이터 원본 관리자를 사용 하 여 32 비트 드라이버용 데이터 원본을 관리할 수 있습니다. Windows 2000를 실행 하는 컴퓨터에서 ODBC 관리자를 열려면 Windows 제어판을 열고 **관리 도구**를 두 번 클릭 한 다음 **데이터 원본 (ODBC)** 을 두 번 클릭 합니다. 이전 버전의 Microsoft Windows를 실행 하는 컴퓨터에서는 아이콘 이름이 **32 비트 odbc** 또는 간단히 **odbc**로 지정 됩니다.  
  
## <a name="components"></a>구성 요소  
 ODBC 구성 요소에는 32 비트 드라이버를 사용 하 여 32 비트 응용 프로그램을 실행 하기 위한 다음 파일이 포함 되어 있습니다. 이러한 구성 요소는 \Redist 디렉터리에 있습니다.  
  
|파일 이름|Description|  
|---------------|-----------------|  
|Odbc32.dll|32 비트 드라이버 관리자|  
|Odbccp32.dll|32 비트 설치 관리자 DLL|  
|Odbcad32.exe|32 비트 ODBC 관리자 프로그램|  
|Odbcinst.ini|설치 관리자 도움말 파일|  
|Msvcrt40.dll|C 런타임 라이브러리|
