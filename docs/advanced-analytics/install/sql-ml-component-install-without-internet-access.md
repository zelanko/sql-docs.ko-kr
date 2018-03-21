---
title: "인터넷 연결 되지 않은 기계 학습 SQL Server 구성 요소 설치 | Microsoft Docs"
ms.custom: 
ms.date: 03/05/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 3f542786420eec8377dfe52ba3a1b73a24fbf524
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2018
---
# <a name="install-sql-server-machine-learning-components-without-internet-access"></a>인터넷 연결 되지 않은 구성 요소를 학습 하는 SQL Server 컴퓨터 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

기본적으로 설치 관리자가 필요한 가져오려는 Microsoft 다운로드 사이트에 연결 하 고 업데이트 된 구성 요소에 대 한 기계 학습에서 SQL Server. 방화벽 제약 때문에 이러한 사이트에서 설치 관리자를 경우, 파일을 다운로드 하 고, 오프 라인 서버에 파일을 전송 하 고, 한 다음 설치 프로그램을 실행 하는 인터넷에 연결 된 장치를 사용할 수 있습니다.

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

> [!NOTE]  
> 로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.  
 
 ###  <a name="bkmk_ga_instalpatch"></a> 패치 설치 요구 사항 

Microsoft는 SQL Server에서 필수 조건으로 설치되는 Microsoft VC++ 2013 런타임 이진 파일의 특정 버전과 관련된 문제를 확인했습니다. VC 런타임 이진 파일에 대한 이 업데이트가 없으면 SQL Server의 특정 시나리오에서 안정성 문제를 발생할 수 있습니다. SQL Server를 설치하기 전에 [SQL Server 릴리스 정보](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) 의 지침에 따라 해당 컴퓨터에 VC 런타임 이진 파일에 대한 패치가 필요한지 확인하세요.  


## <a name="download-cab-files"></a>.Cab 파일을 다운로드

인터넷에 연결 된 서버에서 오프 라인 설치에 필요한.cab 파일을 다운로드 합니다. 설치 프로그램은 추가 기능을 설치 하려면.cab 파일을 사용 합니다.

릴리스  |다운로드 링크  |
---------|---------|
**SQL Server 2017 초기 릴리스** |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python 열기     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |
**SQL Server 2017 CU1** |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
Microsoft Python 열기     |변경 없음 이전에 사용 하 여 |
Microsoft Python Server    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) |
**SQL Server 2017 CU2** |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server      |변경 없음 이전에 사용 하 여|
Microsoft Python 열기     |변경 없음 이전에 사용 하 여|
Microsoft Python Server    |변경 없음 이전에 사용 하 여|
**SQL Server 2017 CU3** |
Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
Microsoft Python 열기     |변경 없음 이전에 사용 하 여|
Microsoft Python Server    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)|
**SQL Server 2017 CU4** |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
Microsoft Python 열기     |변경 없음 이전에 사용 하 여|
Microsoft Python Server    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|

### <a name="bkmk_2016Installers"></a>SQL Server 2016에 대 한 다운로드

> [!IMPORTANT]
> 
> SQL Server 2016 SP1 CU4 또는 CU5 s p 1을 오프 라인으로 설치할 때 SRO_3.2.2.16000_1033.cab 다운로드 합니다. 에서 다운로드 한 SRO_3.2.2.13000_1033.cab FWLINK 831785 설정 대화 상자에 표시 된 대로, 하는 경우 누적 업데이트를 설치 하기 전에 파일을 SRO_3.2.2.16000_1033.cab로 바꿉니다.

릴리스  |다운로드 링크  |
---------|---------|
**SQL Server 2016 RTM**     |
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)
**SQL Server 2016 CU 1**     |
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)
**SQL Server 2016 CU 2**     |
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)
**SQL Server 2016 CU 3**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server     | 변경 없음 이전에 사용 하 여 |
**SQL Server 2016 CU 4**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU 5**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server     |변경 없음 이전에 사용 하 여|
**SQL Server 2016 CU 6**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server     |[SRS_8.0.3.14000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850316)  |
**SQL Server 2016 CU 7**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server     |변경 없음 이전에 사용 하 여 |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 CU1**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server     |변경 없음 이전에 사용 하 여|
**SQL Server 2016 SP 1 CU2**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 SP 1 CU3**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server     |변경 없음 이전에 사용 하 여|
**SQL Server 2016 SP 1 CU4 및 GDR**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP 1 CU5**     |
Microsoft R Open     |변경 없음 이전에 사용 하 여|
Microsoft R Server    |변경 없음 이전에 사용 하 여 |

