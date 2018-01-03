---
title: "인스턴스를 설치할지 컴퓨터 학습 서버 독립 실행형 R 서버 독립 실행형 | Microsoft Docs"
ms.custom: 
ms.date: 11/16/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: "35"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: d69755716ae84ed280f8af9c62a85dc861f66d75
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone"></a>학습 Server 컴퓨터 (독립 실행형) 또는 R Server (독립 실행형) 설치

SQL Server 설치 프로그램에는 기계 학습 SQL Server 외부에서 실행 하는 서버를 설치 하는 옵션이 포함 되어 있습니다. 이 옵션은 원격 계산 컨텍스트를 사용할 수 있는 또는 포함 하 여 여러 플랫폼에 배포할 수 있는 고성능 시스템 학습 솔루션을 개발 하는 경우에 유용할 수 있습니다.
  
  + SQL Server 2016 또는 기계 학습 사용 하도록 설정 하는 SQL Server 2017의 인스턴스
  + R 서버 또는 서버를 학습 하는 컴퓨터의 Hadoop 또는 Spark 클러스터에서 인스턴스
  + R Server 또는 linux에서 컴퓨터 학습 서버

이 문서에서는 시스템 학습 서버 또는 Microsoft R Server의 독립 실행형 버전을 설치 하려면 SQL Server 설치 프로그램을 사용 하는 방법을 설명 합니다. Enterprise Edition 또는 Software Assurance 있으면 기계 학습 독립 실행형 서버를 설치 하는 무료입니다.

