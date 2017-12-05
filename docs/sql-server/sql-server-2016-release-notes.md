---
title: "SQL Server 2016 릴리스 정보 | Microsoft 문서"
ms.date: 10/30/2017
ms.prod: sql-server
ms.prod_service: sql-non-specified
ms.service: server-general
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: server-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- build notes
- release issues
ms.assetid: c64077a2-bec8-4c87-9def-3dbfb1ea1fb6
caps.latest.revision: "276"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 216ae6b44bcfe3166a1b5eb0f989886cc18eaead
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sql-server-2016-release-notes"></a>SQL Server 2016 릴리스 정보
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)] 이 문서에서는 SQL Server 2016 릴리스 관련 제한 사항 및 문제에 대해 설명합니다.    
    
 **사용해보기:**    
   
[![평가 센터에서 다운로드](../includes/media/download2.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)  **[평가 센터](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**에서 SQL Server 2016 다운로드    
    
[![Azure 가상 컴퓨터 소형](../includes/media/azure-vm.png)](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/) Azure 계정이 있습니까?  계정이 있는 경우 **[여기](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)** 로 이동하여 SQL Server 2016 SP1이 이미 설치된 가상 컴퓨터를 실행해 보세요.
    
[![SSMS 다운로드](../includes/media/download2.png)**SSMS:** SQL Server Management Studio의 최신 버전을 얻으려면 **[SSMS(SQL Server Management Studio) 다운로드](../ssms/download-sql-server-management-studio-ssms.md)**를 참조하세요.   
    
 새로운 기능에 대한 자세한 내용은 [SQL Server 2016의 새로운 기능](http://msdn.microsoft.com/library/8223c19b-4b0d-4b1d-a042-9a726c18e708)을 참조하세요.
    
##  <a name="bkmk_top"></a>문서 섹션:    

-   [사용 가능한 SQL Server 2016 서비스 팩 1(SP1)](#bkmk_2016sp1)    
-   [SQL Server 2016 GA(일반 공급)](#bkmk_2016_ga) 
-   [SQL Server 2016 RC3(릴리스 후보 3)](#bkmk_2016_rc3)     

## <a name="bkmk_2016sp1"></a>사용 가능한 SQL Server 2016 서비스 팩 1(SP1)
![info_tip](../sql-server/media/info-tip.png) SQL Server 2016 SP1은 SQL Server 2016의 모든 버전 및 서비스 수준을 SQL Server 2016 SP1로 업그레이드합니다. 이 문서에 나열된 수정 사항 외에 SQL Server 2016 SP1에는 SQL Server 2016 누적 업데이트 1(CU1)부터 SQL Server 2016 CU3에 포함된 핫픽스가 들어 있습니다.
    
- [SQL Server 2016 SP1 다운로드 페이지](https://www.microsoft.com/download/details.aspx?id=54276)
- [SQL Server 2016 서비스 팩 1 릴리스 정보](https://support.microsoft.com/kb/3182545) SP1에서 수정되거나 변경된 개별 버그 및 문제를 나열합니다.
 - ![info_tip](../sql-server/media/info-tip.png) [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 서비스 팩을 포함하여 지원되는 모든 버전에 대한 링크 및 자세한 내용은 [SQL Server 업데이트 센터](https://msdn.microsoft.com/library/ff803383.aspx)를 참조하세요. 
    
    
##  <a name="bkmk_2016_ga"></a> SQL Server 2016 릴리스 - GA (일반 공급)
-   [데이터베이스 엔진(GA)](#bkmk_ga_instalpatch) 
-   [Stretch Database(GA)](#bkmk_ga_stretch)
-   [쿼리 저장소(GA)](#bkmk_ga_query_store)
-   [제품 설명서(GA)](#bkmk_ga_docs)
 
### ![repl_icon_warn](../database-engine/availability-groups/windows/media/repl-icon-warn.gif) <a name="bkmk_ga_instalpatch"></a> Install Patch Requirement (GA) 
**문제 및 고객에게 미치는 영향:** Microsoft는 SQL Server 2016에서 필수 구성 요소로 설치되는 Microsoft VC++ 2013 런타임 이진 파일에 영향을 주는 문제를 확인했습니다. 업데이트로 이 문제를 해결할 수 있습니다. VC 런타임 이진 파일에 대한 이 업데이트가 없으면 SQL Server 2016의 특정 시나리오에서 안정성 문제를 발생할 수 있습니다. SQL Server 2016을 설치하기 전에 컴퓨터에 [KB 3164398](http://support.microsoft.com/kb/3164398)에서 설명한 패치가 필요한지 확인합니다. 패치는 [SQL Server 2016 RTM용 누적 업데이트 패키지 1(CU1)](https://www.microsoft.com/download/details.aspx?id=53338)에도 포함되어 있습니다. 

**해결 방법:** 다음 솔루션 중 하나를 사용합니다.

- [KB 3138367 - Visual C++ 2013 및 Visual C++ 재배포 가능 패키지 업데이트](http://support.microsoft.com/kb/3138367)를 설치합니다. KB는 기본적으로 사용되는 해결 방법입니다. SQL Server 2016 설치 전 또는 설치 후에 이 업데이트를 설치할 수 있습니다. 

    SQL Server 2016이 이미 설치되어 있는 경우 다음 단계를 순서대로 수행합니다.

    1.  적절한 *vcredist_\*exe*를 다운로드합니다.
    1.  데이터베이스 엔진의 모든 인스턴스에 대한 SQL Server 서비스를 중지합니다.
    1.  **KB 3138367**을 설치합니다.
    1.  컴퓨터를 다시 부팅합니다.
 

 - [KB 3164398 - SQL Server 2016 MSVCRT 필수 조건에 대한 중요 업데이트](http://support.microsoft.com/kb/3164398)를 설치합니다.  
 
    **KB 3164398**을 사용하는 경우 Microsoft 업데이트를 통해 또는 Microsoft 다운로드 센터에서 SQL Server 설치 중에 설치할 수 있습니다. 

    - **SQL Server 2016 설치 중:** SQL Server 설치 프로그램을 실행하는 컴퓨터가 인터넷에 액세스하는 경우 전체 SQL ServeR을 설치할 때 업데이트를 검사합니다. 업데이트를 수락하면 설치 프로그램이 다운로드되고 설치하는 동안 이진 파일을 업데이트합니다.

    - **Microsoft 업데이트:** 업데이트는 중요한 비보안 SQL Server 2016 업데이트로 Microsoft 업데이트에서 제공합니다. Microsoft 업데이트를 통해 SQL Server 2016을 설치하면 업데이트를 수행하기 위해 서버를 다시 시작해야 합니다. 

    - **다운로드 센터:** 마지막으로 업데이트는 Microsoft 다운로드 센터에서 제공합니다. SQL Server 2016을 설치한 후 업데이트 소프트웨어를 다운로드하고 서버에 설치할 수 있습니다. 


### <a name="bkmk_ga_stretch"></a>Stretch Database

#### <a name="problem-with-a-specific-character-in-a-database-or-table-name"></a>데이터베이스 또는 테이블 이름의 특정 문자 문제

**문제 및 고객에게 미치는 영향:** 데이터베이스 또는 테이블에서 Stretch Database를 사용하도록 설정하는 작업이 오류로 인해 실패했습니다. 이 문제는 개체의 이름에 소문자에서 대문자로 변환할 때 다른 문자로 취급되는 문자가 포함되는 경우 발생합니다. 이 문제를 일으키는 문자의 예는 "ƒ" 문자입니다(ALT+159를 입력하여 생성).

**해결 방법:** 데이터베이스 또는 테이블에서 Stretch Database를 사용하도록 설정하려면 개체 이름을 바꾸고 문제 문자를 제거하는 것이 유일한 옵션입니다.

#### <a name="problem-with-an-index-that-uses-the-include-keyword"></a>INCLUDE 키워드를 사용하는 인덱스 문제

**문제 및 고객에게 미치는 영향:** 인덱스에서 추가 열을 포함하기 위해 INCLUDE 키워드를 사용하는 인덱스가 있는 테이블에서 Stretch Database를 사용하도록 설정하려고 하면 오류가 발생합니다.

**해결 방법:** INCLUDE 키워드를 사용하는 인덱스를 삭제하고 테이블에서 Stretch Database를 사용하도록 설정한 다음 인덱스를 다시 만듭니다. 이 작업을 수행하는 경우 영향을 받는 테이블의 사용자에게 영향을 주지 않거나 최소화하기 위해 조직의 유지 관리 방법 및 정책을 따라야 합니다.

### <a name="bkmk_ga_query_store"></a>Query Store

#### <a name="problem-with-automatic-data-cleanup-on-editions-other-than-enterprise-and-developer"></a>Enterprise 및 Developer 이외 버전의 자동 데이터 정리 문제

 **문제 및 고객에게 미치는 영향:** Enterprise 및 Developer 이외의 버전에서 자동 데이터 정리를 수행하지 못합니다. 따라서 데이터를 수동으로 제거하지 않으면 쿼리 저장소 사용 공간이 시간이 갈수록 증가하여 한계에 도달합니다. 이 문제가 완화되지 않으면 정리를 실행하려고 할 때마다 덤프 파일을 생성하므로 할당된 디스크 공간이 오류 로그로 채워지게 됩니다. 정리 활성화 기간은 워크로드 빈도에 따라 다르지만 15분 이하입니다.

 **해결 방법:** Enterprise 및 Developer 이외의 버전에서 쿼리 저장소를 사용하려면 정리 정책을 명시적으로 해제해야 합니다. 이 작업은 SQL Server Management Studio(데이터베이스 속성 페이지)에서 또는 Transact-SQL 스크립트를 통해 수행할 수 있습니다.

```ALTER DATABASE <database name> SET QUERY_STORE (OPERATION_MODE = READ_WRITE, CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 0), SIZE_BASED_CLEANUP_MODE = OFF)```

또한 쿼리 저장소가 읽기 전용 모드로 전환되지 않도록 하려면 수동 정리 옵션을 사용하는 것이 좋습니다. 예를 들어 다음 쿼리를 실행하여 전체 데이터 공간을 정기적으로 정리합니다.

```ALTER DATABASE <database name> SET QUERY_STORE CLEAR```

또한 다음 쿼리 저장소 저장 프로시저를 실행하여 런타임 통계, 특정 쿼리 또는 계획을 정기적으로 정리합니다.

- `sp_query_store_reset_exec_stats`

- `sp_query_store_remove_plan`

- `sp_query_store_remove_query`


###  <a name="bkmk_ga_docs"></a> 제품 설명서(GA) 
 **문제 및 고객에게 미치는 영향:** SQL Server 2016 설명서의 다운로드 가능한 버전은 아직 제공되지 않습니다. 도움말 라이브러리 관리자를 사용하여 **온라인에서 콘텐츠를 설치**하려고 하면 SQL Server 2012 및 SQL Sever 2014 설명서가 표시되지만 SQL Server 2016 설명서에 대한 옵션은 없습니다.    
    
 **해결 방법:** 다음 해결 방법 중 하나를 사용하세요.    
    
 ![SQL Server에 대한 도움말 설정 구성](../sql-server/media/docs-sql2016-managehelpsettings.png "SQL Server에 대한 도움말 설정 구성")    
    
-   **온라인 또는 로컬 도움말 선택** 옵션을 사용하고 "온라인 도움말 사용"을 적용하도록 도움말을 구성합니다.    
    
-   **온라인에서 콘텐츠 설치** 옵션을 사용하고 SQL Server 2014 콘텐츠를 다운로드합니다.    
    
 **F1 도움말:** 기본적으로 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 F1 키를 누르면 F1 도움말 문서의 온라인 버전이 브라우저에 표시됩니다. 문제는 로컬 도움말을 구성하고 설치한 경우에도 브라우저 기반 도움말입니다. 
     
**콘텐츠 업데이트:**    
SQL Server Management Studio 및 Visual Studio에서 설명서를 추가하는 프로세스 중에 도움말 뷰어 응용 프로그램이 중단(정지)될 수 있습니다. 이 문제를 해결하려면 다음 단계를 완료하세요. 이 문제에 대한 자세한 내용은 [Visual Studio 도움말 뷰어가 중단됨](https://msdn.microsoft.com/library/mt654096.aspx)을 참조하세요.    
    
* 메모장에서 %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio14_en US.settings 파일을 열고 다음 코드의 날짜를 미래의 날짜로 변경합니다.    
    
     
```    
     Cache LastRefreshed="12/31/2017 00:00:00"    
``` 

## <a name="additional-information"></a>추가 정보
+ [SQL Server 2016 설치](../database-engine/install-windows/installation-for-sql-server-2016.md)
+ [SQL Server 업데이트 센터 - 지원되는 모든 버전에 대한 링크 및 정보](https://msdn.microsoft.com/library/ff803383.aspx)


[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]    

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png "MS_Logo_X-Small")    
