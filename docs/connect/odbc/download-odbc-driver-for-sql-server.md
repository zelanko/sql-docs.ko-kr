---
title: SQL Server용 ODBC 드라이버 다운로드
description: Microsoft ODBC Driver for SQL Server를 다운로드하여 SQL Server 및 Azure SQL Database에 연결하는 네이티브 코드 애플리케이션을 개발합니다.
ms.date: 07/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53b09784-bb9d-4fd4-99d3-0492b3308ac4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1f77ce4eb0b329fdb6911bd38f6e120e4ff7d3d
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727539"
---
# <a name="download-odbc-driver-for-sql-server"></a>SQL Server용 ODBC 드라이버 다운로드

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Microsoft ODBC Driver for SQL Server는 네이티브 코드 API를 사용하여 SQL Server에 연결하는 애플리케이션에 대한 런타임 지원을 포함하는 단일 DLL(동적 연결 라이브러리)입니다. Microsoft ODBC Driver 17 for SQL Server를 사용하여 새로운 SQL Server 기능을 활용해야 하는 새로운 애플리케이션을 만들거나 기존 애플리케이션을 개선할 수 있습니다.

## <a name="download-for-windows"></a>Windows용 다운로드

Microsoft ODBC Driver 17 for SQL Server 재배포 가능 설치 관리자는 런타임에 최신 SQL Server 기능을 활용하는 데 필요한 클라이언트 구성 요소를 설치합니다. 필요에 따라 ODBC API를 사용하는 애플리케이션을 개발하는 데 필요한 헤더 파일을 설치합니다. 버전 17.4.2부터 설치 관리자는 Microsoft Active Directory 인증 라이브러리(ADAL.dll)도 포함하고 설치합니다.

버전 17.6.1은 최신 GA(일반 공급) 버전입니다. 이전 버전의 Microsoft ODBC Driver 17 for SQL Server가 설치되어 있을 경우 17.6.1을 설치하면 17.6.1로 업그레이드됩니다.

