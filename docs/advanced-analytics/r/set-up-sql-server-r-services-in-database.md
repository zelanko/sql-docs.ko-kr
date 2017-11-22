---
title: "SQL Server 컴퓨터 학습 Services (In-database) 설치 | Microsoft Docs"
ms.custom: 
ms.date: 11/15/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "SQL Server R Services 설치"
- "SQL Server 컴퓨터 학습 Services 설치"
- "R 서비스 설정"
- "SQL 기계 학습 설치"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: "36"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 3a32560422e8fc5f1a2e4284702d2cb28562f01f
ms.sourcegitcommit: 06bb91d138a4d6395c7603a2d8f99c69a20642d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/16/2017
---
# <a name="set-up-sql-server-machine-learning-services-in-database"></a>SQL Server 컴퓨터 학습 Services (In-database) 설치

이 항목에는 설치 하 고 SQL Server의 데이터베이스에서 분석을 지 원하는 기능을 학습 한 다음 컴퓨터를 구성 하는 방법을 설명 합니다.

+ **SQL Server 2016 R Services (In-database)**합니다. SQL Server 2016를 설정한 경우 SQL Server에서 R 코드의 실행을 활성화 하려면이 기능을 설치 합니다. 데이터베이스 엔진에 필요합니다.

    [SQL Server 2016의 기계 학습 설정](#bkmk_2016top)

+ **SQL Server 2017 컴퓨터 학습 Services (In-database)**합니다. SQL Server 2017를 설정한 경우 SQL Server에서 R (또는 Python) 코드를 실행 하려면이 설치 합니다. 데이터베이스 엔진에 필요합니다. 

    [SQL Server 2017에 기계 학습 설정](#bkmk_2017top)

+ 사용 하 여 컴퓨터 학습 서버 **없는** SQL Server

    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설정에는 컴퓨터의 구성 요소를 학습 데이터베이스 엔진에 필요 하지 않으며 SQL Server에서는 실행 되지 않습니다 "독립 실행형" 버전을 설치 하는 옵션이 포함 됩니다.  일반적으로 SQL Server를 호스트 하는 컴퓨터와 다른 컴퓨터에이 옵션을 설치 하는 것이 좋습니다.
    
    [기계 학습 독립 실행형 서버를 설정](create-a-standalone-r-server.md)합니다.

사용 하는 설치 과정을 설명 하는이 문서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 마법사입니다. 명령줄 설치에 대 한 또는 오프 라인 서버에서 사용 하려면 설치 관리자를 다운로드 하려면 다음이 문서를 참조 합니다.

+ [명령줄에서 R for SQL Server 설치](unattended-installs-of-sql-server-r-services.md)
+ [명령줄에서 SQL Server에 대 한 Python을 설치](../python/unattended-installs-of-sql-server-python-services.md)
+ [명령줄에서 독립 실행형 컴퓨터 학습 서버를 설치 합니다.](install-microsoft-r-server-from-the-command-line.md)
+ [없는 인터넷 ace 사용 하 여 서버에 컴퓨터 학습 구성 요소 설치](installing-ml-components-without-internet-access.md)

**적용 대상:** SQL Server 2016, SQL Server 2017

## <a name="bkmk_prereqs"></a> 사전 설치 검사 목록

+ 데이터베이스에서 시스템 학습에는 SQL Server 2016 이상 필요합니다. 

+ 지원 되는 언어: 

    + SQL Server 2016 R을만 지원합니다. 

    + R도 몇 가지 제한 사항이 Azure SQL 데이터베이스에서 미리 보기 기능으로 제공 됩니다. 자세한 내용은 참조 [Azure SQL 데이터베이스에서 사용 하 여 R](using-r-in-azure-sql-database.md)

    + Python을 사용 하려면 SQL Server 2017 이상이 필요 합니다.

+ 모든 이전 버전의 Revolution Analytics 개발 환경 또는 RevoScaleR 패키지를 사용 하는 경우 또는 SQL Server 2016의 시험판 버전을 설치한 경우 제거 해야 있습니다. -병렬 설치에 지원 되지 않습니다. 이전 버전을 제거 하는 도움말을 참조 하십시오. [업그레이드 및 SQL Server 컴퓨터 학습 서비스에 대 한 설치 FAQ](../r/upgrade-and-installation-faq-sql-server-r-services.md)합니다.

+ 도메인 컨트롤러에 SQL Server 2016 R Services 또는 SQL Server 2017 컴퓨터 학습 서비스를 설치할 수 없습니다. 설치 프로그램의 R 서비스 또는 컴퓨터 학습 서비스 부분 실패 합니다.

+ 장애 조치 클러스터에 기능을 학습 하는 컴퓨터를 설치할 수 없습니다. 외부 스크립트 프로세스를 격리 하기 위해 사용 되는 보안 메커니즘 Windows Server 장애 조치 클러스터 환경와 호환 되지 않습니다. 이 문제를 해결 다음 중 하나를 수행할 수 있습니다.
    * 복제를 사용 하 여 기계 학습 사용 하도록 설정 된 SQL Server 인스턴스에 필요한 테이블을 복사 합니다.
    * 기계 학습 AlwaysOn을 사용 하 고 가용성 그룹의 일부는 독립 실행형 컴퓨터에 설치 합니다.

+ 기계 학습 프레임 워크는 설치가 완료 된 후 추가 구성이 필요 합니다. 정확한 단계는 조직 및 보안 정책, 서버 구성 및 사용자가에 따라 달라 집니다. 모든 단계를 검토 하 고 사용자 환경의 추가 구성이 필요할 수 있는 결정 하는 것이 좋습니다.

## <a name="bkmk2016top"></a>SQL Server 2016 R Services (In-database) 설치

> [!div class="checklist"]
> * 데이터베이스 엔진 및 기계 학습 기능 설치
> * 설치 후 단계를 필요한: 기계 학습을 사용 하도록 설정 하 고 다시 시작
> * 선택적 사후 설치 단계: 방화벽 규칙을 추가, 사용자를 추가, 변경 또는 서비스 계정 구성 원격 데이터 과학 클라이언트 설정

**SQL Server 2016 설치 마법사를 사용 하 여**

1. SQL Server 설치 마법사를 실행합니다.

2. 에 **설치** 탭에서 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**합니다.

    
     ![R Services (In-database) 설치](media/2016-setup-installation-rsvcs.png "R 서비스와 데이터베이스 엔진의 설치를 시작 합니다.")
   
3. 에 **기능 선택** 페이지에서 다음 옵션을 선택 합니다.

   - 선택 **데이터베이스 엔진 서비스**합니다. 데이터베이스 엔진은 기계 학습을 사용 하는 각 인스턴스에 필요 합니다.
   - 선택 **R Services (In-database)**합니다. R입니다. 데이터베이스의 사용에 대 한 지원을 설치
    
     ![R Services 기능 선택](media/2016setup-rsvcs-features.png "이러한 기능에 대 한 R 서비스에 데이터베이스 선택")

    > [!IMPORTANT]
    > R 서버 및 R 서비스를 동시에 설치 하지 마십시오. 일반적으로 SQL Server에 R Server (독립 실행형)를 연결 하는 데 사용 하는 데이터 과학자 또는 개발자 하는 환경을 만드는 설치 하는 R 솔루션을 배포 합니다. 따라서 같은 컴퓨터에 둘 다 설치할 필요는 없습니다.

4.  에 **Microsoft R Open 설치에 동의** 페이지 **Accept**합니다.
  
    Microsoft R Open, 오픈 소스 R 기본 패키지 및 도구, 고급 R 패키지 및 Microsoft R 개발 팀의 연결 공급자와 함께 배포를 포함 하는 다운로드 하려면이 사용권 계약에 필요 합니다.
  
    이 시점에 설명 된 대로 별도로 설치 관리자를 다운로드 하려면 설치 프로그램을 일시 중지할 수 사용 중인 컴퓨터에 인터넷에 연결 하는 경우 [설치 R components without](installing-ml-components-without-internet-access.md)합니다.
  
5. 다음 사용권 계약에 동의한는 잠깐 일시 중지 된 설치 관리자는 준비 하는 동안입니다. 클릭 **다음** 때 단추를 사용할 수 있습니다.

6. 에 **설치 준비 완료** 페이지에서 다음 항목은 포함 되어 있으며 다음 선택 **설치**합니다.

   + 데이터베이스 엔진 서비스
   + R Services(In-Database)

7. 설치가 완료 되 면 컴퓨터를 다시 시작 합니다.


## <a name="bkmk2017top"></a>SQL Server 2017 기계 학습 Services (In-database) 설치

> [!div class="checklist"]
> * 데이터베이스 엔진 및 기계 학습 기능 설치
> * 설치 후 단계를 필요한: 기계 학습을 사용 하도록 설정 하 고 다시 시작
> * 선택적 사후 설치 단계: 방화벽 규칙을 추가, 사용자를 추가, 변경 또는 서비스 계정 구성 원격 데이터 과학 클라이언트 설정 합니다.

**시작**

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행합니다.
  
2. 에 **설치** 탭에서 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**합니다.

     ![시스템 학습 Services (In-database) 설치](media/2017setup-installation-page-mlsvcs.png "컴퓨터 학습 서비스와 데이터베이스 엔진의 설치를 시작 합니다.")

3. 에 **기능 선택** 페이지에서 다음 옵션을 선택 합니다.
   
    + 선택 **데이터베이스 엔진 서비스**합니다. 데이터베이스 엔진은 기계 학습을 사용 하는 각 인스턴스에 필요 합니다.

    + 선택 **기계 학습 Services (In-database)**합니다. 이 옵션은 R입니다. 데이터베이스의 사용에 대 한 지원 설치 이 옵션을 선택한 후에 기계 학습 언어를 선택할 수 있습니다. R만 선택 하거나 R 및 Python 모두 추가할 수 있습니다.
   
    ![컴퓨터 학습 서비스 기능 선택](media/2017setup-features-page-mls-rpy.png "이러한 기능에 대 한 R 서비스에 데이터베이스 선택")

    Python 또는 R 언어 옵션을 선택 하지 않으면만 확장성 프레임 워크, 모든 언어별 구성 요소를 설치 하지 않는 SQL Server 신뢰할 수 있는 실행 패드를 포함 하는 설치 마법사에서 설치 합니다.  일반적으로 시작 하 여 하나 이상의 언어를 설치 하는 것이 좋습니다. 그러나 즉시 바인딩 프로세스를 사용 하 여 기계 학습 구성 요소를 업그레이드 하려는 경우이 옵션을 사용할 수 있습니다. 자세한 내용은 참조 [R Services의 인스턴스를 업그레이드 하려면 사용 하 여 SqlBindR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

    하는 것이 좋습니다 있습니다 **없는** 동일한 컴퓨터에 독립 실행형 및 데이터베이스의 기능을 설치 하 고 동시에 설치 하지 않습니다. 일반적으로 솔루션을 배포할 때 SQL Server에 학습 서버 컴퓨터를 연결 하는 데 사용 하는 데이터 과학자 또는 개발자 하는 환경을 만드는 (독립 실행형)를 설치 해야 합니다. 따라서 같은 컴퓨터에 둘 다 설치할 필요는 없습니다.

4.  사용권 계약에 대 한 기계 학습: 설치 하는 언어에 따라 R, Python, 또는 둘 다에 대 한 사용권 계약에 동의 해야 합니다.

    + R:가 사용권 계약에 대 한 사용 조건에 Microsoft R Open, 오픈 소스 R 기본 패키지 및 도구는 Microsoft 개발 팀의 연결 공급자 및 고급 R 패키지와 함께 배포를 포함 하는 설명 합니다.
  
    + Python에 대 한 사용 조건입니다. Python 오픈 소스 라이선스 계약 Anaconda 및 관련된 도구 외에 Microsoft 개발 팀에서 몇 가지 새로운 Python 라이브러리에 대해서도 설명 합니다.

    클릭 **Accept** 의 계약을 나타냅니다. 구성 요소를 준비 하는 동안 잠깐 일시 중지에는 다음의 **다음** 버튼을 사용할 수 있습니다.

    여기에 설명 된 대로 별도로 설치 관리자를 다운로드 하려면 설치 프로그램을 일시 중지할 수 사용 중인 컴퓨터에 인터넷에 연결 하는 경우: [인터넷 연결 되지 않은 컴퓨터 학습 구성 요소를 설치](installing-ml-components-without-internet-access.md)합니다.

6. 에 **설치 준비 완료** 페이지에서 다음 항목은 포함 되어 있으며 다음 선택 **설치**합니다.

   - 데이터베이스 엔진 서비스
   - Machine Learning Services(데이터베이스 내)
   - R, Python, 또는 둘 다

7. 설치가 완료 되 면 설치 로그 위치를 기록 하 고 컴퓨터를 다시 시작 합니다.

###  <a name="bkmk_enableFeature"></a>필수 설치 후 단계

보안상의 이유로 컴퓨터 학습 기능은 설치한 경우에 기본적으로 사용 되지 합니다. 서버 관리자는 기능을 설정 하 고 인스턴스를 다시 시작 해야 합니다. 

이 섹션에서는 기계 학습에 대 한 인스턴스를 다시 구성 하는 방법에 설명 합니다. 구성 외부 서비스 계정을 설정 하 고 실행 패드 서비스를 시작 합니다.

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다. 아직 설치되지 않은 경우 SQL Server 설치 마법사를 다시 실행하여 다운로드 링크를 열고 설치할 수 있습니다.
  
2. 기계 학습을 설치한 인스턴스에 연결 하 고 다음 명령을 실행 합니다.

   ```SQL
   sp_configure
   ```

    값을 찾습니다는 **사용 하도록 설정 하는 외부 스크립트** 있어야 하 고 속성 **0**합니다. 기능을 노출 영역을 줄이기 위해 기본적으로 꺼져 때문입니다.
     
3. 외부 스크립팅 기능을 사용 하도록 설정 하려면 다음 문을 실행 합니다.
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
4. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 SQL Server 서비스를 다시 시작합니다. SQL Server 서비스가 자동으로 다시 시작 하면 관련 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다.

    사용 하 여 서비스를 다시 시작할 수는 **서비스** 제어판 또는 SQL Server 구성 관리자를 사용 하 여 패널입니다.

5. SQL Server Management Studio에서 외부 스크립트 실행 서비스 활성화 되어 있는지 확인 하려면 새 열고 **쿼리** 창을 닫은 후 다음 명령 실행 합니다.
  
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```
    이제 **run_value**가 1로 설정되어야 합니다.
    
6. 열기는 **서비스** 패널 및 실행 패드 서비스 인스턴스에 대 한 실행 되 고 있는지 확인 합니다. 여러 인스턴스를 설치할 경우 각 인스턴스에는 자체 실행 패드 서비스가 있습니다.

7. 외부 스크립트 런타임 SQL Server와 통신할 수 있는지 확인 하는 간단한 스크립트를 실행 하는 것이 좋습니다. 

    새 **쿼리** 창을 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 고 다음과 같은 스크립트를 실행 합니다.
    
    + R에 대 한
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + Python에 대 한
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'
    OutputDataSet = InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    스크립트를 처음으로 실행 하려면 외부 스크립트 런타임을 로드 되는 동안 약간 걸릴 수 있습니다. 결과 코드는 다음과 같아야 합니다.

    | hello |
    |----|
    | 1.|


8. 오류가 발생 하는 경우 설치가 완료 된 후 확인 또는 문제 해결 가이드를 참조 해야 할 수 있는 선택적, 기타 변경 내용을 설명 하는 섹션으로 진행 합니다.

    + [선택적 사후 설치 단계: 서비스 및 권한 구성](#bkmk_FollowUp) 
    + [SQL Server의 기계 학습 문제 해결](upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="bkmk_FollowUp"></a>선택적 설치 후 단계

기계 학습에 사용 사례에 따라 서버, 방화벽, 서비스 또는 데이터베이스 사용 권한을 사용 하는 계정에 대 한 추가 변경을 해야 할 수 있습니다. 대/소문자에 따라 다른 변경 해야 합니다.

추가로 변경 해야 하는 일반적인 시나리오는 다음과 같습니다.

* SQL Server에 대 한 인바운드 연결을 허용 하도록 방화벽 규칙을 변경 합니다.
* 추가 네트워크 프로토콜을 사용 하도록 설정 합니다.
* 서버에서 원격 연결을 지원 하는지 확인 합니다.
* 사용 하도록 설정 *암시 된 인증이*, 사용자가 원격 데이터 과학 클라이언트에서 SQL Server 데이터에 액세스 하 고 RODBC 패키지 또는 다른 ODBC 공급자를 사용 하 여 코드를 실행 하는 경우.
* 개별 데이터베이스에 사용자가 액세스할 수 있도록 합니다.
* 실행 패드 서비스와의 통신을 방해 하는 보안 문제를 수정 합니다.
* 사용자가 코드를 실행 하거나 패키지를 설치할 수 있는 권한을 확인 합니다.

> [!NOTE]
> 나열 된 일부 변경 해야 할 수 있습니다. 그러나 시나리오에 적용 가능한 지 확인 하는 모든 항목을 검토 하는 것이 좋습니다.

추가 문제 해결 정보를 볼 수 있습니다: [업그레이드 및 설치 FAQ](../r/upgrade-and-installation-faq-sql-server-r-services.md)

### <a name="bkmk_configureAccounts"></a>실행 패드 계정 그룹에 대 한 묵시적된 인증을 사용 하도록 설정

설치 하는 동안의 보안 토큰에서 작업 실행을 위해 몇 가지 새로운 Windows 사용자 계정이 만들어집니다는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스입니다. 외부 클라이언트에서 R 스크립트를 보낼 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 가능한 작업자 계정을 활성화 하 고 호출 하는 사용자의 id로 매핑합니다 사용자를 위해 R 스크립트를 실행 합니다. 데이터베이스 엔진의이 새로운 서비스 보안 이라는 외부 스크립트 실행을 지원 *암시 된 인증이*합니다.

이러한 계정은 Windows 사용자 그룹에 볼 수 있습니다 **SQLRUserGroup**합니다. 기본적으로 R을 실행 하기 위한 충분 한 더 많은 작업은 일반적으로 20 작업자 계정이 생성 됩니다.

그러나 원격 데이터 과학 클라이언트에서 R 스크립트를 실행 해야 하 고 Windows 인증을 사용 하는 경우 권한을 부여 해야 이러한 작업자 계정에 로그인 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 대신 인스턴스.

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **보안**을 확장하고 **로그인**을 마우스 오른쪽 단추로 클릭한 다음 **새 로그인**을 선택합니다.
2. 에 **로그인-신규** 대화 상자에서 **검색**합니다.
3. 선택 된 **개체 유형** 및 **그룹** 확인란을 선택한 다른 모든 확인란의 선택을 취소 합니다.
4. 클릭 **고급**를 확인 합니다.를 검색할 위치는 현재 컴퓨터를 클릭 한 다음 **지금 찾기**합니다.
5. 부터는 하나를 찾을 때까지 서버에서 그룹 계정 목록 스크롤하여 `SQLRUserGroup`합니다.
    
    + 에 대 한 실행 패드 서비스와 관련 된 그룹의 이름에서 _기본 인스턴스_ 방금는 항상 **SQLRUserGroup**합니다. 기본 인스턴스에 대해서만이 계정을 선택 합니다.
    + 사용 하는 경우는 _명명 된 인스턴스_, 인스턴스 이름이 기본 이름에 추가 됩니다 `SQLRUserGroup`합니다. 따라서 인스턴스 이름이 "MLTEST" 이면이 인스턴스에 대 한 기본 사용자 그룹 이름을 것 **SQLRUserGroupMLTest**합니다.
5. 클릭 **확인** 고급 검색 대화 상자를 닫고 인스턴스에 대 한 올바른 계정 선택 했는지 확인 합니다. 각 인스턴스는 자체 실행 패드 서비스와 해당 서비스에 대해 생성 된 그룹에 사용할 수 있습니다.
6. 클릭 **확인** 를 한 번 더 닫습니다는 **사용자 또는 그룹 선택** 대화 상자.
7. 에 **로그인-신규** 대화 상자를 클릭 **확인**합니다. 기본적으로 로그인은 **public** 역할에 할당되며 데이터베이스 엔진에 연결할 수 있는 권한이 있습니다.

### <a name="bkmk_AllowLogon"></a>사용자 한 외부 스크립트를 실행 하는 권한 부여

> [!NOTE]
> SQL Server 계산 컨텍스트에서에서 R 스크립트를 실행 하기 위한 SQL 로그인을 사용 하는 경우에이 단계가 필요 하지 않습니다.

설치한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 직접에 일반적으로 스크립트를 실행할 관리자 또는 데이터베이스 소유자는 최소한가지고 다양 한 작업, 새 패키지를 설치 하는 기능과 데이터베이스의 모든 데이터에 대 한 암시적 사용 권한 필요한 경우.

그러나 엔터프라이즈 시나리오에서 SQL 로그인을 사용 하 여 데이터베이스를 액세스 하는 사용자를 포함 한 대부분의 사용자 없는 이러한 승격 된 권한입니다. 따라서, Python 또는 R 스크립트를 실행할 각 사용자에 대해 각 데이터베이스에서 스크립트를 실행 한 외부 스크립트 사용될지 사용자 권한을 부여 해야 합니다.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> 설치와 관련된 도움이 필요하세요? 모든 단계를 실행했는지 확인하고 싶으세요? 이러한 사용자 지정 보고서를 사용 하 여 설치 상태를 확인 하 고 추가 단계를 실행 합니다. 
> 
> [사용자 지정 보고서를 사용 하 여 컴퓨터 학습 서비스 모니터링](monitor-r-services-using-custom-reports-in-management-studio.md)합니다.

### <a name="ensure-that-the-sql-server-computer-supports-remote-connections"></a>SQL Server 컴퓨터에서 원격 연결을 지원 하는지 확인 하십시오.

원격 컴퓨터에서 연결할 수 없는 경우 서버에서 원격 연결 허용 되는지 여부를 확인 합니다. 원격 연결이 기본적으로 비활성화 하는 경우가 있습니다.

또한 방화벽 SQL Server에 대 한 액세스를 허용 하는지 여부를 확인 하려면 확인 합니다. 기본적으로 SQL Server에서 사용 되는 포트는 종종 방화벽에 의해 차단 됩니다. Windows 방화벽을 사용 하는 경우 참조 [데이터베이스 엔진 액세스에 대 한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)합니다.

### <a name="give-your-users-read-write-or-ddl-permissions-to-the-database"></a>사용자의 읽기, 쓰기 또는 데이터베이스에 DDL 사용 권한을 부여 합니다.

Python 또는 R을 실행 하는 데 사용 되는 사용자 계정 수 할 다른 데이터베이스에서 데이터를 읽는 결과 저장 하기 위한 새 테이블 만들고 테이블에 데이터를 쓸 합니다. 따라서, Python 또는 R 스크립트를 실행 하는 각 사용자에 대 한 데이터베이스에는 사용자에 적절 한 권한이 있는지 확인 해야: *db_datareader*, *db_datawriter*, 또는 *db_ ddladmin*합니다.

예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 *RSamples* 데이터베이스에서 T-SQL 쿼리를 실행할 수 있는 권한을 SQL 로그인 *MySQLLogin* 에 부여합니다. 이 문을 실행하려면 SQL 로그인이 서버의 보안 컨텍스트에 이미 있어야 합니다.

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

각 역할에 포함 된 사용 권한에 대 한 자세한 내용은 참조 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)합니다.

### <a name="use-machine-learning-in-an-azure-vm"></a>기계 학습을 사용 하 여 Azure VM에서

Azure 가상 컴퓨터에서 컴퓨터 학습 서비스 (또는 R Services)를 설치한 경우 몇 가지 추가 기본값을 변경 해야 합니다. 자세한 내용은 참조 [Azure 가상 컴퓨터에서 SQL Server 기계 학습 설치](installing-sql-server-r-services-on-an-azure-virtual-machine.md)합니다.

### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>데이터 과학 클라이언트의 인스턴스에 대한 ODBC 데이터 원본 만들기

데이터 과학 클라이언트 컴퓨터에서 R 솔루션을 만들고 계산 컨텍스트로 써 SQL Server 컴퓨터를 사용 하 여 코드를 실행 해야 하는 경우에 SQL 로그인 또는 Windows 통합된 인증을 사용할 수 있습니다.

* SQL 로그인의 경우: 데이터를 읽을 데이터베이스에 대한 적절한 권한이 로그인에 있는지 확인합니다. 추가 하 여 그렇게 할 수 *연결할* 및 *선택* 사용 권한 또는 로그인을 추가 하 여는 *db_datareader* 역할입니다. 개체를 만들어야 하는 로그인에 대 한 추가 *DDL_admin* 권한. 테이블에 데이터를 저장 해야 하는 로그인에 대 한 로그인을 추가 *db_datawriter* 역할입니다.

* Windows 인증을 위해: 인스턴스 이름 및 기타 연결 정보를 지정 하는 데이터 과학 클라이언트에 ODBC 데이터 소스를 구성 해야 할 수도 있습니다. 자세한 내용은 참조 [ODBC 데이터 원본 관리자](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)합니다.

## <a name="next-steps"></a>다음 단계

SQL Server에서 스크립트 실행 기능이 작동 하는지 확인 한 후에 SQL Server Management Studio, Visual Studio Code 또는 T-SQL 문을 서버로 보낼 수 있는 다른 모든 클라이언트에서 R 및 Python 명령을 실행할 수 있습니다. 이렇게 하기 전에 새 R 패키지를 추가 또는 기계 학습의 사용을 지원 하도록 시스템 구성에 대 한 일부 변경 하는 것이 좋습니다.

이 섹션에는 몇 가지 일반적인 최적화 및 학습 활동 기계 학습을 나열합니다.

### <a name="add-more-worker-accounts"></a>작업자 계정을 더 추가 합니다.

R을 많이, 사용할 수 있다고 생각 되 면 또는 많은 사용자를 동시에 실행 중인 스크립트 상태가 될 것으로 예상한 경우에 실행 패드 서비스에 할당 된 작업자 계정의 수를 늘릴 수 있습니다. 자세한 내용은 참조 [SQL Server 컴퓨터 학습 서비스에 대 한 사용자 계정 풀 수정](modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

### <a name="bkmk_optimize"></a>외부 스크립트 실행에 대 한 서버를 최적화 합니다.

에 대 한 기본 설정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 다양 한 추출, 변환 및 로드 하는 ETL 프로세스를 보고, 감사를 데이터베이스 엔진에서 지원 되는 서비스에 대 한 서버의 균형을 최적화 하는 데 사용 됩니다 하 고 사용 하는 응용 프로그램 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터입니다. 따라서, 기본 설정에서 기계 학습에 대 한 리소스는 제한 또는 제한 하 여 메모리 집중형 작업에 특히 경우가 있을 수 있습니다.

을 보장 하기 위해 컴퓨터 학습 작업 우선 순위를 지정 하 고 적절 하 게 리소스는 외부 리소스 풀을 구성 하려면 SQL Server 리소스 관리자를 사용 하는 것이 좋습니다. 에 할당 된 메모리 양을 변경할 수도 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진, 또는에서 실행 되는 계정 수가 증가 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다.

- 외부 리소스 관리를 위해 리소스 풀을 구성 하려면 참조 [외부 리소스 풀을 만들](../../t-sql/statements/create-external-resource-pool-transact-sql.md)합니다.
  
- 데이터베이스에 대해 예약 된 메모리의 크기를 변경 하려면 참조 [서버 메모리 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)합니다.
  
- 에 의해 시작 될 수 있는 R 계정의 수를 변경 하려면 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], 참조 [기계 학습에 대 한 사용자 계정 풀 수정](modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

동적 관리 뷰 (Dmv) 및 확장 이벤트 뿐 아니라 Windows 이벤트 모니터링, 오른쪽에서 사용 되는 서버 리소스를 관리할 수 있도록 Standard Edition을 사용 하는 리소스 관리자를 갖지 않는 경우 사용할 수 있습니다. 자세한 내용은 참조 [모니터링 및 R 서비스 관리](managing-and-monitoring-r-solutions.md)합니다.

### <a name="install-additional-r-packages"></a>추가 R 패키지를 설치 합니다.

사용할 수 있는 추가 R 패키지를 설치 하려면 몇 분을 걸립니다.

SQL Server에서 사용할 패키지는 인스턴스에서 사용되는 기본 라이브러리에 설치되어야 합니다. 컴퓨터에서 R의 별도 설치 하는 경우 또는 사용자 라이브러리에 패키지를 설치한 경우에 T-SQL에서 이러한 패키지를 사용할 수 없습니다.

설치 및 R 패키지를 관리 하기 위한 프로세스는 SQL Server 2016 및 SQL Server 2017에서 다릅니다. 예를 들어 SQL Server 2017에 데이터베이스당 수준에 있는 패키지를 공유 하려면 사용자 그룹을 설정 하거나 사용자가 자신의 패키지를 설치할 수 있도록 데이터베이스 역할을 구성할 수 있습니다. 자세한 내용은 참조 [관리 패키지](r-package-management-for-sql-server-r-services.md)합니다.

SQL Server 2016에서 데이터베이스 관리자는 사용자가 필요로 하는 R 패키지를 설치 해야 합니다.

관리 액세스가 인스턴스 라이브러리에 추가 Python 패키지를 설치 하는 데 필요 합니다.

### <a name="upgrade-the-machine-learning-components"></a>기계 학습 구성 요소를 업그레이드 합니다.

SQL Server에서 컴퓨터 학습 기능을 설치 하는 경우 릴리스 나 서비스 팩을 게시할 때 최신 했던 Python 또는 R 구성 요소 버전을 가져올 수 있습니다. 서버를 업그레이드 하거나 패치 때마다 컴퓨터 학습 구성 요소의 업그레이드 됩니다.

그러나 기계 학습가 지 원하는 것 보다 더 빠른 일정에 따라 구성 요소를 업그레이드할 수 있습니다 이라는 프로세스를 사용 하 여 SQL Server 릴리스에서 _바인딩_합니다. SQL Server 인스턴스를 바인딩하는 경우 R, Python 버전을 업그레이드와 지 원하는 좀 더 자주 업그레이드 다른 지원 정책을 변경 합니다. 

이러한 업그레이드는 다음과 같습니다.

* 새 R 패키지
+ Microsoft에 대 한 새로운 Api와 같은 패키지 [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)합니다.
* [모델을 미리 학습 된](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) 이미지 분류 및 텍스트 분석에 대 한 합니다.

SQL Server 인스턴스를 업그레이드 하는 방법에 대 한 정보를 참조 하십시오. [바인딩을 통해 컴퓨터 학습 구성 요소를 업그레이드](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.


### <a name="tutorials"></a>자습서

몇 가지 간단한 예제 시작 하 고 SQL Server R 작동 하는 방법의 기본 사항 참조 [TRANSACT-SQL에서 사용 하 여 R 코드](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)합니다.

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 참조 [자습서 학습 컴퓨터](../tutorials/machine-learning-services-tutorials.md)합니다.

### <a name="troubleshooting"></a>문제 해결

문제가 발생하나요? 업그레이드 하려는? 알려진 문제와 관련 된 일반적인 질문에 대답 하십시오에 대 한 다음 문서를 참조 합니다.

* [업그레이드 및 설치 FAQ-컴퓨터 학습 서비스](upgrade-and-installation-faq-sql-server-r-services.md)

인스턴스의 설치 상태를 확인 하 고 일반적인 문제를 해결 하려면 이러한 사용자 지정 보고서를 봅니다.

* [SQL Server R Services에 대 한 사용자 지정 보고서](\r\monitor-r-services-using-custom-reports-in-management-studio.md)
