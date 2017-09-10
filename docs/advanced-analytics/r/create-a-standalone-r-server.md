---
title: "독립 실행형 R Server 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 35
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4f39a03ecf7b74e0e1305d692a71c28609c80bf0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-standalone-r-server"></a>독립 실행형 R Server 만들기

SQL Server 설치 프로그램에는 기계 학습 SQL Server 외부에서 실행 하는 서버를 설치 하는 옵션이 포함 되어 있습니다. 

이 옵션은 windows에서 고성능 R 솔루션을 개발 하 고 다음 다른 플랫폼에서 솔루션을 공유 하려는 경우에 유용할 수 있습니다. 또한 실행 이러한 이벤트에 대해 지원 되는 원격 계산 컨텍스트에 솔루션을 작성 하기 위한 환경을 설정 하는 서버 옵션을 사용할 수 있습니다.
  
  + R Services를 실행하는 SQL Server 인스턴스
  + Hadoop 또는 Spark 클러스터를 사용하는 R Server 인스턴스
  + Teradata 데이터베이스 내 분석
  + Linux에서 실행하는 R Server 

이 항목에서는 Microsoft R Server 및 Microsoft 학습 서버 컴퓨터에 대 한 SQL Server 설치 프로그램의 설치 단계를 설명 합니다.

## <a name="which-should-i-install"></a>설치 해야 합니까?

**Microsoft R Server** 먼저 SQL Server 2016의 일부로 제공 된 및 R 언어를 지원 합니다. 마지막 버전의 Microsoft R Server 9.0.1 했습니다.
SQL Server 2017 년 1에서 R 서버 이름을 바꾼 **Microsoft 컴퓨터 학습 서버**, Python에 대 한 지원을 추가 합니다. 최신 버전의 Microsoft 컴퓨터 학습 서버 9.1.0입니다.

Microsoft R Server와 Microsoft 학습 서버 컴퓨터 모두 Enterprise Edition이 필요 합니다.

