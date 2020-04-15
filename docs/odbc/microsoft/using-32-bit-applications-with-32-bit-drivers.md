---
title: 32비트 드라이버가 있는 32비트 애플리케이션 사용 | 마이크로 소프트 문서
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
ms.openlocfilehash: 31512f9339b9d46225bb4f1198cb617a48509acb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307604"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>32비트 드라이버와 32비트 애플리케이션 사용
32비트 드라이버로 32비트 응용 프로그램을 실행할 수 있습니다. 32비트 응용 프로그램과 32비트 드라이버는 Win32® API를 사용합니다.  
  
## <a name="architecture"></a>Architecture  
 다음 그림에서는 32비트 응용 프로그램이 32비트 드라이버와 통신하는 방법을 보여 주어 도 있습니다. 응용 프로그램은 32비트 드라이버 관리자를 호출하고, 이 드라이버는 32비트 드라이버를 호출합니다.  
  
 ![32&#45;비트 앱이 32개의&#45;비트 드라이버와 통신하는 방법](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  WindowsNT/Windows2000에서 32비트 터킹 설치 관리자 DLL을 사용하지 마십시오. 32비트 설치 프로그램 DLL과 동일한 파일 이름을 가지고 있지만 다른 DLL입니다.  
  
## <a name="administration"></a>관리  
 ODBC 데이터 원본 관리자를 사용하여 32비트 드라이버의 데이터 원본을 관리할 수 있습니다. Windows 2000을 실행하는 컴퓨터에서 ODBC 관리자를 열려면 Windows 제어판을 열고 **관리 도구를**두 번 클릭한 다음 **ODBC(데이터 원본)를**두 번 클릭합니다. 마이크로 소프트 윈도우의 이전 버전을 실행하는 컴퓨터에서, 아이콘은 **32 비트 ODBC** 또는 단순히 ODBC 의 이름이 **지정됩니다**.  
  
## <a name="components"></a>구성 요소  
 ODBC 구성 요소에는 32비트 드라이버가 있는 32비트 응용 프로그램을 실행하기 위한 다음 파일이 포함되어 있습니다. 이러한 구성 요소는 \Redist 디렉터리에 있습니다.  
  
|파일 이름|설명|  
|---------------|-----------------|  
|Odbc32.dll|32비트 드라이버 관리자|  
|Odbccp32.dll|32비트 설치 관리자 DLL|  
|Odbcad32.exe|32비트 ODBC 관리자 프로그램|  
|오드빈스트.hlp|설치 관리자 도움말 파일|  
|Msvcrt40.dll|C 런타임 라이브러리|
