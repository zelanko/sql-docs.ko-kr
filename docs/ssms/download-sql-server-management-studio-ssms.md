---
title: SSMS(SQL Server Management Studio) 다운로드 | Microsoft 문서
ms.custom: ''
ms.date: 03/29/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
ms.technology: ssms
ms.topic: conceptual
keywords:
- ssms 설치, ssms 다운로드, 최신 ssms
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- sql management studio install
- download sql management studio
- ms sql management studio
- install sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
author: dnethi
ms.author: dinethi
manager: craigg
ms.openlocfilehash: 9bc678f69df60ec07e1cca6eddbb337aab8ed8ff
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59042030"
---
# <a name="download-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio) 다운로드
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SSMS(SQL Server Management Studio)는 SQL Server에서 Azure SQL Database까지 모든 SQL 인프라를 관리하기 위한 통합 환경입니다. SSMS는 SQL Server 및 데이터베이스의 인스턴스를 구성, 모니터링 및 관리하는 도구를 제공합니다. SSMS를 사용하면 애플리케이션에 사용되는 데이터 계층 구성 요소를 배포, 모니터링 및 업그레이드하고 쿼리 및 스크립트를 작성할 수 있습니다.

로컬 컴퓨터 또는 클라우드 등 어디에서나 SSMS를 사용하여 데이터베이스 및 데이터 웨어하우스를 쿼리, 디자인 및 관리할 수 있습니다.

SSMS는 무료입니다.

