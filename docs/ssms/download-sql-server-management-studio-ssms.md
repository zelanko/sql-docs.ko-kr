---
title: "SSMS(SQL Server Management Studio) 다운로드 | Microsoft 문서"
ms.custom: 
ms.date: 06/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "ssms 설치, ssms 다운로드, 최신 ssms"
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
caps.latest.revision: 145
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 47182ebd082dfae0963d761e54c4045be927d627
ms.openlocfilehash: 8c43f57c6d40d3f2c29f220581dddcf74bf96287
ms.contentlocale: ko-kr
ms.lasthandoff: 07/11/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio) 다운로드
SSMS(SQL Server Management Studio)는 SQL Server에서 SQL Database까지 모든 SQL 인프라를 관리하기 위한 통합 환경입니다. SSMS는 어디에 배포하든 배포 위치에서 SQL의 인스턴스를 구성, 모니터링 및 관리하는 도구를 제공합니다. SSMS를 사용하면 응용 프로그램에 사용되는 데이터 계층 구성 요소를 배포, 모니터링 및 업그레이드하고 쿼리 및 스크립트를 작성할 수 있습니다. 

이 릴리스는 이전 버전의 SQL Server와의 향상된 호환성, 독립 실행형 웹 설치 관리자 및 새 릴리스를 사용할 수 있는 경우 SSMS 내 알림 메시지 기능을 제공합니다.  
  
