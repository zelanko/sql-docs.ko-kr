---
title: 시스템 요구 사항, 설치 및 드라이버 파일 | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd37c097873b104f3f53e9ca92e50b6f7c1acafe
ms.sourcegitcommit: 4cf0fafe565b31262e4148b572efd72c2a632241
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56464769"
---
# <a name="system-requirements-installation-and-driver-files"></a>시스템 요구 사항, 설치 및 드라이버 파일
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 SQL Server 2014, SQL Server 2012 R2, [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)] 및 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에 대한 연결을 지원합니다.  
  
Windows 기반 ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 하나 이상의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 버전이 있는 컴퓨터에도 설치할 수 있습니다.  
  
ODBC Driver 13 및 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 위의 외에도 SQL Server 2016을 지원 합니다. 

ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 지원 위의 모든 항목 및 SQL Server 2017.
  
연결 문자열에서 지정 하는 드라이버 이름은 `ODBC Driver 11 for SQL Server` 나 `ODBC Driver 13 for SQL Server` (에 대 한 13 및 13.1) 또는 `ODBC Driver 17 for SQL Server`합니다.
  
## <a name="supported-operating-systems"></a>지원되는 운영 체제

다음 Windows 운영 체제에서 드라이버를 사용하여 애플리케이션을 실행할 수 있습니다.  

-   Windows Server 2008 R2 
-   Windows Server 2012
-   Windows Server 2012 R2    
-   Windows Vista SP2 *(ODBC Driver 11 에서만)*  
-   Windows 7  
-   Windows 8
-   Windows 8.1
-   Windows 10
  
## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Microsoft SQL Server용 ODBC 드라이버 설치

실행 하면 드라이버가 설치 된 `msodbcsql.msi` 다음 링크 중 하나에서:

