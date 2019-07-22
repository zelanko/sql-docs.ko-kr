---
title: SSMS(SQL Server Management Studio) 다운로드 | Microsoft 문서
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
ms.custom: ''
ms.date: 06/12/2019
ms.openlocfilehash: 0841379b0b64ebe81e4a23f76b21f6cf6abe0ec3
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265157"
---
# <a name="download-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio) 다운로드

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SSMS(SQL Server Management Studio)는 SQL Server에서 Azure SQL Database까지 모든 SQL 인프라를 관리하기 위한 통합 환경입니다. SSMS는 SQL Server 및 데이터베이스의 인스턴스를 구성, 모니터링 및 관리하는 도구를 제공합니다. SSMS를 사용하면 애플리케이션에 사용되는 데이터 계층 구성 요소를 배포, 모니터링 및 업그레이드하고 쿼리 및 스크립트를 작성할 수 있습니다.

로컬 컴퓨터 또는 클라우드 등 어디에서나 SSMS를 사용하여 데이터베이스 및 데이터 웨어하우스를 쿼리, 디자인 및 관리할 수 있습니다.

SSMS는 무료입니다.

## <a name="download-ssms-181"></a>SSMS 18.1 다운로드

**이제 SSMS 18.1을 사용할 수 있습니다. SSMS 18.1은 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]를 지원하는 *SQL Server Management Studio*의 최신 GA(일반 공급) 버전입니다!**

