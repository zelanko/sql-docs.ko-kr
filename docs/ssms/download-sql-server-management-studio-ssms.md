---
title: "SSMS(SQL Server Management Studio) 다운로드 | Microsoft 문서"
ms.custom: 
ms.date: 10/09/2017
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
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: be3d22491e1cf5e6446f9ac597d613e1d203a28e
ms.contentlocale: ko-kr
ms.lasthandoff: 10/10/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio) 다운로드

SSMS는 SQL Server에서 SQL Database까지 모든 SQL 인프라를 관리하기 위한 통합 환경입니다. SSMS는 SQL의 인스턴스를 구성, 모니터링 및 관리하는 도구를 제공합니다. SSMS를 사용하면 응용 프로그램에 사용되는 데이터 계층 구성 요소를 배포, 모니터링 및 업그레이드하고 쿼리 및 스크립트를 작성할 수 있습니다.

로컬 컴퓨터 또는 클라우드 등 어디에서나 SSMS(SQL Server Management Studio)를 사용하여 데이터베이스 및 데이터 웨어하우스를 쿼리, 디자인 및 관리할 수 있습니다.

**SSMS는 무료입니다.**

SSMS 17.X는 *SQL Server Management Studio*의 최신 세대이며 SQL Server 2017을 지원합니다.

