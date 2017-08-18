---
title: "SSMS(SQL Server Management Studio) 다운로드 | Microsoft 문서"
ms.custom: 
ms.date: 08/07/2017
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
ms.sourcegitcommit: 3f12671ace99d5fefc199c7b1c2db31e5b3cfade
ms.openlocfilehash: a689293fadb1a442f94d88cc06a9e7a4ef06650f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/08/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio) 다운로드

SSMS는 SQL Server에서 SQL Database까지 모든 SQL 인프라를 관리하기 위한 통합 환경입니다. SSMS는 SQL의 인스턴스를 구성, 모니터링 및 관리하는 도구를 제공합니다. SSMS를 사용하면 응용 프로그램에 사용되는 데이터 계층 구성 요소를 배포, 모니터링 및 업그레이드하고 쿼리 및 스크립트를 작성할 수 있습니다.

로컬 컴퓨터 또는 클라우드 등 어디에서나 SSMS(SQL Server Management Studio)를 사용하여 데이터베이스 및 데이터 웨어하우스를 쿼리, 디자인 및 관리할 수 있습니다.

**SSMS는 무료입니다.**

SSMS 17.X는 *SQL Server Management Studio*의 최신 세대이며 SQL Server 2017을 지원합니다.

**[![다운로드](../ssdt/media/download.png) SQL Server Management Studio 17.2 다운로드](https://go.microsoft.com/fwlink/?linkid=854085)**

**[![다운로드](../ssdt/media/download.png) SQL Server Management Studio 17.2 업그레이드 패키지 다운로드(17.x에서 17.2로 업그레이드)](https://go.microsoft.com/fwlink/?linkid=854087)**

SSMS 17.x 설치는 SSMS 16.x 이전 버전을 업그레이드 또는 대체하지 않습니다. SSMS 17.x는 이전 버전과 함께 설치되므로 두 버전을 모두 사용할 수 있습니다.
컴퓨터에 SSMS가 병렬로 설치되어 있으면 특정 요구에 맞는 올바른 버전을 시작해야 합니다. 최신 버전에는 *Microsoft SQL Server Management Studio 17* 레이블이 지정되며 새 아이콘이 추가됩니다. 
 
   ![SSMS 17.x](media/download-sql-server-management-studio-ssms/version-icons.png)


> [!NOTE]
> SQL Server PowerShell 모듈은 이제 PowerShell 갤러리를 통해 별도로 설치됩니다.  자세한 내용은 [다운로드 지침](download-sql-server-ps-module.md)을 참조하세요.

## <a name="sql-server-management-studio"></a>SQL Server Management Studio

**버전 정보**

릴리스 번호: 17.2, 이 릴리스에 대한 빌드 번호: 14.0.17177.0

## <a name="new-in-this-release"></a>이 릴리스의 새로운 기능

SSMS 17.2는 최신 버전의 SQL Server Management Studio입니다. 17.X 세대의 SSMS는 SQL Server 2017을 통해 SQL Server 2008의 거의 모든 기능 영역을 지원합니다. 버전 17.x는 SQL Analysis Service PaaS도 지원합니다.

17.2 버전에는 다음이 포함됩니다.

- MFA(Multi-Factor Authentication)
  - MFA(Multi-Factor Authentication)를 지원하는 UA(유니버설 인증)에 대한 다중 사용자 Azure AD 인증
  - 다중 사용자 인증을 지원하기 위해서 새 사용자 자격 증명 입력 필드가 MFA를 지원하는 유니버설 인증에 대해 추가되었습니다.
- 이제 연결 대화 상자는 다음 5개 인증 방법을 지원합니다.
  - Windows 인증
  - SQL Server 인증(SQL Server Authentication)
  - Active Directory - MFA 지원을 포함한 유니버설 인증
  - Active Directory - 암호
  - Active Directory - 통합

- 이제 DACFx 마법사에 대한 데이터베이스 가져오기/내보내기는 MFA를 지원하는 유니버설 인증을 사용할 수 있습니다.
- API 지원에 대해서는 [IUniversalAuthProvider 인터페이스](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)를 참조하세요.
- MFA를 지원하는 Azure AD 유니버설 인증에 사용되는 ADAL 관리 라이브러리가 버전 3.13.9로 업그레이드되었습니다.
- SQL Database 및 SQL Data Warehouse에 대한 Azure AD 관리자 설정을 지원하는 새 CLI 인터페이스.

 Active Directory 인증 방법에 대한 자세한 내용은 [SQL Database 및 SQL Data Warehouse에 대한 유니버설 인증(MFA에 대한 SSMS 지원)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) 및 [SQL Server Management Studio에 대한 Azure SQL Database 다단계 인증 구성](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure)을 참조하세요.

- 출력 창에는 개체 탐색기 노드를 확장하는 동안 실행되는 쿼리에 대한 항목이 있습니다.
- Azure SQL Database에 대해 뷰 디자이너 사용 설정
- SSMS의 개체 탐색기에서 개체를 스크립팅하기 위한 기본 스크립팅 옵션이 변경되었습니다.
  - 이전에는 생성된 스크립트의 대상을 SQL Server의 최신 버전(현재 SQL Server 2017)으로 지정하는 것이 새 설치에 대한 기본값이었습니다.
  - SSMS 17.2에서는 *스크립트 설정을 원본과 일치* 옵션이 새로 추가되었습니다. *True*로 설정하면 생성된 스크립트의 대상은 스크립팅되는 개체가 있는 서버와 동일한 버전, 엔진 유형 및 엔진 버전이 됩니다.
  - *스크립트 설정을 원본과 일치* 값은 기본적으로 *True*로 설정되므로 새 SSMS 설치의 기본값은 자동으로 항상 개체를 원본 서버와 동일한 대상으로 스크립팅이 됩니다.
  - *스크립트 설정을 원본과 일치* 값을 *False*로 설정하면 기본 스크립팅 대상 옵션이 사용하도록 설정되어 이전과 같이 작동합니다.
  - 또한 모든 스크립팅 옵션이 자체 섹션인 *버전 옵션*으로 이동하였습니다. 따라서 더 이상 *일반 스크립팅 옵션* 아래에 없습니다.

- “URL에서 복원”에서 국가 클라우드에 대한 지원 추가
- 이제 QueryStoreUI 보고서는 sys.query_store_runtime_stats에서 추가 메트릭(RowCount, DOP, CLR Time 등)을 지원합니다.
- Azure SQL Database에 IntelliSense 지원
    - https://connect.microsoft.com/SQLServer/feedback/details/3100677/ssms-2016-would-be-nice-to-have-intellisense-on-azure-sql-databases
- 보안: 연결 대화 상자가 기본적으로 Azure SQL Database 연결을 위해 신뢰하는 서버 인증서 및 요청 암호화에 연결되지 않음
- Linux에서 SQL Server에 대한 지원과 관련된 일반 개선 사항:
 - 데이터베이스 메일 노드의 재등장
 - 경로와 관련된 몇 가지 문제 해결
 - 작업 모니터 안정성 개선
 - [연결 속성] 대화 상자에 정확한 플랫폼 표시
- 성능 대시보드 서버 보고서를 기본 보고서로 제공:
  - SQL Server 2008 이상의 버전에 연결할 수 있습니다.
  - 누락된 인덱스 하위 보고서는 점수 매기기를 사용하여 가장 유용한 인덱스를 식별하는 데 도움을 줍니다.
  - 기록 대기 상태 하위 보고서는 대기 범주를 집계합니다. 유휴 및 중지 대기는 기본적으로 필터링됩니다.
  - 새 기록 래치 하위 보고서.
- 실행 계획 노드 검색을 사용하여 계획 속성을 검색할 수 있습니다. 테이블 이름과 같은 연산자 속성을 쉽게 찾을 수 있습니다. 계획을 볼 때 이 옵션을 사용하려면
  - 계획을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 [노드 찾기] 옵션을 클릭합니다.
  - CTRL+F 사용

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

SQL Server Management Studio 17.2:<br>
[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

SQL Server Management Studio 17.2 업그레이드 패키지(17.x에서 17.2로 업그레이드):<br>
[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=854087&clcid=0x40a)

## <a name="release-notes"></a>릴리스 정보

다음은 이 17.2 릴리스의 문제 및 제한 사항입니다.

- “Active Directory - MFA를 지원하는 유니버설” 인증을 사용하는 쿼리 창을 한 시간 이상 연 후 쿼리를 실행하면 다음과 유사한 오류가 발생할 수 있습니다.

   `Msg 0, Level 11, State 0, Line 0
The connection is broken and recovery is not possible. The client driver attempted to recover the connection one or more times and all attempts failed. Increase the value of *ConnectRetryCount* to increase the number of recovery attempts.`

   쿼리를 다시 실행하면 오류를 통과하고 성공하게 됩니다.

- MFA를 지원하는 유니버설 인증을 사용하는 Azure AD에는 다른 SSMS 기능이 지원되지 않습니다.
  - **새 테이블/뷰** 디자이너는 이전 스타일 로그인 프롬프트를 표시하며 Azure AD 인증을 위해 작동하지 않습니다.
  - **상위 200개의 행 편집** 기능은 Azure AD 인증을 지원하지 않습니다.
  - **등록된 서버** 구성 요소는 Azure AD 인증을 지원하지 않습니다.
  - **데이터베이스 엔진 튜닝 관리자**는 Azure AD 인증에 대해 지원되지 않습니다. 사용자에게 제공된 오류 메시지가 유용하지 않은 알려진 문제가 있습니다. *예상과는 달리 파일 또는 어셈블리 'Microsoft.IdentityModel.Clients.ActiveDirectory,...를 로드할 수 없습니다.* *데이터베이스 엔진 튜닝 관리자는 Microsoft Azure SQL Database를 지원하지 않습니다. (DTAClient)*.

**AS**

- SSAS의 개체 탐색기는 AS Azure 연결 속성에 Windows 인증 사용자 이름을 표시하지 않습니다.
자세한 내용은 [SSMS 변경 로그](sql-server-management-studio-changelog-ssms.md)를 참조하세요.

## <a name="previous-releases"></a>이전 릴리스

[이전 SQL Server Management Studio 릴리스](../ssms/sql-server-management-studio-changelog-ssms.md#previous-ssms-releases)

## <a name="feedback"></a>피드백

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 클라이언트 도구 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Microsoft Connect에 문제 또는 제안을 기록하세요](https://connect.microsoft.com/SQLServer/Feedback)

## <a name="see-also"></a>관련 항목:

- [자습서: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio 설명서](sql-server-management-studio-ssms.md)
- [추가 업데이트 및 서비스 팩](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)