**[![다운로드](../ssdt/media/download.png) SQL Server Management Studio 18.1 다운로드](https://go.microsoft.com/fwlink/?linkid=2094583)**

SSMS 18.1은 SSMS의 최신 GA(일반 공급) 버전입니다. SSMS 18.0(GA)이 설치되어 있는 경우 SSMS 18.1을 설치하면 18.1로 업그레이드됩니다. SSMS 18.0의 *미리 보기* 버전이 설치된 경우에는 이것을 제거한 후에 SSMS 18.1을 설치해야 합니다.

**버전 정보**

- 릴리스 번호: 18.1<br>
- 빌드 번호: 15.0.18131.0<br>
- 릴리스 날짜: 2019년 6월 11일

의견 또는 제안 사항이 있거나 문제를 보고하려는 경우 SSMS 팀에 연락하는 가장 좋은 방법은 [UserVoice](https://aka.ms/sqlfeedback)를 사용하는 것입니다.

SSMS 18.x 설치는 SSMS 17.x 이전 버전을 업그레이드 또는 대체하지 않습니다. SSMS 18.x는 이전 버전과 함께 설치되므로 두 버전을 모두 사용할 수 있습니다.

컴퓨터에 SSMS가 병렬로 설치되어 있으면 특정 요구에 맞는 올바른 버전을 시작해야 합니다. 최신 버전에는 **Microsoft SQL Server Management Studio 18** 레이블이 지정됩니다.

## <a name="available-languages-ssms-181"></a>사용 가능한 언어(SSMS 18.1)

이 SSMS 릴리스는 다음 언어로 설치할 수 있습니다.

SQL Server Management Studio 18.1:<br>
[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40a)

> [!NOTE]
> SQL Server PowerShell 모듈은 PowerShell 갤러리를 통해 별도로 설치됩니다. 자세한 내용은 [SQL Server PowerShell 모듈 다운로드](download-sql-server-ps-module.md)를 참조하세요.

## <a name="new-in-this-release-ssms-181"></a>이 릴리스의 새로운 기능(SSMS 18.1)

- **데이터베이스 다이어그램** - 데이터베이스 다이어그램이 SSMS에 다시 추가되었습니다. 자세한 내용은 [데이터베이스 다이어그램](https://feedback.azure.com/forums/908035/suggestions/37507828)을 참조하세요.
- **SSBDIAGNOSE.EXE** - SQL Server 진단 명령줄 도구가 SSMS 패키지에 다시 추가되었습니다.
- **Integration Services(SSIS)** - Azure의 SSIS 카탈로그 또는 Azure의 파일 시스템에 있는 SSIS 패키지 일정 예약이 지원됩니다. 새 일정 대화 상자를 실행할 수 있는 항목은 세 가지입니다. *새 일정…* 메뉴 항목은 Azure의 SSIS 카탈로그에서 SSIS 패키지를 마우스 오른쪽 단추로 클릭하면 나타납니다. *Schedule SSIS Package in Azure* 메뉴 항목은 *도구* 메뉴 항목 아래 *Azure로 마이그레이션* 메뉴 항목에 있습니다. "Schedule SSIS in Azure"는 Azure SQL Database Managed Instance의 SQL Server 에이전트 아래 있는 작업 폴더를 마우스 오른쪽 단추로 클릭하면 표시됩니다.

이 릴리스의 새로운 기능에 대한 자세한 내용은 [SSMS release notes](release-notes-ssms.md)(SSMS 릴리스 정보)를 참조하세요.

## <a name="supported-sql-offerings-ssms-181"></a>지원되는 SQL 제품(SSMS 18.1)

* 이 버전의 SSMS는 [지원되는 모든 버전의 SQL Server 2008 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044)에서 작동하며 Azure SQL Database와 Azure SQL Data Warehouse의 최신 클라우드 기능 사용에 대해 최고 수준의 지원을 제공합니다.
* 또한 SSMS 18.x는 SSMS 17.x, SSMS 16.x 또는 SQL Server 2014 SSMS 및 이전 버전과 함께 설치할 수 있습니다.
* SSIS(SQL Server Integration Services) - SSMS 버전 17.x 이상은 레거시 SQL Server Integration Services 서비스에 대한 연결을 지원하지 않습니다. 이전 버전의 레거시 Integration Services에 연결하려면 SQL Server의 버전과 정렬된 SSMS 버전을 사용합니다. 예를 들어 SSMS 16.x를 사용하여 레거시 SQL Server 2016 Integration Services 서비스에 연결합니다. SSMS 17.x 및 SSMS 16.x는 동일한 컴퓨터에 나란히 설치될 수 있습니다. SQL Server 2012 설치 이후 SSIS 카탈로그 데이터베이스인 SSISDB를 사용하여 Integration Services 패키지를 저장하고, 관리하고, 실행하고, 모니터링하는 것이 좋습니다. 자세한 내용은 [SSIS 카탈로그](../integration-services/catalog/ssis-catalog.md)를 참조하세요.

## <a name="supported-operating-systems-ssms-181"></a>지원되는 운영 체제(SSMS 18.1)

이 SSMS 릴리스는 사용 가능한 최신 서비스 팩과 함께 사용할 경우 다음과 같은 64비트 플랫폼을 지원합니다.

- Windows 10(64비트) <sup>*</sup>
- Windows 8.1(64비트)
- Windows Server 2019(64비트)
- Windows Server 2016(64비트) <sup>*</sup>
- Windows Server 2012 R2(64비트)
- Windows Server 2012(64비트)
- Windows Server 2008 R2(64비트)

<sup>*</sup> 버전 1607(10.0.14393) 이상이 필요

> [!NOTE]
> SSMS는 Windows에서만 실행됩니다. Windows 이외의 플랫폼에서 실행되는 도구가 필요한 경우 Azure Data Studio를 살펴보세요. Azure Data Studio는 macOS, Linux 및 Windows를 실행하는 새로운 플랫폼 간 도구입니다. 자세한 내용은 [Azure Data Studio](../azure-data-studio/what-is.md)를 참조하세요.

## <a name="release-notes-ssms-181"></a>릴리스 정보(SSMS 18.1)

이 릴리스에는 몇 가지 [알려진 문제](release-notes-ssms.md#known-issues-181)가 있습니다.

이 릴리스에 대한 자세한 내용은 [SSMS 릴리스 정보](release-notes-ssms.md)를 참조하세요.

## <a name="previous-ssms-releases"></a>이전 SSMS 릴리스

[이전 SQL Server Management Studio 릴리스](../ssms/release-notes-ssms.md#previous-ssms-releases)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## <a name="see-also"></a>참고 항목

- [자습서: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio 설명서](sql-server-management-studio-ssms.md)
- [추가 업데이트 및 서비스 팩](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