Microsoft R에 대 한 소스 코드를 보고 하려는 경우 다운로드할 수 있는.tar 형식으로 보관으로: [다운로드 R 서버 설치 관리자](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

### <a name = "bkmk_OtherComponents"></a>추가 필수 구성 요소

사용자 환경에 따라 다음 필수 구성 요소에 대한 설치 관리자의 로컬 복사본을 만들어야 할 수 있습니다.

구성 요소  |버전
---------|---------
[SQL Server 2016용 Microsoft AS OLE DB 공급자](https://go.microsoft.com/fwlink/?linkid=834405)     |  13.0.1601.5
[Microsoft .NET Core](https://go.microsoft.com/fwlink/?linkid=834319)     | 1.0.1
[Microsoft MPI](https://go.microsoft.com/fwlink/?linkid=834316)     | 7.1.12437.25
[Microsoft Visual C++ 2013 재배포 가능](https://go.microsoft.com/fwlink/?linkid=799853)     | 12.0.30501.0
[Microsoft Visual C++ 2015 재배포 가능](https://go.microsoft.com/fwlink/?linkid=828641)     | 14.0.23026.0

## <a name="transfer-files"></a>파일 전송

압축 된 SQL Server 설치 미디어와 설치 프로그램을 설치 하는 컴퓨터에 이미 다운로드 파일을 전송 합니다.

와 같은 편리한 폴더 CAB 파일을 저장할 **다운로드** 또는 설치 사용자의 임시 폴더: < 사용자 이름 > C:\Users \AppData\Local\Temp 합니다.

En_sql_server_2017.iso 파일을 편리한 폴더에 넣습니다. 두 번 클릭 **setup.exe** 설치를 시작 합니다.

### <a name="run-setup"></a>설치 프로그램 실행

인터넷에서 연결이 끊어진 컴퓨터에 SQL Server 설치 프로그램을 실행 하면 설치 프로그램 추가 **오프 라인 설치** 마법사 페이지를 이전 단계에서 복사 하는.cab 파일의 위치를 지정할 수 있습니다.

1. SQL Server 설치 마법사를 시작 합니다.

2. 설치 마법사는 오픈 소스 R 또는 Python 구성 요소에 대 한 라이선스 페이지가 표시 되 면 클릭 **Accept**합니다. 라이선스 계약을 사용 하면 다음 단계를 진행할 수 있습니다.

3. 에 **오프 라인 설치** 페이지 **설치 경로**를 앞에서 복사한.cab 파일이 있는 폴더를 지정 합니다.

4. 계속 다음의 설치를 완료 하려면 화면의 지시 합니다.

설치가 완료 되는 서비스를 다시 시작 되 고 다음에 설명 된 대로 스크립트 실행을 사용 하도록 설정 하려면 서버를 구성 [설치할 SQL Server 2017 컴퓨터 학습 Services (In-database)](sql-machine-learning-services-windows-install.md) 또는 [SQL Server 설치 R Services (In-database) 2016](sql-r-services-windows-install.md)합니다.

## <a name="slipstream-upgrades-for-offline-servers"></a>오프 라인 서버에 대 한 통합 설치 업그레이드

통합 설치는 실패한 인스턴스 설치에 패치나 업데이트를 적용하여 기존 문제를 해결하는 기능을 말합니다. 이 방법은 설치를 수행할 때 동시에 SQL Server가 업데이트되므로 이후에 별도로 다시 시작할 필요가 없는 장점이 있습니다.

+ 서버가 인터넷에 연결되어 있지 않으면 SQL Server 설치 관리자를 다운로드하고 나서 업데이트 프로세스를 시작하기 **전에** R 구성 요소 설치 관리자의 일치하는 버전을 다운로드해야 합니다.  R 구성 요소는 SQL Server와 함께 기본적으로 포함 되지 않습니다.

+ 기존 설치에 이러한 구성 요소를 추가 하는 경우 SQL Server 설치 프로그램의 업데이트 된 버전 및 해당 업데이트 된 버전의 추가 구성 요소를 사용 합니다. R 기능이 설치 되도록 상태임을 지정 하면 설치 관리자 구성 요소를 학습 하는 컴퓨터에 대 한 설치 관리자의 일치 하는 버전을 찾습니다.

## <a name="get-help"></a>도움말 보기

설치 또는 업그레이드로 도움이 필요 하세요? 알려진 문제와 관련 된 일반적인 질문에 대답 하십시오에 대 한 다음 문서를 참조 합니다.

* [업그레이드 및 설치 FAQ-컴퓨터 학습 서비스](../r/upgrade-and-installation-faq-sql-server-r-services.md)

인스턴스의 설치 상태를 확인 하 고 일반적인 문제를 해결 하려면 이러한 사용자 지정 보고서를 봅니다.

* [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

R 서비스 지원 팀에서이 문서에서는 SQL Server 2016의 무인된 설치 또는 R services의 업그레이드를 수행 하는 방법을 보여 줍니다: [인터넷 액세스가 없는 컴퓨터에 R 서비스 배포](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)합니다.


## <a name="next-steps"></a>다음 단계

R 개발자 몇 가지 간단한 예제 차별화할 수 및 R SQL Server와 함께 작동 하는 방법에 대 한 기본 사항을 설명 합니다. 다음 단계에서는 다음 링크 참조:

+ [자습서: T-SQL에서 R을 실행](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R 개발자를 위한 자습서: 데이터베이스에서 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 개발자는이 자습서를 수행 하 여 SQL Server와 함께 Python을 사용 하는 방법을 배울 수 있습니다.

+ [자습서: T-SQL에서 Python 실행](../tutorials/run-python-using-t-sql.md)
+ [Python 개발자를 위한 자습서: 데이터베이스에서 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 참조 [자습서 학습 컴퓨터](../tutorials/machine-learning-services-tutorials.md)합니다.