+ [R 서버 설치](#bkmk_installRServer) -SQL Server 2016 설치 프로그램을 사용 하 여
+ [시스템 학습 서버 설치](#bkmk_installMLServer) -SQL Server 2017 설치 프로그램을 사용 하 여
+ [Microsoft R Server의 기존 인스턴스를 업그레이드 합니다.](#bkmk_upgrade)
+ [도움말 설치할 항목에 보기](#bkmk_tips)

##  <a name="bkmk_installMLServer"></a>기계 학습 Server (독립 실행형) 설치

이 기능을 사용 하려면 엔터프라이즈 라이선스 또는 동등한 옵션이 **SQL Server 2017**합니다.

이전 버전의 Microsoft R Server를 설치한 경우 제거 하는 것 먼저 하는 것이 좋습니다.

컴퓨터에 인터넷 액세스가 없는 경우 사전에 있는 구성 요소 설치 관리자를 다운로드 합니다. 자세한 내용은 참조 [인터넷 연결 되지 않은 컴퓨터 학습 구성 요소 설치](./installing-ml-components-without-internet-access.md)합니다.

1. SQL Server 2017 설치 프로그램을 실행 합니다.

2. 클릭는 **설치** 탭을 선택 **새 컴퓨터 학습 Server (독립 실행형) 설치**합니다.
    
     ![시스템 학습 서버 독립 실행형 설치](media/2017setup-installation-page-mlsvr.png "학습 서버 독립 실행형 컴퓨터의 설치를 시작 합니다.")

3. 규칙 확인이 완료 된 후에 SQL Server 라이선스 조건에 동의 하 고 새로 설치를 선택 합니다.

4. 에 **기능 선택** 페이지에서 다음 옵션을 이미 선택 되어 있어야 합니다.

    - Microsoft 기계 Server (독립 실행형)를 학습 합니다.

    - R 및 Python 기본적으로 선택 됩니다. 두 언어 선택을 취소할 수 있지만 지원 되는 언어 중 하나 이상을 설치 하는 것이 좋습니다.

     ![시스템 학습 서버 독립 실행형 설치](media/2017setup-features-page-mlsvr-rpy.png "학습 서버 독립 실행형 컴퓨터의 설치를 시작 합니다.")
    
    기타 모든 옵션은 무시해야 합니다. 
    
    > [!NOTE]
    > 설치 하지 않습니다는 **공유 기능** 컴퓨터에 SQL Server 데이터베이스에서 분석에 대 한 설치 된 컴퓨터 학습 서비스 하는 경우. 중복 된 라이브러리를 만듭니다.
    > 
    > 또한 SQL Server에서 실행 되는 R, Python 스크립트를 SQL Server를 하지 못하도록 다른 데이터베이스 엔진 서비스에서 사용 되는 메모리와 충돌 하 여 관리 하는 반면 서버는 독립 실행형 컴퓨터 학습에는 이러한 제한이 있으며, 다른 데이터베이스 작업을 방해할 수 있습니다. . 마지막으로, 화에 대해 자주 사용 되는 RDP 세션을 통한 원격 액세스는 일반적으로 데이터베이스 관리자가 차단 됩니다.
    > 
    > 이러한 이유로, 일반적으로 권장 SQL Server 컴퓨터 학습 서비스와에서 별도 컴퓨터에 학습 Server 컴퓨터 (독립 실행형)를 설치 하는 합니다.

5.  다운로드 하 고 기계 학습 구성 요소 설치에 대 한 사용 조건에 동의 합니다. 언어를 모두 설치 하는 경우 별도 사용권 계약은 Python 및 Microsoft R에 필요 합니다.
    
     ![Python 사용권 계약](media/2017setup-python-license.png "Python 사용권 계약")
    
    이러한 구성 요소 및 해야, 모든 필수 구성 요소 설치에는 시간이 걸릴 수 있습니다. **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다.

6.  **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.

자동 또는 오프 라인 설치에 대 한 자세한 내용은 참조 [명령줄에서 Microsoft R Server 설치](../../advanced-analytics/r/install-microsoft-r-server-from-the-command-line.md)합니다.

##  <a name="bkmk_installRServer"></a> Microsoft R Server(독립 실행형) 설치

이 기능을 사용 하려면 엔터프라이즈 라이선스 또는 동등한 옵션이 **SQL Server 2016**합니다.

모든 이전 버전의 Revolution Analytics 도구 또는 패키지를 설치한 경우에 먼저 제거 해야 있습니다. 참조 [Microsoft R Server의 이전 버전에서 업그레이드](#bkmk_Uninstall)합니다.

1. SQL Server 2016 설치 프로그램을 실행 합니다. 서비스 팩 1 이상을 설치 하는 것이 좋습니다.

2. 에 **설치** 탭을 클릭 **새 R Server (독립 실행형) 설치**합니다.
    
     ![R 서버 독립 실행형의 설치 프로그램을 시작](media/2016-setup-installation-rsvr.png "R 서버 독립 실행형의 설치를 시작 합니다.")
    
3.  **기능 선택** 페이지에서 다음 옵션은 이미 선택되어 있습니다.
    
    **R 서버(독립 실행형)**  
    
    ![기능 선택 R Server 독립 실행형에 대 한](media/2016setup-rserver-features.png "기능 서버 독립 실행형 R에 대 한 선택")
    
    기타 모든 옵션은 무시해도 됩니다. 
    
    > [!NOTE]
    > 설치 하지 않습니다는 **공유 기능** R Services 이미 설치 되어 있는 SQL Server 데이터베이스에서 분석에 대 한 컴퓨터에서 설치를 실행 하는 경우. 중복 된 라이브러리를 만듭니다.
    > 
    > SQL Server에서 실행 되는 R 스크립트를 SQL Server를 하지 못하도록 다른 데이터베이스 엔진 서비스에서 사용 되는 메모리와 충돌 하 여 관리 하는 반면 독립 실행형 R 서버에는 이러한 제한이 응용 프로그램과 다른 데이터베이스 작업을 방해할 수 있습니다.
    > 
    > 일반적으로 SQL Server 컴퓨터 학습 서비스와에서 별도 컴퓨터에 학습 Server 컴퓨터 (독립 실행형)를 설치 하는 것이 좋습니다.

4.  Microsoft R Open을 다운로드 및 설치하려면 사용 조건에 동의합니다. **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다.
    
    이러한 구성 요소 및 해야, 모든 필수 구성 요소 설치에는 시간이 걸릴 수 있습니다.
    
5.  **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.

## <a name="bkmk_upgrade"></a>R Server의 기존 인스턴스를 업그레이드 합니다.

이전 버전의 Microsoft R Server (독립 실행형)를 설치한 경우에 최신 버전의 R 구성 요소를 사용 하도록 인스턴스를 업그레이드할 수 있습니다. 또한 업그레이드 최신 소프트웨어 수명 주기 지원 정책을 사용 하 여 지원 정책을 변경 합니다. 따라서 인스턴스를 SQL Server를 해제 하는 보다 다른 일정에서 더 자주 업데이트 될 수 있습니다.

1. 여기에 나열 된 위치에서 별도 Windows 기반 설치 관리자를 다운로드 합니다. 

    + [Windows에 대 한 서버를 학습 하는 컴퓨터를 설치 합니다.](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
    + [Windows 용 R Server 9.1 설치](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

2. 설치 프로그램을 실행 하 고 지시를 따릅니다. 설치할 기능을 선택 하면 페이지에서 업그레이드 하려는 R Server의 각 인스턴스를 선택 합니다.

## <a name ="bkmk_tips"></a>설치에 대 한 추가 작업

이 섹션에서는 설치와 관련 된 추가 정보를 제공 합니다.

### <a name="which-version-should-i-install"></a>어떤 버전을 설치 해야 합니까?

+ **Microsoft R Server** 먼저 SQL Server 2016의 일부로 제공 된 및 R 언어를 지원 합니다. 마지막 버전의 Microsoft R Server 9.0.1 했습니다.

+ **서버를 Microsoft 컴퓨터 학습** Python에 대 한 지원 등의 최신 버전으로 SQL Server 2017와 함께 출시 된 대량 업데이트 기능을 합니다. SQL Server 2017 용 누적 업데이트 1 버전 9.2.1.24 학습 서버 컴퓨터의 포함 된 놓았습니다. 최신 Python Api를 원하는 경우이 업데이트를 좋습니다.

+ **직접 업그레이드**: 설치 하려면 SQL Server 라이선스 및 업그레이드는 일반적으로 SQL Server 릴리스 일정에 맞춰집니다. 이렇게 하면 개발 도구가 SQL Server 계산 컨텍스트에서 실행되는 버전과 동기화됩니다. 그러나 최신 소프트웨어 수명 주기 지원 정책 더 자주 업데이트 하려면 별도 Windows 기반 설치 관리자를 사용할 수 있습니다. SQL Server 2016 또는 SQL Server 2017의 인스턴스를 업그레이드 하려면이 설치 관리자를 사용할 수도 있습니다.

### <a name="default-installation-folders"></a>기본 설치 폴더

R 서버를 설치할 때 또는 SQL Server 설치 프로그램을 사용 하 여 컴퓨터 학습 서버, R 라이브러리 설치에 사용 된 SQL Server 버전에 연결 하는 폴더에 설치 됩니다. 이 폴더에 샘플 데이터, R 기본 패키지에 대 한 설명서 및 R 도구 및 런타임의 설명서도 찾을 수 있습니다.

그러나 별도 Windows installer를 사용 하 여 설치 하는 경우 또는 별도 Windows installer를 사용 하 여 업그레이드 하는 경우 R 라이브러리는 다른 폴더에 설치 됩니다.

참조를 위해 R Services (In-database) 또는 컴퓨터 학습 Services (In-database)와 SQL Server의 인스턴스를 설치 했 고 인스턴스가 동일한 컴퓨터에 해당 하는 경우 R 라이브러리 및 도구를 다른 폴더에 기본적으로 설치 됩니다.

다음 표에서 각 설치에 대 한 경로 나열합니다.

|버전 옵션| 설치 방법 | 기본 폴더|
|----|----|----|
|R Server (Standalone) |SQL Server 2016 설치 마법사|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R Server (Standalone) |독립 실행형 응용 프로그램|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|Machine Learning Server(독립 실행형) |  SQL Server 2017 설치 마법사 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|Machine Learning Server(독립 실행형) |  독립 실행형 응용 프로그램 |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services(In-Database) |SQL Server 2016 설치 마법사|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|Machine Learning Services(데이터베이스 내) |SQL Server 2017 설치 마법사|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES` 또는 `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |

### <a name="development-tools"></a>개발 도구

개발 IDE 설정의 일부분으로 설치 되지 않았습니다. 추가 도구 필요 하지 않은, 포함 된 모든 표준 도구와는 제공 되는 R, Python의 배포와 함께 합니다.

새 릴리스를 시도 하는 것이 좋습니다 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]합니다. Visual Studio 모두 R 및 Python으로 데이터베이스 개발 도구, SQL Server와의 연결 및 BI 도구를 지원합니다. 그러나 RStudio를 포함 하 여 모든 기본 설정된 개발 환경에 사용할 수 있습니다.

## <a name="troubleshooting"></a>문제 해결

이 섹션은 R 서버나 컴퓨터 학습 서버를 설치 하는 경우 고려해 야 할 몇 가지 일반적인 문제를 나열 합니다.

### <a name="incompatible-version-of-r-client-and-r-server"></a>호환되지 않는 버전의 R 클라이언트 및 R 서버

Microsoft R 클라이언트를 설치 하 고 사용 하 여 원격 SQL Server 계산 컨텍스트에서 R을 실행할 경우 다음과 같은 오류가 발생할 수 있습니다.

*9.0.0 버전의 Microsoft R 클라이언트가 8.0.3 버전의 Microsoft R Server와 호환 되지 않는 컴퓨터에 실행 합니다. 호환되는 버전을 다운로드하여 설치하세요.*

SQL Server 2016에서 필수 된 SQL Server R Services에서 실행 중인 R의 버전 수 정확 하 게 Microsoft R 클라이언트에서 라이브러리와 동일 합니다. 이후 버전에서 해당 요구 사항을 제거 되었습니다. 그러나 항상 가져올 구성 요소를 학습 하는 컴퓨터의 최신 버전을 설치 하는 모든 서비스 팩 것이 좋습니다. 

이전 버전의 Microsoft R Server가 설치 하 고 Microsoft R 9.0.0 클라이언트와의 호환성을 위해 필요한 경우이 설명 하는 업데이트를 설치 [지원 문서](https://support.microsoft.com/kb/3210262)합니다.

### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>Windows Core에 설치된 SQL Server 인스턴스에 Microsoft R Server 설치

SQL Server 2016 RTM 버전 있었습니다 알려진된 문제를 Microsoft R Server Windows Server Core edition의 인스턴스에 추가 하는 경우. 이 문제가 해결되었습니다.

이 문제가 발생 하는 경우에에 설명 된 수정 프로그램을 적용할 수 있습니다 [KB3164398](https://support.microsoft.com/kb/3164398) 를 Windows Server Core에서 기존 인스턴스에 R 기능을 추가 합니다.   자세한 내용은 [Windows Server Core 운영 체제에 Microsoft R Server 독립 실행형을 설치할 수 없음](https://support.microsoft.com/kb/3168691)을 참조하세요.

###  <a name="bkmk_Uninstall"></a>Microsoft R Server의 이전 버전에서 업그레이드

Microsoft R Server 시험판 버전을 설치한 경우 먼저 제거해야 최신 버전으로 업그레이드할 수 있습니다.

**R 서버(독립 실행형)를 제거하려면**

1.  **제어판**에서 **프로그램 추가/제거**를 클릭하고 `Microsoft SQL Server 2016 <version number>`을 선택합니다.

2.  구성 요소 **추가**, **복구**또는 **제거** 옵션이 있는 대화 상자에서 **제거**를 선택합니다.
  
3.  **기능 선택** 페이지의 **공유 기능**에서 **R 서버(독립 실행형)**를 선택합니다. **다음**을 클릭한 다음 **마침** 을 클릭하여 방금 선택한 구성 요소를 제거합니다.

### <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>"한 번에 하나의 Revolution Enterprise 제품만 설치할 수 있습니다." 오류가 발생하고 설치에 실패함

Revolution Analytics 제품의 이전 설치 또는 SQL Server R Services 시험판 버전이 있는 경우 이 오류가 발생할 수 있습니다. 먼저 이전 버전을 제거해야 최신 버전의 Microsoft R Server를 설치할 수 있습니다. 다른 버전의 Revolution Enterprise 도구와 함께 설치하는 것은 지원되지 않습니다.

그러나 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 또는 SQL Server 2016과 함께 R 서버 독립 실행형을 사용하는 경우에는 나란히 설치할 수 있습니다.

### <a name="unable-to-uninstall-older-components"></a>이전 구성 요소를 제거할 수 없음

이전 버전을 제거하는 데 문제가 있는 경우 레지스트리를 편집하여 관련 키를 제거해야 할 수도 있습니다.

> [!IMPORTANT]
> 이 문제는 Microsoft R Server 시험판 버전 또는 SQL Server 2016 R Services CTP 버전을 설치한 경우에만 적용됩니다.
  
1. Windows 레지스트리를 열고 `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`키를 찾습니다.
2. 다음 항목이 있고 키에 `sEstimatedSize2`값만 포함된 경우에는 모두 삭제합니다.
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (8.0.2의 경우)
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (8.0.1의 경우)
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (8.0.0의 경우)
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (7.5.0의 경우)
  
## <a name="see-also"></a>관련 항목:

[Machine Learning Server(독립 실행형)](../../advanced-analytics/r/r-server-standalone.md)
