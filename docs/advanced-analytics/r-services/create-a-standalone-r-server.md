---
title: "독립 실행형 R Server 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 35
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 27
---
# 독립 실행형 R Server 만들기
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에는 **Microsoft R Server(독립 실행형)**를 설치하는 옵션이 포함되어 있습니다. 이 옵션을 사용하면 선택한 데이터베이스 또는 데이터 원본에 연결하는 동시에 Windows에서 고성능 R 솔루션을 개발할 수 있습니다. Microsoft R Server는 Enterprise Edition에서만 사용할 수 있습니다.  
  
 Microsoft R Server를 설치하면 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 제공되는 것과 동일한 고급 R 패키지 및 연결 도구를 사용할 수 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 필요하지 않으며 R 스크립트 실행이 데이터베이스가 아니라 독립 실행형 컴퓨터에서 수행됩니다.  
  
> [!NOTE]  
>  이제 [최신 수명 주기](https://support.microsoft.com/help/447912) 정책에 인스턴스를 등록하는 간소화된 설치를 통해 Microsoft R Server를 사용할 수도 있습니다. 이 지원을 통해 항상 최신 버전의 R을 사용할 수 있습니다. 간소화된 설치 사용에 대한 자세한 내용은 [Windows용 Microsoft R Server 실행](https://msdnstage.redmond.corp.microsoft.com/microsoft-r/rserver-install-windows?branch=r-server-nov16-dev)을 참조하세요.
>  
> 간소화된 설치를 통해 Microsoft R Server를 설치하는 경우 새 지원 정책을 사용하고 R 구성 요소 업데이트를 더 자주 가져오도록 지정된 R Services 인스턴스를 변환할 수도 있습니다. 자세한 내용은 [SqlBindR.exe를 사용하여 R Services 인스턴스 업그레이드](http://www.bing.com)를 참조하세요.   
  
##  <a name="a-namebkmkinstallrservicesindatabasea-install-microsoft-r-server-standalone"></a><a name="bkmk_installRServicesInDatabase"></a> Microsoft R Server(독립 실행형) 설치  
  
1.  이전 버전의 Microsoft R Server를 설치한 경우 이전 버전을 먼저 제거해야 합니다.  [이전 버전의 Microsoft R Server에서 업그레이드](#bkmk_Uninstall)를 참조하세요. 

2. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행합니다.  
  
2.  **설치** 탭에서 **새 R Server(독립 실행형) 설치** 를 클릭합니다.  
  
     ![Setup option for R Server Standalone](../../advanced-analytics/r-services/media/rsql-rstandalonesetup.png "Setup option for R Server Standalone")  
  
3.  **기능 선택** 페이지에서 다음 옵션은 이미 선택되어 있습니다.  
  
    -   **R 서버(독립 실행형)**  
  
         이 옵션을 사용하는 경우 오픈 소스 R 도구 및 기본 패키지를 비롯한 공유 기능과 Microsoft R에서 제공하는 고급 R 패키지 및 연결 도구를 설치합니다.  
  
     기타 모든 옵션은 무시해도 됩니다.  
  
4.  Microsoft R Open을 다운로드 및 설치하려면 사용 조건에 동의합니다. **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다. 이러한 구성 요소와 구성 요소에 필요할 수 있는 필수 구성 요소를 설치하려면 다소 시간이 걸릴 수 있습니다.   
  
5.  **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.  
  
> [!TIP]
> 자동 설치 또는 오프라인 설치에 대한 자세한 내용은 [명령줄에서 Microsoft R Server 설치](../../advanced-analytics/r-services/install-microsoft-r-server-from-the-command-line.md)를 참조하세요.

  
## <a name="what-is-installed-and-where-to-find-r-packages"></a>설치된 기능 및 R 패키지를 찾을 수 있는 위치  
 Microsoft R Server에는 병렬 처리, 향상된 성능, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Hadoop을 비롯한 데이터 원본에 대한 연결을 지원하는 고급 R 패키지 집합과 R 기본 패키지가 포함되어 있습니다.  
  
-   **R 패키지**  
  
     R 라이브러리는 Microsoft SQL Server 2016과 함께 설치되는 다른 도구 및 유틸리티와 함께 설치됩니다. 예를 들어  
  
     `C:\Program Files\Microsoft SQL Server\130\R_SERVER`  
  
     또한 이 폴더에는 R 기본 패키지에 대한 설명서, 샘플 데이터, R 도구 및 런타임에 대한 설명서가 들어 있습니다.  
  
    > [!NOTE]  
    >  SQL Server 인스턴스와 R Services(In-Database)를 동일한 컴퓨터에 설치한 경우에는 R 라이브러리 및 도구가 다른 폴더에 설치됩니다. `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`  
    >   
    >  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스와 연결된 R 패키지 또는 유틸리티를 사용하지 마세요. 항상 R_SERVER 폴더에 있는 R 도구와 패키지를 사용합니다.  
  
-   **R 도구**  
  
     R 개발 IDE는 설치의 일부로 설치되지 않습니다. RStudio, [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 또는 원하는 다른 개발 환경을 설치할 수 있습니다.  
  
     그러나 추가 도구는 필요하지 않습니다. 모든 표준 기본 R 도구는 `C:\Program Files\Microsoft SQL Server\130\R_SERVER\bin`에 들어 있습니다.  
  
     자세한 내용은 [R 도구 설치 또는 구성](../../advanced-analytics/r-services/setup-or-configure-r-tools.md)을 참조하세요.  


 
## <a name="troubleshooting"></a>문제 해결  

### <a name="incompatible-version-of-r-client-and-r-server"></a>호환되지 않는 버전의 R 클라이언트 및 R 서버

최신 버전의 Microsoft R Client를 설치하고 이 클라이언트를 통해 SQL Server에서 원격 계산 컨텍스트를 사용하여 R을 실행하는 경우 다음과 같은 오류가 발생할 수 있습니다.

*컴퓨터에서 Microsoft R Server 버전 8.0.3과 호환되지 않는 Microsoft R Client 버전 9.0.0을 실행 중입니다. 호환되는 버전을 다운로드하여 설치하세요.*

일반적으로 서비스 릴리스가 게시되면 SQL Server R Services와 함께 설치된 R 버전이 업데이트됩니다. 항상 최신 버전의 R 구성 요소가 있도록 하려면 모든 서비스 팩을 설치합니다. Microsoft R Client 9.0.0과 호환성을 위해 이 [지원 문서](https://support.microsoft.com/kb/3210262)에 설명된 업데이트를 설치해야 합니다. 


### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>Windows Core에 설치된 SQL Server 인스턴스에 Microsoft R Server 설치
SQL Server 2016 릴리스 버전에서는 Windows Server Core 버전의 인스턴스에 Microsoft R Server를 추가하는 경우 알려진 문제가 있었습니다. 이 문제가 해결되었습니다. 

이 문제가 발생하는 경우 [KB3164398](https://support.microsoft.com/kb/3164398)에 설명된 수정 사항을 적용하여 Windows Server Core의 기존 인스턴스에 R 기능을 추가할 수 있습니다.   자세한 내용은 [Windows Server Core 운영 체제에 Microsoft R Server 독립 실행형을 설치할 수 없음](https://support.microsoft.com/kb/3168691)을 참조하세요.


###  <a name="a-namebkmkuninstalla-upgrading-from-an-older-version-of-microsoft-r-server"></a><a name="bkmk_Uninstall"></a> 이전 버전의 Microsoft R Server에서 업그레이드  
 Microsoft R Server 시험판 버전을 설치한 경우 먼저 제거해야 최신 버전으로 업그레이드할 수 있습니다.  
  
**R 서버(독립 실행형)를 제거하려면**  
  
1.  **제어판**에서 **프로그램 추가/제거**를 클릭하고 `Microsoft SQL Server 2016 <version number>`을 선택합니다.  
  
2.  구성 요소 **추가**, **복구** 또는 **제거** 옵션이 있는 대화 상자에서 **제거**를 선택합니다.  
  
3.  **기능 선택** 페이지의 **공유 기능**에서 **R 서버(독립 실행형)**를 선택합니다. **다음**을 클릭한 다음 **마침**을 클릭하여 방금 선택한 구성 요소를 제거합니다.  
   
### <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>"한 번에 하나의 Revolution Enterprise 제품만 설치할 수 있습니다." 오류가 발생하고 설치에 실패함  
Revolution Analytics 제품의 이전 설치 또는 SQL Server R Services 시험판 버전이 있는 경우 이 오류가 발생할 수 있습니다. 먼저 이전 버전을 제거해야 최신 버전의 Microsoft R Server를 설치할 수 있습니다. 다른 버전의 Revolution Enterprise 도구와 함께 설치하는 것은 지원되지 않습니다.  

그러나 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]와 함께 R 서버 독립 실행형을 사용하는 경우에는 나란히 설치할 수 있습니다. 
  
### <a name="unable-to-uninstall-older-components"></a>이전 구성 요소를 제거할 수 없음   
  
이전 버전을 제거하는 데 문제가 있는 경우 레지스트리를 편집하여 관련 키를 제거해야 할 수도 있습니다.  

> [!IMPORTANT]
> 이 문제는 Microsoft R Server 시험판 버전 또는 SQL Server 2016 R Services CTP 버전을 설치한 경우에만 적용됩니다.
  
1. Windows 레지스트리를 열고 `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall` 키를 찾습니다.  
2. 다음 항목이 있고 키에 `sEstimatedSize2` 값만 포함된 경우에는 모두 삭제합니다.  
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (8.0.2의 경우)  
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (8.0.1의 경우)  
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (8.0.0의 경우)  
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (7.5.0의 경우)  
  
## <a name="see-also"></a>관련 항목:  
 [Microsoft R Server](../../advanced-analytics/r-services/r-server-standalone.md)  
  
  