**[![다운로드](../../ssms/media/download-icon.png) Microsoft ODBC Driver 17 for SQL Server 다운로드(x64)](https://go.microsoft.com/fwlink/?linkid=2137027)**  
**[![다운로드](../../ssms/media/download-icon.png) Microsoft ODBC Driver 17 for SQL Server 다운로드(x86)](https://go.microsoft.com/fwlink/?linkid=2137028)**  

### <a name="version-information"></a>버전 정보

- 릴리스 번호: 17.6.1.1
- 릴리스 날짜: 2020년 7월 31일

> [!Note]
> 영어가 아닌 언어 버전에서 이 페이지에 액세스하고 최신 콘텐츠를 보려는 경우 [영어 버전 사이트]()를 방문하세요. 영어 버전 사이트에서 [사용 가능한 언어](#available-languages)를 선택하여 다른 언어를 다운로드할 수 있습니다.

## <a name="available-languages"></a>사용 가능한 언어

이 Microsoft ODBC Driver for SQL Server 릴리스는 다음 언어로 설치할 수 있습니다.

Microsoft ODBC Driver 17.6.1 for SQL Server(x64):  
[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2137027&clcid=0x40a)

Microsoft ODBC Driver 17.6.1 for SQL Server(x86):  
[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2137028&clcid=0x40a)

### <a name="release-notes-for-windows"></a>Windows 기반 릴리스 정보

이 Windows 기반 릴리스에 대한 자세한 내용은 [Windows 릴리스 정보](windows\release-notes-odbc-sql-server-windows.md)를 참조하세요.

### <a name="previous-releases-for-windows"></a>이전 Windows 기반 릴리스

이전 Windows 기반 릴리스를 다운로드하려면 [이전 Microsoft ODBC Driver for SQL Server 릴리스](windows\release-notes-odbc-sql-server-windows.md#previous-releases)를 참조하세요.

## <a name="download-for-linux-and-macos"></a>Linux 및 macOS용 다운로드

관련 설치 지침에 따라 Linux 및 macOS용 패키지 관리자를 사용하여 Microsoft ODBC Driver for SQL Server를 다운로드하고 설치할 수 있습니다.  
[SQL Server용 ODBC 설치(Linux)](linux-mac\installing-the-microsoft-odbc-driver-for-sql-server.md)  
[SQL Server용 ODBC 설치(macOS)](linux-mac\install-microsoft-odbc-driver-sql-server-macos.md)  

오프라인 설치를 위해 패키지를 다운로드해야 하는 경우 아래 링크를 통해 모든 버전을 사용할 수 있습니다.

> [!Note]
> `msodbcsql17-*` 패키지가 최신 버전입니다. `msodbcsql-*` 패키지는 드라이버 버전 13입니다.

### <a name="alpine"></a>Alpine

- [17.6.1.1 Alpine 패키지](https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.6.1.1-1_amd64.apk)([PGP 서명](https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.6.1.1-1_amd64.sig))
- [17.5.2.2 Alpine 패키지](https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.2-1_amd64.apk)([PGP 서명](https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.2-1_amd64.sig))
- [17.5.2.1 Alpine 패키지](https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.1-1_amd64.apk)([PGP 서명](https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.2.1-1_amd64.sig))
- [17.5.1.1 Alpine 패키지](https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.1.1-1_amd64.apk)([PGP 서명](https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.1.1-1_amd64.sig))

### <a name="debian"></a>Debian

- [Debian 10 .deb 패키지](https://packages.microsoft.com/debian/10/prod/pool/main/m/msodbcsql17/)
- [Debian 9 .deb 패키지](https://packages.microsoft.com/debian/9/prod/pool/main/m/msodbcsql17/)
- [Debian 8 .deb 패키지](https://packages.microsoft.com/debian/8/prod/pool/main/m/msodbcsql17/)
- [Debian 8 .deb 패키지(msodbcsql 13.x)](https://packages.microsoft.com/debian/8/prod/pool/main/m/msodbcsql/)

### <a name="redhat"></a>RedHat

- [RedHat 8 .rpm 패키지](https://packages.microsoft.com/rhel/8/prod/)
- [RedHat 7 .rpm 패키지](https://packages.microsoft.com/rhel/7/prod/)
- [RedHat 6 .rpm 패키지](https://packages.microsoft.com/rhel/6/prod/)

### <a name="suse"></a>Suse

- [SuSE 15 .rpm 패키지](https://packages.microsoft.com/sles/15/prod/)
- [SuSE 12 .rpm 패키지](https://packages.microsoft.com/sles/12/prod/)
- [SuSE 11 .rpm 패키지](https://packages.microsoft.com/sles/11/prod/)

### <a name="ubuntu"></a>Ubuntu

- [Ubuntu 20.04 .deb 패키지](https://packages.microsoft.com/ubuntu/20.04/prod/pool/main/m/msodbcsql17/)
- [Ubuntu 18.04 .deb 패키지](https://packages.microsoft.com/ubuntu/18.04/prod/pool/main/m/msodbcsql17/)
- [Ubuntu 16.04 .deb 패키지](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql17/)
- [Ubuntu 14.04 .deb 패키지](https://packages.microsoft.com/ubuntu/14.04/prod/pool/main/m/msodbcsql17/)
- [Ubuntu 16.04 .deb 패키지(msodbcsql 13.x)](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/)
- [Ubuntu 14.04 .deb 패키지(msodbcsql 13.x)](https://packages.microsoft.com/ubuntu/14.04/prod/pool/main/m/msodbcsql/)

[Linux 드라이버 설치](linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)도 참조하시기 바랍니다.

### <a name="macos"></a>macOS

- 자세한 내용은 [Homebrew 수식](https://github.com/Microsoft/homebrew-mssql-release)을 참조하세요.

[macOS 드라이버 설치](linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)도 참조하시기 바랍니다.

### <a name="older-linux-releases"></a>이전 Linux 릴리스

- **Red Hat Enterprise Linux 5 및 6(64비트)**  - [Microsoft ODBC Driver 11 for SQL Server 다운로드 - Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321)  
- **SUSE Linux Enterprise 11 서비스 팩 2(64비트)**  - [Microsoft ODBC Driver 11 Preview for SQL Server 다운로드 - SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)

### <a name="release-notes-for-linux-and-macos"></a>Linux 및 macOS 기반 릴리스 정보

Linux 및 macOS 기반 릴리스에 대한 자세한 내용은 [Linux 및 macOS 릴리스 정보](linux-mac\release-notes-odbc-sql-server-linux-mac.md)를 참조하세요.