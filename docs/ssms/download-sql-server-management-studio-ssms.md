---
title: SSMS(SQL Server Management Studio) 다운로드 | Microsoft 문서
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: sstein, maghan
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
ms.date: 10/03/2019
ms.openlocfilehash: b3fa70eb83ddd46c0901cfe5d5499a0a12f33db8
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251396"
---
# <a name="download-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio) 다운로드

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SSMS(SQL Server Management Studio)는 SQL Server에서 Azure SQL Database까지 모든 SQL 인프라를 관리하기 위한 통합 환경입니다. SSMS는 SQL Server 및 데이터베이스의 인스턴스를 구성, 모니터링 및 관리하는 도구를 제공합니다. SSMS를 사용하면 애플리케이션에 사용되는 데이터 계층 구성 요소를 배포, 모니터링 및 업그레이드하고 쿼리 및 스크립트를 작성할 수 있습니다.

로컬 컴퓨터 또는 클라우드 등 어디에서나 SSMS를 사용하여 데이터베이스 및 데이터 웨어하우스를 쿼리, 디자인 및 관리할 수 있습니다.

SSMS는 무료입니다.

## <a name="download-ssms-1831"></a>SSMS 18.3.1 다운로드

**이제 SSMS 18.3.1을 사용할 수 있습니다. SSMS 18.3은 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]를 지원하는 *SQL Server Management Studio*의 최신 GA(일반 공급) 버전입니다!**

**[SQL Server Management Studio 18.3.1 다운로드](https://go.microsoft.com/fwlink/?linkid=2105412)**

SSMS 18.3.1은 SSMS의 최신 GA(일반 공급) 버전입니다. 이전 GA 버전의 SSMS 18이 설치되어 있는 경우 SSMS 18.3.1을 설치하면 18.3.1로 업그레이드됩니다. SSMS 18.x의 이전 *미리 보기* 버전이 설치된 경우 SSMS 18.3.1을 설치하기 전에 제거해야 합니다.

**버전 정보**

- 릴리스 번호: 18.3.1  
- 빌드 번호: 15.0.18183.0  
- 릴리스 날짜: 2019년 10월 2일  

의견 또는 제안 사항이 있거나 문제를 보고하려는 경우 SSMS 팀에 연락하는 가장 좋은 방법은 [UserVoice](https://aka.ms/sqlfeedback)를 사용하는 것입니다.

SSMS 18.x 설치는 SSMS 17.x 이전 버전을 업그레이드 또는 대체하지 않습니다. SSMS 18.x는 이전 버전과 함께 설치되므로 두 버전을 모두 사용할 수 있습니다.

컴퓨터에 SSMS가 병렬로 설치되어 있으면 특정 요구에 맞는 올바른 버전을 시작해야 합니다. 최신 버전에는 **Microsoft SQL Server Management Studio 18** 레이블이 지정됩니다.

## <a name="available-languages-ssms-1831"></a>사용 가능한 언어(SSMS 18.3.1)

이 SSMS 릴리스는 다음 언어로 설치할 수 있습니다.

SQL Server Management Studio 18.3.1:  
[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2105412&clcid=0x40a)

> [!NOTE]
> SQL Server PowerShell 모듈은 PowerShell 갤러리를 통해 별도로 설치됩니다. 자세한 내용은 [SQL Server PowerShell 모듈 다운로드](download-sql-server-ps-module.md)를 참조하세요.

## <a name="new-in-this-release-ssms-1831"></a>이 릴리스의 새로운 기능(SSMS 18.3.1)

| 새 항목 | 세부 정보 |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 데이터 분류 | 데이터 분류 정보를 열 속성 UI에 추가했습니다(*정보 유형*, *정보 유형 ID*, *민감도 레이블* 및 *민감도 레이블 ID*는 SSMS UI에 노출되지 않음). |
| Intellisense/편집기 | 최근 SQL Server 2019에 추가된 기능에 대한 지원이 업데이트되었습니다(예: "ALTER SERVER CONFIGURATION"). |
| Integration Services | ADF 파이프라인에서 SSIS 패키지 실행 작업으로 Azure-SSIS Integration Runtime에서 SSIS 패키지 실행을 호출하는 새 선택 메뉴 항목 `Tools > Migrate to Azure > Configure Azure-enabled DTExec`이 추가되었습니다. |
| SMO/스크립팅 | Azure SQL DW UNIQUE 제약 조건의 스크립팅 지원에 대한 지원이 추가되었습니다. |
| SMO/스크립팅 | 데이터 분류 - SQL 버전 10(SQL 2008) 이상에 대한 지원이 추가되었습니다.  - SQL 버전 15(SQL 2019) 이상 및 Azure SQL DB에 대한 새 민감도 특성 '순위'가 추가되었습니다. |

이 릴리스의 새로운 기능에 대한 자세한 내용은 [SSMS release notes](release-notes-ssms.md)(SSMS 릴리스 정보)를 참조하세요.

## <a name="supported-sql-offerings-ssms-1831"></a>지원되는 SQL 제품(SSMS 18.3.1)

- 이 버전의 SSMS는 [지원되는 모든 버전의 SQL Server 2008 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044)에서 작동하며 Azure SQL Database와 Azure SQL Data Warehouse의 최신 클라우드 기능 사용에 대해 최고 수준의 지원을 제공합니다.
- 또한 SSMS 18.x는 SSMS 17.x, SSMS 16.x 또는 SQL Server 2014 SSMS 및 이전 버전과 함께 설치할 수 있습니다.
- SSIS(SQL Server Integration Services) - SSMS 버전 17.x 이상은 레거시 SQL Server Integration Services 서비스에 대한 연결을 지원하지 않습니다. 이전 버전의 레거시 Integration Services에 연결하려면 SQL Server의 버전과 정렬된 SSMS 버전을 사용합니다. 예를 들어 SSMS 16.x를 사용하여 레거시 SQL Server 2016 Integration Services 서비스에 연결합니다. SSMS 17.x 및 SSMS 16.x는 동일한 컴퓨터에 나란히 설치될 수 있습니다. SQL Server 2012 설치 이후 SSIS 카탈로그 데이터베이스인 SSISDB를 사용하여 Integration Services 패키지를 저장하고, 관리하고, 실행하고, 모니터링하는 것이 좋습니다. 자세한 내용은 [SSIS 카탈로그](../integration-services/catalog/ssis-catalog.md)를 참조하세요.

## <a name="supported-operating-systems-ssms-1831"></a>지원되는 운영 체제(SSMS 18.3.1)

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

## <a name="release-notes-ssms-1831"></a>릴리스 정보(SSMS 18.3.1)

이 릴리스에는 몇 가지 [알려진 문제](release-notes-ssms.md#known-issues-1831)가 있습니다.

이 릴리스에 대한 자세한 내용은 [SSMS 릴리스 정보](release-notes-ssms.md)를 참조하세요.

## <a name="previous-ssms-releases"></a>이전 SSMS 릴리스

[이전 SQL Server Management Studio 릴리스](../ssms/release-notes-ssms.md#previous-ssms-releases)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## <a name="see-also"></a>관련 항목:

- [자습서: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio 설명서](sql-server-management-studio-ssms.md)
- [추가 업데이트 및 서비스 팩](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
