---
title: 시스템 요구 사항, 설치 및 드라이버 파일 | Microsoft Docs
description: 이 문서에서는 Microsoft ODBC Driver for SQL Server에 대한 시스템 요구 사항을 설명합니다.
ms.custom: ''
ms.date: 03/18/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2b56528a369d58238a545afc20b35787003b6b1
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484472"
---
# <a name="system-requirements-installation-and-driver-files"></a>시스템 요구 사항, 설치 및 드라이버 파일

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 문서에서는 SQL Server에 연결하는 ODBC 드라이버에 대해 설명합니다.

## <a name="sql-version-compatibility"></a>SQL 버전 호환성

호환성은 드라이버가 드라이버의 릴리스 시점에 기존 SQL 릴리스와 호환되는지 테스트되었음을 나타냅니다. 일반적으로 SQL Server 릴리스는 기존 클라이언트 드라이버와 이전 버전과의 호환성을 유지하려고 시도합니다. 그러나 SQL Server 릴리스의 새로운 기능은 이전 클라이언트 드라이버에서 사용하지 못할 수 있습니다.

|드라이버 버전|Azure SQL Database|Azure SQL DW|Azure SQL Managed Instance|SQL Server 2019|SQL Server 2017|SQL Server 2016|SQL Server 2014|SQL Server 2012|SQL Server 2008 R2|SQL Server 2008|SQL Server 2005|
|-|-|-|-|-|-|-|-|-|-|-|-|
|17.5|Y|Y|Y|Y|Y|Y|Y|Y| | | |
|17.4|Y|Y|Y|Y|Y|Y|Y|Y| | | |
|17.3|Y|Y|Y|Y|Y|Y|Y|Y|Y|Y| |
|17.2|Y|Y|Y| |Y|Y|Y|Y|Y|Y| |
|17.1|Y|Y|Y| |Y|Y|Y|Y|Y|Y| |
|17.0|Y|Y|Y| |Y|Y|Y|Y|Y|Y| |
|13.1| | | | |Y|Y|Y|Y|Y|Y| |
|13  | | | | | |Y|Y|Y|Y|Y| |
|11  | | | | | | |Y|Y|Y|Y|Y|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

### <a name="connection-string-details"></a>연결 문자열 정보

연결 문자열에서 지정하는 드라이버 이름은 `ODBC Driver 11 for SQL Server` 또는 `ODBC Driver 13 for SQL Server`(13 및 13.1의 경우) 또는 `ODBC Driver 17 for SQL Server`입니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제

다음 매트릭스는 Windows 운영 체제 버전별 드라이버 버전 지원 여부를 보여 줍니다.

|드라이버 버전|Windows Server 2019|Windows Server 2016|Windows Server 2012 R2|Windows Server 2012|Windows Server 2008 R2|윈도우 10|Windows 8.1|Windows 7|Windows Vista SP2|
|-|-|-|-|-|-|-|-|-|-|
|17.5|Y|Y|Y|Y| |Y|Y| | |
|17.4|Y|Y|Y|Y|Y|Y|Y|Y| |
|17.3|Y|Y|Y|Y|Y|Y|Y|Y| |
|17.2| |Y|Y|Y|Y|Y|Y|Y| |
|17.1| |Y|Y|Y|Y|Y|Y|Y| |
|17.0| |Y|Y|Y|Y|Y|Y|Y| |
|13.1| |Y|Y|Y|Y|Y|Y|Y| |
|13  | | | |Y|Y| |Y|Y| |
|11  | | | |Y|Y| | |Y|Y|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Microsoft SQL Server용 ODBC 드라이버 설치

