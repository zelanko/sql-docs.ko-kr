---
title: "시스템 요구 사항, 설치 및 드라이버 파일 | Microsoft Docs"
ms.custom: 
ms.date: 02/14/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f25aa61329742373cff9fcbb38b893500d5baa12
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
---
# <a name="system-requirements-installation-and-driver-files"></a>시스템 요구 사항, 설치 및 드라이버 파일
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 은 SQL Server 2014, SQL Server 2012 R2, [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro_md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)]및 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)]에 대한 연결을 지원합니다.  
  
Windows 기반 ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client 버전이 하나 이상 있는 컴퓨터에도 설치할 수 있습니다.  
  
ODBC Driver 13 및에 대 한 13.1 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], 외에, SQL Server 2016을 지원 합니다. 

에 대 한 ODBC 드라이버 17 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 위의 1 모두 지원 하 고 SQL Server 2017도 합니다.
  
연결 문자열에서 지정 하는 드라이버 이름은 `ODBC Driver 11 for SQL Server` 또는 `ODBC Driver 13 for SQL Server` (에 대해 13 및 13.1) 또는 `ODBC Driver 17 for SQL Server`합니다.
  
## <a name="supported-operating-systems"></a>지원되는 운영 체제

다음 Windows 운영 체제에서 드라이버와 응용 프로그램을 실행할 수 있습니다.  

-   Windows Server 2008 R2 
-   Windows Server 2012
-   Windows Server 2012 R2    
-   Windows Vista SP2 *(ODBC Driver 11만)*  
-   Windows 7  
-   Windows 8
-   Windows 8.1
-   Windows 10
  
## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server 설치

실행 하면 드라이버가 설치 되었는지 `msodbcsql.msi` 다음 링크 중 하나에서:

- [17 기반 Microsoft ODBC Driver for SQL Server 다운로드](https://www.microsoft.com/download/details.aspx?id=56567)
- [Microsoft ODBC Driver 13.1 for SQL Server 다운로드](https://www.microsoft.com/download/details.aspx?id=53339)
- [Microsoft ODBC Driver 13 for SQL Server 다운로드](https://www.microsoft.com/download/details.aspx?id=50420)
- [Microsoft ODBC Driver 11 for SQL Server 다운로드](https://www.microsoft.com/download/details.aspx?id=36434)합니다. 

설치 된--와 함께 수 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client입니다.  

호출 하는 경우 `msodbcsql.msi`, 클라이언트 구성 요소만 기본적으로 설치 됩니다. 클라이언트 구성 요소는 드라이버를 사용 하 여 개발 된 응용 프로그램을 실행 하는 데 파일입니다. SDK 구성 요소를 설치 하려면 지정 `ADDLOCAL=ALL` 명령줄에서. 예를 들어  
  
```  
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  
  
 지정 `IACCEPTMSODBCSQLLICENSETERMS=YES` 사용 하는 경우 최종 사용자 사용권 약관에 동의 하는 `/passive`, `/qn`, `/qb`, 또는 `/qr` 설치 하는 옵션입니다. 이 옵션은 모두 대문자로 지정해야 합니다. 예를 들어  
  
```  
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  
  
 자동으로 설치를 제거하려면  
  
```  
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  
  
응용 프로그램에서 드라이버를 사용 하는 경우 응용 프로그램을 나타내야 설치 옵션을 통해 드라이버에 종속 된 `APPGUID`합니다. 이렇게 하면 특정 보고서 종속 응용 프로그램에 드라이버 설치 프로그램을 제거 하기 전에. 드라이버에 대 한 종속성을 지정 하려면는 `APPGUID` 를 제품 코드로 자동으로 드라이버를 설치할 때 명령줄 매개 변수입니다. (제품 코드는 Microsoft 설치 관리자를 사용하여 응용 프로그램 설치 프로그램 번들을 작성할 때 만들어야 합니다.) 예를 들어  
  
```  
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>명령줄 도구: sqlcmd.exe 및 bcp.exe

`bcp.exe` 및 `sqlcmd.exe` 도구에서 사용 하 여 드라이버를 다운로드할 수 있습니다에 대 한 [SQL Server 용 Microsoft 명령줄 유틸리티 11](http://www.microsoft.com/download/details.aspx?id=36433), [SQL Server 용 Microsoft 명령줄 유틸리티 13](https://www.microsoft.com/download/details.aspx?id=52680), 또는 [SQL Server 용 Microsoft 명령줄 유틸리티 13.1](https://www.microsoft.com/download/details.aspx?id=53591)합니다. 드라이버를 설치 하려면은 `sqlcmd.exe` 및 `bcp.exe`합니다.
  
`bcp.exe` 및 `sqlcmd.exe` 에 설치 되는 `110\Tools` 의 하위 폴더 `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` version 11에 대 한 및 `130\Tools` 13 및 13.1에 대 한 합니다.

BCP 함수를 사용 하는 응용 프로그램은 헤더 파일 및 응용 프로그램을 컴파일하는 데 사용 되는 라이브러리와 함께 제공 되는 동일한 버전의에서 드라이버를 지정 해야 합니다.  

예를 들어 ODBC 응용 프로그램을 컴파일할 때 `msodbcsql11.lib` 및 `msodbcsql.h`를 사용 하 여 "드라이버 = {ODBC Driver 11 for SQL Server}" 연결 문자열에 합니다.

## <a name="components-of-the-microsoft-odbc-driver-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Microsoft ODBC Driver for의 구성 요소 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Windows에서 
 Windows 기반 ODBC 드라이버는 다음 구성 요소를 포함합니다.
 
|구성 요소|Description|  
|---------------|-----------------|  
|msodbcsql17.dll or <br> msodbcsql13.dll 또는 <br> msodbcsql11.dll|드라이버 기능이 모두 포함된 DLL(동적 연결 라이브러리) 파일입니다. 이 파일은 %SYSTEMROOT%\System32에서 설치 됩니다.|  
|msodbcsqlr17.rll 또는 <br> msodbcsqlr13.rll 또는 <br> msodbcsqlr11.rll|드라이버 라이브러리에 대한 해당 리소스 파일입니다. 이 파일은 %SYSTEMROOT%\System32\1033에서 설치 됩니다.| 
|s13ch_msodbcsql.chm or <br> s11ch_msodbcsql.chm |드라이버에 대 한 데이터 원본을 만드는 방법을 문서화 하는 데이터 원본 마법사 도움말 파일입니다. 이 파일은 %SYSTEMROOT%\System32\1033에 설치 됩니다. <br /> <br /> **참고:** ODBC 드라이버 17에 대해 chm 파일이 없습니다. |  
|msodbcsql.h|모든 드라이버를 사용 하는 데 필요한 새 정의 포함 하는 헤더 파일입니다.<br /><br /> **참고:**  동일한 프로그램에서 msodbcsql.h 및 odbcss.h를 참조할 수 없습니다.<br /><br /> ODBC 드라이버 17 또는 13 msodbcsql.h는 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK에에서 설치 됩니다. <br /> ODBC Driver 11에 대 한 msodbcsql.h는 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK에에서 설치 되어 있습니다.| 
|msodbcsql17.lib or <br> msodbcsql13.lib or <br> msodbcsql11.lib|호출 하는 데 필요한 라이브러리 파일의 **bcp** 드라이버의 일부인 유틸리티 함수입니다.<br /><br /> **참고:** 프로그램에서이 라이브러리 파일 참조를 하는 경우 시스템 경로 및 응용 프로그램을 사용 하는 시스템 경로에 있는지 확인 하십시오.<br /><br /> msodbcsql17.lib 또는 msodbcsql13.lib는 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK에에서 설치 됩니다.<br /> msodbcsql11.lib는 %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK에 설치됩니다.|

  
## <a name="see-also"></a>관련 항목:  
 [Windows의 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