[SSMS 18.0 RC1(릴리스 후보 1)은 현재 사용할 수 있으며](#ssms-180-rc1), [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]를 지원하는 최신 세대 *SQL Server Management Studio*입니다.

## <a name="ssms-1791-is-the-current-general-availability-ga-version-of-ssms"></a>SSMS 17.9.1은 SSMS의 현재 GA(일반 공급) 버전입니다.

[![다운로드](../ssdt/media/download.png) SQL Server Management Studio 17.9.1 다운로드](https://go.microsoft.com/fwlink/?linkid=2043154)

[![다운로드](../ssdt/media/download.png) SQL Server Management Studio 17.9.1 업그레이드 패키지 다운로드(17.x에서 17.9.1로 업그레이드)](https://go.microsoft.com/fwlink/?linkid=2043430)

**버전 정보**

- 릴리스 번호: 17.9.1<br>
- 빌드 번호: 14.0.17289.0<br>
- 릴리스 날짜: 2018년 11월 21일

### <a name="available-languages-ssms-1791"></a>사용 가능한 언어(SSMS 17.9.1)

> [!NOTE]
> 영어 이외의 지역화된 SSMS 17.x 릴리스를 다음 위치에 설치하는 경우 [KB 2862966 보안 업데이트 패키지](https://support.microsoft.com/kb/2862966)가 필요합니다. Windows 8, Windows 7, Windows Server 2012 및 Windows Server 2008 R2.

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40a)

SSMS 17.9.1에 대한 자세한 내용은 [SSMS 17.9.1 변경 로그](release-notes-ssms.md#1791-latest-ga-release)를 참조하세요.

## <a name="ssms-installation-tips-and-issues-ssms-1791"></a>SSMS 설치 팁 및 문제(SSMS 17.9.1)

### <a name="minimize-installation-reboots"></a>설치 시 다시 부팅 최소화

* SSMS 설치 프로그램에서 설치 후 다시 부팅하도록 요구할 가능성을 줄이려면 다음 작업을 수행합니다.
  * 최신 버전의 Visual C++ 2013 재배포 가능 패키지를 실행하고 있는지 확인합니다. 버전 12.0.40649.5 이상이 필요합니다. x64 버전만 필요합니다.
  * 컴퓨터의 .NET Framework 버전이 4.6.1 이상인지 확인합니다.
  * 컴퓨터에서 열려 있는 Visual Studio의 모든 인스턴스를 닫습니다.
  * 컴퓨터에 최신 OS 업데이트가 모두 설치되어 있는지 확인합니다.
  * 위에 언급한 작업은 일반적으로 한 번만 수행하면 됩니다. 동일한 주 버전의 SSMS로 추가 업그레이드를 수행하는 동안 다시 부팅해야 하는 몇 가지 경우가 있습니다. 부 버전 업그레이드의 경우 SSMS에 대한 모든 필수 구성 요소가 컴퓨터에 이미 설치되어 있습니다.

## <a name="ssms-180-rc1"></a>SSMS 18.0(RC1)

**SSMS 18.0 RC1(릴리스 후보 1)은 현재 사용할 수 있으며, [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]!** 를 지원하는 최신 세대 *SQL Server Management Studio*입니다.

**[![다운로드](../ssdt/media/download.png) SQL Server Management Studio 18.0(RC1) 다운로드](https://go.microsoft.com/fwlink/?linkid=2085742)**

*RC1*은 SSMS 18.0의 최신 공개 미리 보기입니다. 이전 SSMS 18.0 미리 보기가 설치되어 있으면 먼저 이를 제거한 후에 SSMS 18.0 RC1을 설치합니다.

**버전 정보**

- 릴리스 번호: 18.0(RC1)<br>
- 빌드 번호: 15.0.18098.0<br>
- 릴리스 날짜: 2019년 3월 28일

의견 또는 제안 사항이 있거나 문제를 보고하려는 경우 SSMS 팀에 연락하는 가장 좋은 방법은 [UserVoice](https://aka.ms/sqlfeedback)를 사용하는 것입니다.

SSMS 18.x 설치는 SSMS 17.x 이전 버전을 업그레이드 또는 대체하지 않습니다. SSMS 18.x는 이전 버전과 함께 설치되므로 두 버전을 모두 사용할 수 있습니다.

컴퓨터에 SSMS가 병렬로 설치되어 있으면 특정 요구에 맞는 올바른 버전을 시작해야 합니다. 최신 버전에는 **Microsoft SQL Server Management Studio 18** 레이블이 지정됩니다.
 
## <a name="available-languages-ssms-180-rc1"></a>사용 가능한 언어(SSMS 18.0 RC1)

이 SSMS 릴리스는 다음 언어로 설치할 수 있습니다.

SQL Server Management Studio 18.0 (RC1):<br>
[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2085742&clcid=0x40a)

SQL Server Management Studio 18.0 업그레이드 패키지 다운로드(18.0으로 업그레이드):<br>
지금은 업그레이드 옵션을 사용할 수 없습니다. 이전 SSMS 18.0 미리 보기가 설치되어 있으면 먼저 이를 제거한 후에 SSMS 18.0 RC1을 설치합니다.

> [!NOTE]
> SQL Server PowerShell 모듈은 PowerShell 갤러리를 통해 별도로 설치됩니다. 자세한 내용은 [SQL Server PowerShell 모듈 다운로드](download-sql-server-ps-module.md)를 참조하세요.

## <a name="new-in-this-release-ssms-180-rc1"></a>이 릴리스의 새로운 기능(SSMS 18.0 RC1)

SSMS 18.0(RC1)은 최신 버전의 SQL Server Management Studio입니다. 18.X 세대의 SSMS는 SQL Server 2019 미리 보기를 통해 SQL Server 2008의 거의 모든 기능 영역을 지원합니다.

이 릴리스의 새로운 기능에 대한 자세한 내용은 [SSMS release notes](release-notes-ssms.md)(SSMS 릴리스 정보)를 참조하세요.

## <a name="supported-sql-offerings-ssms-180-rc1"></a>지원되는 SQL 제품(SSMS 18.0 RC1)

* 이 버전의 SSMS는 [지원되는 모든 버전의 SQL Server 2008 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044)에서 작동하며 Azure SQL Database와 Azure SQL Data Warehouse의 최신 클라우드 기능 사용에 대해 최고 수준의 지원을 제공합니다.
* 또한 SSMS 18.x는 SSMS 17.x, SSMS 16.x 또는 SQL Server 2014 SSMS 및 이전 버전과 함께 설치할 수 있습니다.
* SSIS(SQL Server Integration Services) - SSMS 버전 17.x 이상은 레거시 SQL Server Integration Services 서비스에 대한 연결을 지원하지 않습니다. 이전 버전의 레거시 Integration Services에 연결하려면 SQL Server의 버전과 정렬된 SSMS 버전을 사용합니다. 예를 들어 SSMS 16.x를 사용하여 레거시 SQL Server 2016 Integration Services 서비스에 연결합니다. SSMS 17.x 및 SSMS 16.x는 동일한 컴퓨터에 나란히 설치될 수 있습니다. SQL Server 2012 설치 이후 SSIS 카탈로그 데이터베이스인 SSISDB를 사용하여 Integration Services 패키지를 저장하고, 관리하고, 실행하고, 모니터링하는 것이 좋습니다. 자세한 내용은 [SSIS 카탈로그](../integration-services/catalog/ssis-catalog.md)를 참조하세요.

## <a name="supported-operating-systems-ssms-180-rc1"></a>지원되는 운영 체제(SSMS 18.0 RC1)

이 SSMS 릴리스는 사용 가능한 최신 서비스 팩과 함께 사용할 경우 다음과 같은 64비트 플랫폼을 지원합니다.

- Windows 10(64비트) <sup>*</sup>
- Windows Server 2016 <sup>*</sup>
- Windows Server 2012 R2(64비트)
- Windows Server 2012(64비트)
- Windows Server 2008 R2(64비트)

<sup>*</sup> 버전 1607(10.0.14939) 이상이 필요

> [!NOTE]
> SSMS는 Windows에서만 실행됩니다. Windows 이외의 플랫폼에서 실행되는 도구가 필요한 경우 Azure Data Studio를 살펴보세요. Azure Data Studio는 macOS, Linux 및 Windows를 실행하는 새로운 플랫폼 간 도구입니다. 자세한 내용은 [Azure Data Studio](../azure-data-studio/what-is.md)를 참조하세요.
  
## <a name="release-notes-ssms-180-rc1"></a>릴리스 정보(SSMS 18.0 RC1)

해당 사항 없음

## <a name="previous-releases"></a>이전 릴리스

[이전 SQL Server Management Studio 릴리스](../ssms/release-notes-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>피드백

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 클라이언트 도구 포럼](https://social.msdn.microsoft.com/Forums/home?forum=sqltools)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="see-also"></a>참고 항목

- [자습서: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio 설명서](sql-server-management-studio-ssms.md)
- [추가 업데이트 및 서비스 팩](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

의견 또는 제안 사항이 있거나 문제를 보고하려는 경우 SSMS 팀에 연락하는 가장 좋은 방법은 [UserVoice](https://aka.ms/sqlfeedback)를 사용하는 것입니다.