드라이버는 [Windows용 다운로드](../download-odbc-driver-for-sql-server.md#download-for-windows) 중 하나에서 `msodbcsql.msi`를 실행할 때 설치됩니다.

> [!NOTE]
> Driver 17.1.0.1 이하 버전이 설치되어 있는 사용자의 경우 최신 버전의 Driver를 설치하기 전에 수동으로 제거하는 것이 좋습니다.

### <a name="side-by-side-with-native-client"></a>Native Client와 함께 실행

드라이버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기본 클라이언트가 설치된 상태에서 설치될 수 있습니다. 드라이버의 주 버전(11, 13, 17) 또한 모두 동시에 설치할 수 있습니다.

`msodbcsql.msi`를 호출하면 클라이언트 구성 요소만 기본적으로 설치됩니다. 클라이언트 구성 요소는 드라이버를 사용하여 개발된 애플리케이션을 실행하는 데 필요한 파일입니다. SDK 구성 요소를 설치하려면 명령줄에 `ADDLOCAL=ALL`을 지정합니다. 다음 예를 참조하세요.
  
```console
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  

### <a name="end-user-license"></a>최종 사용자 라이선스

`/passive`, `/qn`, `/qb` 또는 `/qr` 옵션을 사용하여 설치하는 경우 `IACCEPTMSODBCSQLLICENSETERMS=YES`을 지정하여 최종 사용자 사용권에 동의하세요. 이 옵션은 모두 대문자로 지정해야 합니다. 다음 예를 참조하세요.
  
```console
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  

### <a name="silent-uninstall"></a>자동 제거

다음 예제에서는 자동 제거를 수행하는 방법을 보여 줍니다.
  
```console
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  

### <a name="indicate-dependency"></a>종속성 표시

애플리케이션에서 드라이버를 사용하는 경우 애플리케이션은 설치 옵션 `APPGUID`를 통해 드라이버에 종속된 애플리케이션을 나타내야 합니다. 이 표시를 통해 설치를 제거하기 전 드라이버 설치 프로그램에서 종속 애플리케이션을 보고할 수 있습니다. 드라이버에 대한 종속성을 지정하려면 드라이버를 자동으로 설치할 때 `APPGUID` 명령줄 매개 변수를 제품 코드로 설정합니다. 제품 코드는 Microsoft 설치 관리자를 사용하여 애플리케이션 설치 프로그램 번들을 작성할 때 만들어야 합니다. 다음 예를 참조하세요.
  
```console
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>명령줄 도구: sqlcmd.exe 및 bcp.exe

드라이버에 사용되는 `bcp.exe` 및 `sqlcmd.exe` 도구는 [SQL Server용 Microsoft 명령줄 유틸리티 11](https://www.microsoft.com/download/details.aspx?id=36433), [SQL Server용 Microsoft 명령줄 유틸리티 13](https://www.microsoft.com/download/details.aspx?id=52680) 또는 [SQL Server용 Microsoft 명령줄 유틸리티 13.1](https://www.microsoft.com/download/details.aspx?id=53591)에서 다운로드할 수 있습니다. 드라이버는 `sqlcmd.exe` 및 `bcp.exe`를 설치하기 위한 필수 구성 요소입니다.
  
`bcp.exe` 및 `sqlcmd.exe`는 버전 11의 경우 `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC`의 `110\Tools` 하위 폴더, 13 및 13.1의 경우 `130\Tools`에 설치됩니다.

BCP 함수를 사용하는 애플리케이션은 애플리케이션을 컴파일하는 데 사용되는 헤더 파일 및 라이브러리가 함께 제공되는 동일한 버전의 드라이버를 지정해야 합니다.  

예를 들어 `msodbcsql11.lib` 및 `msodbcsql.h`로 ODBC 애플리케이션을 컴파일하는 경우 연결 문자열에 "DRIVER={ODBC Driver 11 for SQL Server}"를 사용합니다.

## <a name="components-of-the-microsoft-odbc-driver-for-ssnoversion-on-windows"></a>Windows 기반 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 ODBC 드라이버 구성 요소

Windows 기반 ODBC 드라이버는 다음 구성 요소를 포함합니다.

| 구성 요소 | Description |
| :-------- | :---------- |
|msodbcsql17.dll 또는 <br/> msodbcsql13.dll or <br/> msodbcsql11.dll|드라이버 기능이 모두 포함된 DLL(동적 연결 라이브러리) 파일입니다. 이 파일은 %SYSTEMROOT%\System32에 설치됩니다.|  
|msodbcdiag17.dll 또는 <br/> msodbcdiag13.dll 또는 <br/> msodbcdiag11.dll|드라이버의 진단(추적) 인터페이스가 포함된 DLL(동적 연결 라이브러리) 파일입니다. 이 파일은 %SYSTEMROOT%\System32에 설치됩니다.|
|msodbcsqlr17.rll 또는 <br/> msodbcsqlr13.rll or <br/> msodbcsqlr11.rll|드라이버 라이브러리에 대한 해당 리소스 파일입니다. 이 파일은 %SYSTEMROOT%\System32\1033에 설치됩니다.| 
|s13ch_msodbcsql.chm or <br/> s11ch_msodbcsql.chm |드라이버용 데이터 원본을 만드는 방법을 문서화하는 데이터 원본 마법사 도움말 파일입니다. 이 파일은 %SYSTEMROOT%\System32\1033에 설치됩니다. <br /> <br /> **참고:** ODBC Driver 17용 chm 파일은 없습니다. |  
|msodbcsql.h|드라이버를 사용하는 데 필요한 새 정의를 모두 포함하는 헤더 파일입니다.<br /><br /> **참고:**  동일한 프로그램에서 msodbcsql.h 및 odbcss.h를 참조할 수 없습니다.<br /><br /> ODBC Driver 17 또는 13용 msodbcsql.h는 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK에 설치됩니다. <br /> ODBC 드라이버 11용 msodbcsql.h는 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK에 설치됩니다.| 
|msodbcsql17.lib 또는 <br/> msodbcsql13.lib or <br/> msodbcsql11.lib|드라이버의 일부인 **bcp** 유틸리티 함수를 호출하는 데 필요한 라이브러리 파일입니다.<br /><br /> **참고:**  프로그램에서 이 라이브러리 파일을 참조하는 경우 시스템 경로 및 해당 애플리케이션을 사용하는 시스템 경로에 있는지 확인합니다.<br /><br /> msodbcsql17.lib 또는 msodbcsql13.lib는 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK에 설치됩니다.<br /> msodbcsql11.lib는 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK에 설치됩니다.|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>참고 항목

[Windows의 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
