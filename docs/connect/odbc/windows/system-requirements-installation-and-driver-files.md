---
title: 시스템 요구 사항, 설치 및 드라이버 파일 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6365b86a4efe8d29273035d62f76c7bb02b15335
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74908852"
---
# <a name="system-requirements-installation-and-driver-files"></a>시스템 요구 사항, 설치 및 드라이버 파일

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

이 문서에서는 SQL Server에 연결하는 ODBC 드라이버에 대해 설명합니다.

## <a name="driver-versions"></a>드라이버 버전

| 드라이버 버전 | 지원 설명 |
| :------------- | :--------------------- |
| ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | SQL Server 2014, SQL Server 2012, [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)], [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 대한 연결을 지원합니다. |
| Windows 기반 ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | 하나 이상의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 버전이 있는 컴퓨터에도 설치할 수 있습니다. |
| ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | SQL Server 2016, SQL Server 2014, SQL Server 2012, [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)]에 대한 연결을 지원합니다. |
| ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | 위 13 버전의 경우 외에도 SQL Server 2017을 지원합니다. |
| ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | 13.1과 동일한 데이터베이스 버전을 지원합니다. |
| ODBC Driver 17 for SQL Server | 드라이버 버전 17.3부터 SQL Server 2019를 지원합니다. |
| &nbsp; | &nbsp; |

### <a name="connection-string-details"></a>연결 문자열 정보

연결 문자열에서 지정하는 드라이버 이름은 `ODBC Driver 11 for SQL Server` 또는 `ODBC Driver 13 for SQL Server`(13 및 13.1의 경우) 또는 `ODBC Driver 17 for SQL Server`입니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제

다음 Windows 운영 체제에서 드라이버를 사용하여 애플리케이션을 실행할 수 있습니다.  

- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Vista SP2 &nbsp; _(ODBC Driver 11만 해당)_
- Windows 7
- Windows 8
- Windows 8.1
- 윈도우 10

## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Microsoft SQL Server용 ODBC 드라이버 설치

다음 링크 중 하나에서 `msodbcsql.msi`를 실행하면 드라이버가 설치됩니다.

- [Windows 기반 Microsoft ODBC Driver 17 for SQL Server 다운로드](https://www.microsoft.com/download/details.aspx?id=56567)
- [Windows 기반 Microsoft ODBC Driver 13.1 for SQL Server 다운로드](https://www.microsoft.com/download/details.aspx?id=53339)
- [Windows 기반 Microsoft SQL Server용 ODBC Driver 13 다운로드](https://www.microsoft.com/download/details.aspx?id=50420)
- [Windows 기반 Microsoft ODBC Driver 11 for SQL Server 다운로드](https://www.microsoft.com/download/details.aspx?id=36434)

> [!NOTE]
> Driver 17.1.0.1 이하 버전이 설치되어 있는 사용자의 경우 최신 버전의 Driver를 설치하기 전에 수동으로 제거하는 것이 좋습니다.

### <a name="side-by-side-with-native-client"></a>Native Client와 함께 실행

드라이버는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기본 클라이언트가 설치된 상태에서 설치될 수 있습니다.

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

## <a name="components-of-the-microsoft-odbc-driver-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 기반 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 ODBC 드라이버 구성 요소

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