![다운로드](../ssdt/media/download.png) SSMS는 무료입니다! **[SQL Server Management Studio 17.1 다운로드](https://go.microsoft.com/fwlink/?linkid=849819)** SSMS 17.X는 최신 세대의 SQL Server Management Studio이며 SQL Server 2017을 지원합니다. 

![다운로드](../ssdt/media/download.png) **[SQL Server Management Studio 17.1 업그레이드 패키지 다운로드(17.0에서 17.1로 업그레이드)](https://go.microsoft.com/fwlink/?linkid=849821)**

> [!NOTE]
> SQL Server PowerShell 모듈은 이제 PowerShell 갤러리를 통해 별도로 설치됩니다.  자세한 내용은 [다운로드 지침](download-sql-server-ps-module.md)을 참조하세요.

## <a name="sql-server-management-studio"></a>SQL Server Management Studio   
**버전 정보**  
  
릴리스 번호: 17.1  
이 릴리스에 대한 빌드 번호: 14.0.17119.0

## <a name="new-in-this-release"></a>이 릴리스의 새로운 기능  

SSMS 17.1은 SQL Server Management Studio 17.X 세대로의 첫 번째 업데이트입니다.  17.X 세대는 SQL Server 2017을 통해 SQL Server 2008의 거의 모든 기능 영역을 지원합니다.  버전 17.X는 SQL Analysis Service PaaS를 지원하는 SSMS의 세대이기도 합니다.

17.1 버전에는 다음이 포함됩니다.

* 사용자가 보고한 여러 문제에 대한 수정 사항 
* 새 Integration Services 확장 관리 도구

변경 내용의 전체 목록은   
                [SQL Server Management Studio - 변경 로그(SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md)를 참조하세요.  
   
사용자 데이터 컬렉션에 대한 정보는   
                [SQL Server 개인정보처리방침](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx)을 참조하세요. 
  
## <a name="supported-sql-offerings"></a>지원되는 SQL 서비스
  
* 이 버전의 SSMS는 [지원되는 모든 버전의 SQL Server 2008 - SQL Server 2017](https://support.microsoft.com/lifecycle?C2=1044)에서 작동하며 Azure SQL Database와 Azure SQL Data Warehouse의 최신 클라우드 기능 사용에 대해 최고 수준의 지원을 제공합니다.  
* SQL Server 2000 또는 SQL Server 2005에 대한 명시적 블록은 없지만 일부 기능이 제대로 작동하지 않을 수 있습니다.  
* 또한 SSMS 17.X는 SSMS 16.X 또는 SQL Server 2014 SSMS 및 이전 버전과 함께 설치할 수 있습니다. 
  
## <a name="supported-operating-systems"></a>지원되는 운영 체제
  
이 SSMS 릴리스는 사용 가능한 최신 서비스 팩과 함께 사용할 경우 다음과 같은 플랫폼을 지원합니다.   
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7(SP1)
- Windows Server 2016
- Windows Server 2012(64비트) 
- Windows Server 2012 R2(64비트) 
- Windows Server 2008 R2(64비트)  

>[!NOTE]
>SSMS 17.X는 Windows Server 2016 이전에 출시된 Visual Studio 2015 격리 셸을 기반으로 합니다. Microsoft는 앱 호환성을 중요하게 생각하며 이미 제공된 응용 프로그램이 최신 Windows 버전에서 계속 실행되는지 확인합니다. Windows Server 2016에서 SSMS 실행 시 발생하는 문제를 최소화하려면 SSMS에 최신 업데이트가 모두 적용되어 있는지 확인합니다. Windows Server 2016에서 SSMS와 관련된 문제가 발생하는 경우 지원 센터로 문의하세요. 지원 팀에서는 문제가 SSMS, Visual Studio 또는 Windows 호환성과 관련이 있는지 확인합니다. 그런 후 해당 문제를 추가 조사를 위해 해당 팀으로 전송합니다.

## <a name="ssms-installation-tips-and-issues"></a>SSMS 설치 팁 및 문제

>[!NOTE]
> SSMS 17.x 설치는 이전 버전의 SSMS를 업그레이드하거나 대체하지 않습니다.  SSMS 17.x은 이전 버전과 나란히 설치되므로 두 버전을 모두 사용할 수 있습니다.
> 컴퓨터에 SSMS가 병렬로 설치되어 있으면 특정 요구에 맞는 올바른 버전을 시작해야 합니다.
>  ![SSMS 17.x](media/ssms-start-menu.png)

**설치 시 다시 부팅 최소화**
- SSMS 설치 프로그램에서 설치 후 다시 부팅하도록 요구할 가능성을 줄이려면 다음 작업을 수행합니다.
  - 최신 버전의 Visual C++ 2013 재배포 가능 패키지를 실행하고 있는지 확인합니다. 버전 12.00.40649.5 이상이 필요합니다. x64 버전만 필요합니다.
  - 컴퓨터의 .NET Framework 버전이 4.6.1 이상인지 확인합니다.
  - 컴퓨터에 열려 있는 다른 Visual Studio 인스턴스를 닫습니다.
  - 컴퓨터에 최신 OS 업데이트가 모두 설치되어 있는지 확인합니다.
  - 위에 언급한 작업은 일반적으로 한 번만 수행하면 됩니다. 동일한 주 버전의 SSMS로 추가 업그레이드를 수행하는 동안 다시 부팅해야 하는 몇 가지 경우가 있습니다. 부 버전 업그레이드의 경우 SSMS에 대한 모든 필수 조건이 컴퓨터에 이미 설치되어 있습니다.

- 알려진 문제 및 해결 방법 목록을 보려면 [SQL Server Management Studio - 릴리스 정보](../ssms/sql-server-management-studio-release-notes.md)를 참조하세요.

## <a name="available-languages"></a>사용 가능한 언어  
> 영어 이외의 지역화된 SSMS 릴리스는 Windows 8, Windows 7, Windows Server 2012 및 Windows Server 2008 R2에 설치하는 경우 [KB 2862966 보안 업데이트 패키지](https://support.microsoft.com/en-us/kb/2862966) 가 필요합니다. 
  
이 SSMS 릴리스는 다음 언어로 설치할 수 있습니다.

SQL Server Management Studio 17.1:<br>
[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40a)

SQL Server Management Studio 17.1 업그레이드 패키지 다운로드(17.0에서 17.1로 업그레이드):<br>
[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=849821&clcid=0x40a)

## <a name="previous-releases"></a>이전 릴리스  
[이전 SQL Server Management Studio 릴리스](../ssms/previous-sql-server-management-studio-releases.md)  
  
## <a name="feedback"></a>피드백  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 클라이언트 도구 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Microsoft Connect에 문제 또는 제안을 기록하세요](https://connect.microsoft.com/SQLServer/Feedback)  
  
## <a name="see-also"></a>관련 항목:  
[자습서: SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[SQL Server Management Studio 설명서](https://msdn.microsoft.com/library/hh213248(v=sql.130).aspx)  
[Microsoft SQL Server](https://msdn.microsoft.com/library/bb545450.aspx)  
[추가 업데이트 및 서비스 팩](https://technet.microsoft.com/sqlserver/ff803383.aspx)  
[SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)  