+ [SQL Server 설치 프로그램을 사용 하 여 Microsoft R Server (독립 실행형) 설치](#bkmk_installRServer)
+ [Microsoft 컴퓨터 학습 Server (독립 실행형) SQL Server 설치 프로그램을 사용 하 여 설치](#bkmk_installRServer) 

  설치하려면 SQL Server 라이선스가 필요하며, 일반적으로 업그레이드는 SQL Server 릴리스 주기와 일치합니다. 이렇게 하면 개발 도구가 SQL Server 계산 컨텍스트에서 실행되는 버전과 동기화됩니다.

+ [Windows 용 R 서버 설치](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)

  이 옵션을 최신 수명 주기 지원 정책을 사용 하 여 R 서버가 설치 됩니다. SQL Server 2016의 인스턴스를 업그레이드 하려면 설치 후이 설치 관리자를 실행할 수도 있습니다. 현재 있습니다 _없습니다_ Python 지원이 옵션을 사용 하 여 설치 합니다. Python를 얻으려면 SQL Server 2017 설치 프로그램을 사용 하 여 컴퓨터 학습 서버를 설치 해야 합니다.

##  <a name="bkmk_installRServer"></a>Microsoft 컴퓨터 학습 Server (독립 실행형)를 설치 하는 방법
  
1. 이전 버전의 Microsoft R Server를 설치한 경우 제거 하는 것 먼저 하는 것이 좋습니다.

2. SQL Server 2017 설치 프로그램을 실행 합니다.
  
3. 클릭는 **설치** 탭을 선택 **새 컴퓨터 학습 Server (독립 실행형) 설치**합니다.

4. 규칙 확인이 완료 된 후에 SQL Server 라이선스 조건에 동의 하 고 새로 설치를 선택 합니다.

5. 에 **기능 선택** 페이지에서 다음 옵션은 이미 선택:
    
    - Microsoft 기계 Server (독립 실행형)를 학습 합니다.
    
    - R 및 Python 기본적으로 선택 됩니다.
    
    기타 모든 옵션은 무시해야 합니다.

6.  다운로드 하 고 기계 학습 구성 요소 설치에 대 한 사용 조건에 동의 합니다. 별도 라이선스 계약은 Microsoft R Open 및 Python 필요입니다. 
    
    **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다. 
    
    이러한 구성 요소와 구성 요소에 필요할 수 있는 필수 구성 요소를 설치하려면 다소 시간이 걸릴 수 있습니다. 
    
    컴퓨터에 인터넷 액세스가 없는 경우 사전에 있는 구성 요소 설치 관리자를 다운로드 합니다. 자세한 내용은 참조 [인터넷 연결 되지 않은 구성 요소 설치 ML](./installing-ml-components-without-internet-access.md)합니다. 
    
7.  **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.


자동 설치 또는 오프라인 설치에 대한 자세한 내용은 [명령줄에서 Microsoft R Server 설치](../../advanced-analytics/r-services/install-microsoft-r-server-from-the-command-line.md)를 참조하세요.

###  <a name="bkmk_installRServer"></a> Microsoft R Server(독립 실행형) 설치  

1. 이전 버전의 Microsoft R Server 또는 모든 버전의 Revolution Analytics 도구를 설치 하는 경우 먼저 제거 해야 있습니다.  [이전 버전의 Microsoft R Server에서 업그레이드](#bkmk_Uninstall)를 참조하세요.

2. SQL Server 2016 설치 프로그램을 실행 합니다. 서비스 팩 1 이상을 설치 하는 것이 좋습니다.

3. **설치** 탭에서 **새 R Server(독립 실행형) 설치** 를 클릭합니다.
    
     ![R Server 독립 실행형에 대한 설치 옵션](media/rsql-rstandalonesetup.png "R Server 독립 실행형에 대한 설치 옵션")
    
4.  **기능 선택** 페이지에서 다음 옵션은 이미 선택되어 있습니다.
    
    **R 서버(독립 실행형)**  
    
    기타 모든 옵션은 무시해도 됩니다. SQL Server 데이터베이스 엔진 또는 SQL Server R Services를 설치 하지 마십시오.
    
5.  Microsoft R Open을 다운로드 및 설치하려면 사용 조건에 동의합니다. **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다. 
    
    이러한 구성 요소와 구성 요소에 필요할 수 있는 필수 구성 요소를 설치하려면 다소 시간이 걸릴 수 있습니다.
    
6.  **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.  


### <a name="upgrade-an-existing-r-server-to-901"></a>기존 R 서버 9.0.1로 업그레이드

이전 버전의 Microsoft R Server (독립 실행형)를 설치한 경우에 최신 버전의 R 구성 요소를 사용 하도록 인스턴스를 업그레이드할 수 있습니다. 업그레이드는 최신 수명 주기 지원 정책 서버도 변경 됩니다. 따라서 인스턴스를 SQL Server를 해제 하는 보다 다른 일정에서 더 자주 업데이트 될 수 있습니다.

1. 아직 설치되어 있지 않으면 Microsoft R Server(독립 실행형)를 설치합니다.

2. 여기에 나열 된 위치에서 별도 Windows 기반 installer 다운로드: [Windows 용 Microsoft R Server 실행](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall)합니다.

3. 설치 관리자를 실행 하 고 따릅니다 [이러한 지침](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#download-r-server-installer)합니다.


### <a name="change-in-default-folder-for-r-packages"></a>R 패키지에 대 한 기본 폴더 변경

SQL Server 설치 프로그램을 사용 하 여를 설치 하면 R 라이브러리 설치에 사용 된 SQL Server 버전에 연결 하는 폴더에 설치 됩니다. 이 폴더에는 샘플 데이터, R 기본 패키지에 대한 설명서, R 도구 및 런타임에 대한 설명서도 들어 있습니다.

**SQL Server 2016을 사용하여 설치된 R Server(독립 실행형)**

`C:\Program Files\Microsoft SQL Server\130\R_SERVER`

**SQL Server 2017을 사용하여 설치된 R Server(독립 실행형)**

`C:\Program Files\Microsoft SQL Server\140\R_SERVER`

**Windows 독립 실행형 설치 관리자를 사용 하 여 설치**

그러나 별도 Windows installer를 사용 하 여 설치 하는 경우 또는 별도 Windows installer를 사용 하 여 업그레이드 하는 경우 R 라이브러리는 다음 R 서버 폴더로 이동 됩니다.

`C:\Program Files\Microsoft\R Server\R_SERVER`
      
**R Servies 또는 기계 학습의 설치 프로그램에서 데이터베이스 서비스**

R Services (In-database) 또는 컴퓨터 학습 Services (In-database)와 함께 SQL Server의 인스턴스를 설치한 경우 해당 인스턴스가 동일한 컴퓨터에 R 라이브러리 및 도구는 다른 폴더에 기본적으로 설치 됩니다.

`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스와 연결된 R 패키지 또는 유틸리티를 직접 호출하지 마세요. R 서버와 R 서비스를 관리자 권한 또는 기타 도구를 실행 해야 하는 경우 동일한 컴퓨터에 설치 되 면 R 도구 및 R_SERVER 폴더에 설치 된 패키지를 사용 합니다.


### <a name="development-tools"></a>개발 도구

개발 IDE 설정의 일부분으로 설치 되지 않았습니다. 추가 도구 필요 하지 않은, 포함 된 모든 표준 도구와는 제공 되는 R, Python의 배포와 함께 합니다.

시도 하는 것이 좋습니다는 새 버전의 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], Visual Studio에서 R 및 Python으로 SQL Server와 BI 도구를 지원 합니다. 그러나 RStudio를 포함 하 여 모든 기본 설정된 개발 환경에 사용할 수 있습니다.

## <a name="troubleshooting"></a>문제 해결  

### <a name="incompatible-version-of-r-client-and-r-server"></a>호환되지 않는 버전의 R 클라이언트 및 R 서버

최신 버전의 Microsoft R Client를 설치하고 이 클라이언트를 통해 SQL Server에서 원격 계산 컨텍스트를 사용하여 R을 실행하는 경우 다음과 같은 오류가 발생할 수 있습니다.

*컴퓨터에서 Microsoft R Server 버전 8.0.3과 호환되지 않는 Microsoft R Client 버전 9.0.0을 실행 중입니다. 호환되는 버전을 다운로드하여 설치하세요.*

일반적으로 서비스 릴리스가 게시되면 SQL Server R Services와 함께 설치된 R 버전이 업데이트됩니다. 항상 최신 버전의 R 구성 요소가 있도록 하려면 모든 서비스 팩을 설치합니다. Microsoft R Client 9.0.0과 호환성을 위해 이 [지원 문서](https://support.microsoft.com/kb/3210262)에 설명된 업데이트를 설치해야 합니다. 


### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>Windows Core에 설치된 SQL Server 인스턴스에 Microsoft R Server 설치

SQL Server 2016 RTM 버전 있었습니다 알려진된 문제를 Microsoft R Server Windows Server Core edition의 인스턴스에 추가 하는 경우. 이 문제가 해결되었습니다.

이 문제가 발생하는 경우 [KB3164398](https://support.microsoft.com/kb/3164398) 에 설명된 수정 사항을 적용하여 Windows Server Core의 기존 인스턴스에 R 기능을 추가할 수 있습니다.   자세한 내용은 [Windows Server Core 운영 체제에 Microsoft R Server 독립 실행형을 설치할 수 없음](https://support.microsoft.com/kb/3168691)을 참조하세요.


###  <a name="bkmk_Uninstall"></a> 이전 버전의 Microsoft R Server에서 업그레이드

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

[Microsoft R Server](../../advanced-analytics/r-services/r-server-standalone.md)