- [Windows 기반 Microsoft ODBC Driver 17 for SQL Server 다운로드](https://www.microsoft.com/download/details.aspx?id=56567)
- [Windows 기반 Microsoft SQL Server용 ODBC 드라이버 13.1 다운로드](https://www.microsoft.com/download/details.aspx?id=53339)
- [Windows 기반 Microsoft SQL Server용 ODBC Driver 13 다운로드](https://www.microsoft.com/download/details.aspx?id=50420)
- [Windows 기반 Microsoft SQL Server용 ODBC Driver 11을 다운로드합니다](https://www.microsoft.com/download/details.aspx?id=36434). 

> [!NOTE]
> 이러한 드라이버 17.1.0.1 했거나 아래 설치에 대 한 것이 좋습니다 최신 버전의 드라이버를 설치 하기 전에 수동으로 제거할 수

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client가 설치된 상태에서 설치될 수 있습니다.  

`msodbcsql.msi`를 호출하면 클라이언트 구성 요소만 기본적으로 설치됩니다. 클라이언트 구성 요소는 드라이버를 사용하여 개발된 애플리케이션을 실행하는 데 필요한 파일입니다. SDK 구성 요소를 설치하려면 명령줄에 `ADDLOCAL=ALL`을 지정합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  
  
 `/passive`, `/qn`, `/qb` 또는 `/qr` 옵션을 사용하여 설치하는 경우 `IACCEPTMSODBCSQLLICENSETERMS=YES`을 지정하여 최종 사용자 사용권에 동의하세요. 이 옵션은 모두 대문자로 지정해야 합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  
  
 자동으로 설치를 제거하려면  
  
```  
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  
  
애플리케이션에서 드라이버를 사용하는 경우 애플리케이션은 설치 옵션 `APPGUID`를 통해 드라이버에 종속된 애플리케이션을 나타내야 합니다. 이렇게 하면 설치를 제거하기 전 드라이버 설치 프로그램에서 종속 애플리케이션을 보고할 수 있습니다. 드라이버에 대한 종속성을 지정하려면 드라이버를 자동으로 설치할 때 `APPGUID` 명령줄 매개 변수를 제품 코드로 설정합니다. (제품 코드는 Microsoft 설치 관리자를 사용하여 응용 프로그램 설치 프로그램 번들을 작성할 때 만들어야 합니다.) 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>명령줄 도구: sqlcmd.exe 및 bcp.exe

`bcp.exe` 하 고 `sqlcmd.exe` 도구에서 사용 하 여 드라이버를 다운로드할 수 있습니다 [SQL Server 용 Microsoft 명령줄 유틸리티 11](https://www.microsoft.com/download/details.aspx?id=36433)를 [SQL Server 용 Microsoft 명령줄 유틸리티 13](https://www.microsoft.com/download/details.aspx?id=52680), 또는 [SQL Server 용 Microsoft 명령줄 유틸리티 13.1](https://www.microsoft.com/download/details.aspx?id=53591)합니다. 드라이버를 설치 하려면 필수 구성 요소 `sqlcmd.exe` 고 `bcp.exe`입니다.
  
`bcp.exe` 및 `sqlcmd.exe` 에 설치 됩니다 합니다 `110\Tools` 의 하위 폴더 `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` 버전 11 및 `130\Tools` 13 및 13.1에 대 한 합니다.

BCP 함수를 사용하는 애플리케이션은 애플리케이션을 컴파일하는 데 사용되는 헤더 파일 및 라이브러리가 함께 제공되는 동일한 버전의 드라이버를 지정해야 합니다.  

예를 들어 ODBC 응용 프로그램을 컴파일할 때 `msodbcsql11.lib` 및 `msodbcsql.h`, 사용 하 여 "DRIVER = {ODBC Driver 11 for SQL Server}" 연결 문자열에.

## <a name="components-of-the-microsoft-odbc-driver-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Windows 기반 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]용 ODBC 드라이버 구성 요소 
 Windows 기반 ODBC 드라이버는 다음 구성 요소를 포함합니다.
 
|구성 요소|설명|  
|---------------|-----------------|  
|msodbcsql17.dll or <br> msodbcsql13.dll or <br> msodbcsql11.dll|드라이버 기능이 모두 포함된 DLL(동적 연결 라이브러리) 파일입니다. 이 파일은 %SYSTEMROOT%\System32에서 설치 됩니다.|  
|msodbcdiag17.dll or <br> msodbcdiag13.dll 또는 <br> msodbcdiag11.dll|드라이버의 진단 (추적) 인터페이스를 포함 하는 동적 연결 라이브러리 (DLL) 파일입니다. 이 파일은 %SYSTEMROOT%\System32에서 설치 됩니다.|
|msodbcsqlr17.rll or <br> msodbcsqlr13.rll or <br> msodbcsqlr11.rll|드라이버 라이브러리에 대한 해당 리소스 파일입니다. 이 파일은 %SYSTEMROOT%\System32\1033에서 설치 됩니다.| 
|s13ch_msodbcsql.chm or <br> s11ch_msodbcsql.chm |드라이버용 데이터 원본을 만드는 방법을 문서화하는 데이터 원본 마법사 도움말 파일입니다. 이 파일은 %SYSTEMROOT%\System32\1033 systemroot%\system32\1033에 설치 <br /> <br /> **참고:** ODBC 드라이버 17에 대 한 chm 파일이 없습니다. |  
|msodbcsql.h|드라이버를 사용하는 데 필요한 새 정의를 모두 포함하는 헤더 파일입니다.<br /><br /> **참고:**  동일한 프로그램에서 msodbcsql.h 및 odbcss.h를 참조할 수 없습니다.<br /><br /> ODBC Driver 17 또는 13용 msodbcsql.h는 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK에 설치됩니다. <br /> ODBC 드라이버 11용 msodbcsql.h는 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK에 설치됩니다.| 
|msodbcsql17.lib or <br> msodbcsql13.lib or <br> msodbcsql11.lib|드라이버의 일부인 **bcp** 유틸리티 함수를 호출하는 데 필요한 라이브러리 파일입니다.<br /><br /> **참고:**  프로그램에서 이 라이브러리 파일을 참조하는 경우 시스템 경로 및 해당 애플리케이션을 사용하는 시스템 경로에 있는지 확인합니다.<br /><br /> msodbcsql17.lib 또는 msodbcsql13.lib는 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK에 설치됩니다.<br /> msodbcsql11.lib는 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK에 설치됩니다.|

  
## <a name="see-also"></a>참고 항목  
 [Windows의 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