**[![다운로드](../ssdt/media/download.png) SQL Server Management Studio 17.3 다운로드](https://go.microsoft.com/fwlink/?linkid=858904)**

**[![다운로드](../ssdt/media/download.png) SQL Server Management Studio 17.3 업그레이드 패키지 다운로드(17.x에서 17.3으로 업그레이드)](https://go.microsoft.com/fwlink/?linkid=858906)**

SSMS 17.x 설치는 SSMS 16.x 이전 버전을 업그레이드 또는 대체하지 않습니다. SSMS 17.x는 이전 버전과 함께 설치되므로 두 버전을 모두 사용할 수 있습니다.
컴퓨터에 SSMS가 병렬로 설치되어 있으면 특정 요구에 맞는 올바른 버전을 시작해야 합니다. 최신 버전에는 *Microsoft SQL Server Management Studio 17* 레이블이 지정되며 새 아이콘이 추가됩니다. 
 
   ![SSMS 17.x](media/download-sql-server-management-studio-ssms/version-icons.png)


> [!NOTE]
> SQL Server PowerShell 모듈은 이제 PowerShell 갤러리를 통해 별도로 설치됩니다.  자세한 내용은 [다운로드 지침](download-sql-server-ps-module.md)을 참조하세요.

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

**버전 정보**

릴리스 번호: 17.3

이 릴리스에 대한 빌드 번호: 14.0.17199.0

## <a name="new-in-this-release"></a>이 릴리스의 새로운 기능

SSMS 17.3은 최신 버전의 SQL Server Management Studio입니다. 17.X 세대의 SSMS는 SQL Server 2017을 통해 SQL Server 2008의 거의 모든 기능 영역을 지원합니다. 버전 17.x는 SQL Analysis Service PaaS도 지원합니다.

17.3 버전에는 다음이 포함됩니다.

- 최소한의 사용자 간섭 또는 특수화된 도메인 지식을 요구하는 지능형 프레임워크로 CSV 파일의 가져오기 작업을 단순화하기 위해 새 "플랫 파일 가져오기" 마법사가 추가되었습니다. 자세한 내용은 [SQL 마법사로 플랫 파일 가져오기](../relational-databases/import-export/import-flat-file-wizard.md)를 참조하세요.
- 개체 탐색기에 "XEvent Profiler" 노드가 추가되었습니다. 자세한 내용은 [SSMS XEvent Profiler 사용](../relational-databases/extended-events/use-the-ssms-xe-profiler.md)을 참조하세요.
- 성능 대시보드 기록 대기 작업 보고서에 대기 작업 필터링 및 분류가 업데이트되었습니다.
- "Predict" 함수의 구문 검사가 추가되었습니다.
- 외부 라이브러리 관리 쿼리의 구문 검사가 추가되었습니다.
- 외부 라이브러리 관리에 대한 SMO 지원이 추가되었습니다.
- "등록된 서버" 창에 "PowerShell 시작" 지원이 추가되었습니다(새 SQL PowerShell 모듈 필요).
- Always On: 가용성 그룹에 대한 [읽기 전용 라우팅 지원](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)이 추가되었습니다.
- "Active Directory - MFA 지원을 포함한 유니버설 인증" 로그인에 대한 출력 창에 상세 내용 추적을 전송하는 옵션이 추가되었습니다(기본적으로 꺼짐. "도구 > 옵션 > Azure 서비스 > Azure 클라우드 > ADAL 출력 창 추적 수준" 아래의 사용자 설정에서 켜야 함). 
- 쿼리 저장소: 
  - 쿼리 저장소 UI는 QDS가 모든 데이터를 기록하는 한 QDS가 OFF인 경우에도 액세스할 수 있습니다.
  - 이제 쿼리 저장소 UI는 모든 기존 보고서의 대기 분류를 노출합니다. 이를 통해 고객은 상위 대기 중인 쿼리 등의 시나리오를 잠금 해제할 수 있습니다.
- 스크립팅 매개 변수 헤더 옵션을 포함했습니다(기본적으로 꺼짐. "도구 > 옵션 > SQL Server 개체 탐색기 > 스크립팅 > 스크립팅 매개 변수 헤더 포함" 아래의 사용자 설정에서 활성화될 수 있음). - [연결 항목 3139199](https://connect.microsoft.com/SQLServer/feedback/details/3139199)
- "RC" 브랜딩이 제거되었습니다.

전체 변경 내용 목록을 보려면 [SQL Server Management Studio - 변경 로그(SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md)를 참조하세요.

사용자 데이터 수집에 대한 자세한 내용은 [SQL Server 개인 정보 취급 방침](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx)을 참조하세요.

## <a name="supported-sql-offerings"></a>지원되는 SQL 서비스

* 이 버전의 SSMS는 [지원되는 모든 버전의 SQL Server 2008 - SQL Server 2017](https://support.microsoft.com/lifecycle?C2=1044)에서 작동하며 Azure SQL Database와 Azure SQL Data Warehouse의 최신 클라우드 기능 사용에 대해 최고 수준의 지원을 제공합니다.
* SQL Server 2000 또는 SQL Server 2005에 대한 명시적 블록은 없지만 일부 기능이 제대로 작동하지 않을 수 있습니다.
* 또한 SSMS 17.x는 SSMS 16.x 또는 SQL Server 2014 SSMS 및 이전 버전과 함께 설치할 수 있습니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제
  
이 SSMS 릴리스는 사용 가능한 최신 서비스 팩과 함께 사용할 경우 다음과 같은 64비트 플랫폼을 지원합니다.
- Windows 10(64비트)
- Windows 8.1(64비트)
- Windows 8(64비트)
- Windows 7(SP1)(64비트)
- Windows Server 2016 *
- Windows Server 2012 R2(64비트)
- Windows Server 2012(64비트)
- Windows Server 2008 R2(64비트)

\* SSMS 17.X는 Windows Server 2016 이전에 출시된 Visual Studio 2015 격리 셸을 기반으로 합니다. Microsoft는 앱 호환성을 중요하게 생각하며 이미 제공된 응용 프로그램이 최신 Windows 버전에서 계속 실행되는지 확인합니다. Windows Server 2016에서 SSMS 실행 시 발생하는 문제를 최소화하려면 SSMS에 최신 업데이트가 모두 적용되어 있는지 확인합니다. Windows Server 2016에서 SSMS와 관련된 문제가 발생하는 경우 지원 센터로 문의하세요. 지원 팀에서는 문제가 SSMS, Visual Studio 또는 Windows 호환성과 관련이 있는지 확인합니다. 그런 후 해당 문제를 추가 조사를 위해 해당 팀으로 전송합니다.

## <a name="ssms-installation-tips-and-issues"></a>SSMS 설치 팁 및 문제

### <a name="minimize-installation-reboots"></a>설치 시 다시 부팅 최소화

* SSMS 설치 프로그램에서 설치 후 다시 부팅하도록 요구할 가능성을 줄이려면 다음 작업을 수행합니다.
  * 최신 버전의 Visual C++ 2013 재배포 가능 패키지를 실행하고 있는지 확인합니다. 버전 12.00.40649.5 이상이 필요합니다. x64 버전만 필요합니다.
  * 컴퓨터의 .NET Framework 버전이 4.6.1 이상인지 확인합니다.
  * 컴퓨터에 열려 있는 다른 Visual Studio 인스턴스를 닫습니다.
  * 컴퓨터에 최신 OS 업데이트가 모두 설치되어 있는지 확인합니다.
  * 위에 언급한 작업은 일반적으로 한 번만 수행하면 됩니다. 동일한 주 버전의 SSMS로 추가 업그레이드를 수행하는 동안 다시 부팅해야 하는 몇 가지 경우가 있습니다. 부 버전 업그레이드의 경우 SSMS에 대한 모든 필수 조건이 컴퓨터에 이미 설치되어 있습니다.

* 알려진 문제 및 해결 방법 목록을 보려면 [SQL Server Management Studio - 릴리스 정보](../ssms/sql-server-management-studio-release-notes.md)를 참조하세요.

## <a name="available-languages"></a>사용 가능한 언어

> [!NOTE]
> 영어 이외의 지역화된 SSMS 릴리스는 Windows 8, Windows 7, Windows Server 2012 및 Windows Server 2008 R2에 설치하는 경우 [KB 2862966 보안 업데이트 패키지](https://support.microsoft.com/en-us/kb/2862966) 가 필요합니다.

이 SSMS 릴리스는 다음 언어로 설치할 수 있습니다.

SQL Server Management Studio 17.3:<br>
[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)

SQL Server Management Studio 17.3 업그레이드 패키지(17.x에서 17.3으로 업그레이드):<br>
[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=858906&clcid=0x40a)

## <a name="release-notes"></a>릴리스 정보

다음은 이 17.3 릴리스의 문제 및 제한 사항입니다.

**일반 SSMS**

- MFA를 지원하는 UA를 사용하는 Azure AD 인증에는 다른 SSMS 기능이 지원되지 않습니다.
   - 데이터베이스 엔진 튜닝 관리자는 Azure AD 인증에 지원되지 않습니다. 사용자에게 제공된 오류 메시지가 유용하지 않은 알려진 문제가 있습니다. "예상과는 달리 파일 또는 어셈블리 'Microsoft.IdentityModel.Clients.ActiveDirectory,...를 로드할 수 없습니다." "데이터베이스 엔진 튜닝 관리자는 Microsoft Azure SQL Database를 지원하지 않습니다(DTAClient)". (DTAClient)".
- 오류의 DTA 결과에서 쿼리 분석 시도: "개체는 IConvertible을 구현해야 합니다(mscorlib)". (mscorlib)".
- *재발된 쿼리*가 개체 탐색기에서 보고서의 쿼리 저장소 목록에서 누락되었습니다.
   - 해결 방법: 마우스 오른쪽 단추로 **쿼리 저장소** 노드를 클릭하고 **재발된 쿼리 보기**를 선택합니다.

**IS(Integration Services)**

- [catalog].[event_messagea]에서 [execution_path]가 Scale Out에서 패키지 실행에 대해 올바르지 않습니다. [execution_path]는 패키지 실행 파일의 개체 이름 대신 "\Package"로 시작합니다. SSMS에서 패키지 실행의 개요 보고서를 볼 때 실행 개요에서 "실행 경로"의 링크는 작동하지 않습니다. 해결 방법은 개요 보고서에서 "메시지 보기"를 클릭하여 모든 이벤트 메시지를 확인하는 것입니다.



## <a name="previous-releases"></a>이전 릴리스

[이전 SQL Server Management Studio 릴리스](../ssms/sql-server-management-studio-changelog-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>피드백

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 클라이언트 도구 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Microsoft Connect에 문제 또는 제안을 기록하세요](https://connect.microsoft.com/SQLServer/Feedback)

## <a name="see-also"></a>관련 항목:

- [자습서: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio 설명서](sql-server-management-studio-ssms.md)
- [추가 업데이트 및 서비스 팩](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)

