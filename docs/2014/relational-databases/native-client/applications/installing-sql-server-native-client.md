---
title: SQL Server Native Client 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, uninstalling
- SQLNCLI, installing
- SQLNCLI, uninstalling
- Setup [SQL Server Native Client]
- uninstalling SQL Server Native Client
- data access [SQL Server Native Client], uninstalling SQL Server Native Client
- installing SQL Server Native Client
- SQL Server Native Client, installing
- data access [SQL Server Native Client], installing SQL Server Native Client
- removing SQL Server Native Client
ms.assetid: c6abeab2-0052-49c9-be79-cfbc50bff5c1
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ca4e2935a8b1ff0ef8ed2571d0e1791206a492bd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187389"
---
# <a name="installing-sql-server-native-client"></a>SQL Server Native Client 설치
  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치할 때 Native Client 11.0이 설치 되어 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]합니다. [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client는 없습니다. 자세한 내용은 참조 [SQL Server Native Client의 새로운](../sql-server-native-client.md)합니다. sqlncli.msi는 SQL Server 2012 기능 팩 웹 페이지에서도 제공됩니다. 최신 버전의 SQL Server Native Client를 다운로드 하려면로 이동 [Microsoft® SQL Server® 2012 SP2 기능 팩](http://www.microsoft.com/en-us/download/details.aspx?id=43339)합니다. 이전 버전의 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client도 SQL Server 2012 컴퓨터에 설치 되어 보다 일찍 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 이전 버전와 함께 설치 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 파일(sqlncli11.dll, sqlnclir11.rll 및 s11ch_sqlncli.chm)은 다음 위치에 설치됩니다.  
  
 `%SYSTEMROOT%\system32\`  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 대한 모든 적절한 레지스트리 설정은 설치 프로세스의 일부로 설정됩니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 헤더 및 라이브러리 파일(sqlncli.h 및 sqlncli11.lib)은 다음 위치에 설치됩니다.  
  
 `%PROGRAMFILES%\Microsoft SQL Server\110\SDK`  
  
 설치 하는 것 외에도 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 일부로 Native Client는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치에 sqlncli.msi 라는 재배포 가능 설치 프로그램은 또한는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다음 위치에 설치 디스크: `%CD%\Setup\`.  
  
 sqlncli.msi를 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 배포할 수 있습니다. 응용 프로그램을 배포할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 설치해야 할 수 있습니다. 여러 패키지를 단일 설치인 것처럼 보이게 설치하려는 경우 chainer와 부트스트래퍼 기술을 사용하는 것이 하나의 방법이 될 수 있습니다. 자세한 내용은 참조 [Visual Studio 2005 용 사용자 지정 부트스트래퍼 패키지 제작](http://go.microsoft.com/fwlink/?LinkId=115667) 및 [사용자 지정 필수 구성 요소 추가](http://go.microsoft.com/fwlink/?LinkId=115668)합니다.  
  
 x64 및 Itanium 버전의 sqlncli.msi가 32비트 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client도 설치합니다. 응용 프로그램을 처음에 개발된 플랫폼이 아니라 다른 플랫폼에서 사용하려는 경우에는 Microsoft 다운로드 센터에서 x64, Itanium 및 x86용 sqlncli.msi 버전을 다운로드할 수 있습니다.  
  
 sqlncli.msi를 호출하면 클라이언트 구성 요소만 기본적으로 설치됩니다. 클라이언트 구성 요소는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client를 사용하여 개발된 응용 프로그램을 실행하는 데 필요한 파일입니다. SDK 구성 요소도 함께 설치하려면 명령줄에 `ADDLOCAL=All`을 지정하면 됩니다. 예를 들어:  
  
 `msiexec /i sqlncli.msi ADDLOCAL=ALL APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
## <a name="silent-install"></a>자동 설치  
 msiexec 명령에 /passive, /qn, /qb, or /qr 옵션을 사용할 경우 IACCEPTSQLNCLILICENSETERMS=YES를 지정하여 최종 사용자 사용권 약관에 동의함을 명시적으로 나타내야 합니다. 이 옵션은 모두 대문자로 지정해야 합니다.  
  
## <a name="uninstalling-sql-server-native-client"></a>SQL Server Native Client 제거  
 때문에 같은 응용 프로그램 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서버 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 도구에 따라 다릅니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 은 제거 하지 않아야 Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 모든 종속 된 응용 프로그램이 제거 될 때까지 Native Client입니다. 응용 프로그램에 의존 하는 경고와 함께 공급자 사용자에 게 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client MSI에 다음과 같이 APPGUID 설치 옵션을 사용 합니다.  
  
 `msiexec /i sqlncli.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
 APPGUID에는 제품 코드를 전달해야 합니다. 제품 코드는 Microsoft 설치 관리자를 사용하여 응용 프로그램 설치 프로그램 번들을 작성할 때 만들어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 사용한 응용 프로그램 작성](installing-sql-server-native-client.md)   
 [설치 방법 도움말 항목](../../../sql-server/install/installation-how-to-topics.md)  
  
  