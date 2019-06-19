---
title: SQL Server 2016 Integration Services의 새로운 기능 | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 09/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 659059130d63dd2f320dcbd9ec0364b249f0889b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65713857"
---
# <a name="what39s-new-in-integration-services-in-sql-server-2016"></a>SQL Server 2016 Integration Services의 새로운 기능

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



이 항목에서는 SQL Server 2016 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 추가되거나 업데이트된 기능에 대해 설명합니다. 또한 SQL Server 2016 시간 프레임 동안 [Azure Feature Pack for Integration Services &#40;SSIS&#41;](../integration-services/azure-feature-pack-for-integration-services-ssis.md)에 포함되거나 업데이트된 기능도 포함됩니다.  

## <a name="new-for-ssis-in-azure-data-factory"></a>Azure Data Factory SSIS의 새로운 기능

2017년 9월 Azure Data Factory 버전 2의 공개 미리 보기에서 이제 다음과 같은 작업을 수행할 수 있습니다.
-   Azure SQL Database의 SSISDB(SSIS 카탈로그 데이터베이스)에 패키지를 배포합니다.
-   Azure SSIS Integration Runtime에서 Azure에 배포된 패키지 및 Azure Data Factory 버전 2의 구성 요소를 실행합니다.

자세한 내용은 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)를 참조하세요.

이러한 새로운 기능을 사용하려면 SSDT(SQL Server Data Tools) 버전 17.2 이상이 필요하지만, SQL Server 2017 또는 SQL Server 2016은 필요하지 않습니다. Azure에 패키지를 배포할 때 패키지 배포 마법사는 항상 패키지를 최신 패키지 형식으로 업그레이드합니다.

## <a name="2016-improvements-by-category"></a>범주별로 2016 향상된 기능  
  
-   **관리 효율**  
  
    -   배포 향상  
  
        -   [SSISDB 업그레이드 마법사](#ssisdbupgrwiz)  
  
        -   [SSIS 카탈로그에서 Always On 지원](#AlwaysOn)  
  
        -   [증분 패키지 배포](#IncrementalDeployment)  
  
        -   [SSIS 카탈로그에서 항상 암호화 지원](#encrypted)  
  
    -   디버깅 향상  
  
        -   [SSIS 카탈로그에서 새 ssis_logreader 데이터베이스 수준 역할](#LogReader)  
  
        -   [SSIS 카탈로그에서 새 RuntimeLineage 로깅 수준](#RuntimeLineage)  
  
        -   [SSIS 카탈로그에서 새 사용자 지정 로깅 수준](#CustomLogging)  
  
        -   [데이터 흐름의 오류에 대한 열 이름](#ErrorColumn)  
  
        -   [오류 열 이름에 대한 지원 확장](#getidstring)  
  
        -   [서버 차원의 기본 로깅 수준 지원](#ServerLogLevel)  
  
        -   [API의 새로운 IDTSComponentMetaData130 인터페이스](#CMD130)  
  
    -   패키지 관리 향상  
  
        -   [프로젝트 업그레이드에 대한 경험 향상](#ProjectUpgrade)  
  
        -   [AutoAdjustBufferSize 속성에서 데이터 흐름에 대한 버퍼 크기를 자동으로 계산](#BufferSize)  
  
        -   [재사용 가능한 제어 흐름 템플릿](#Templates)  
  
        -   [새 템플릿의 이름을 파트로 변경](#Parts)  
  
-   **연결**  
  
    -   온-프레미스에서 확장된 연결  
  
        -   [OData v4 데이터 원본 지원](#ODatav4)  
  
        -   [Excel 2013 데이터 원본에 대한 명시적 지원](#Excel2013)  
  
        -   [HDFS(Hadoop 파일 시스템) 지원](#HDFS)  
  
        -   [Hadoop과 HDFS에 대한 지원 확장](#more_hadoop)  
  
        -   [HDFS 파일 대상에 이제 ORC 파일 형식 지원](#hdfsORC)  
  
        -   [ODBC 구성 요소가 SQL Server 2016용으로 업데이트됨](#odbc2016)  
  
        -   [Excel 2016 데이터 원본에 대한 명시적 지원](#Excel2016)  
  
        -   [Connector for SAP BW for SQL Server 2016 릴리스됨](#SAPBW)
        
        -   [Oracle 및 Teradata용 Connectors v4.0 릴리스됨](#oracleteradata)
        
        -   [PDW(분석 플랫폼 시스템) 어플라이언스 업데이트 5용 커넥터 릴리스됨](#pdwau5)
  
    -   클라우드에 연결 확장  
  
        -   HDInsight에 대한 Azure Storage 커넥터 및 Hive 및 Pig 태스크 - [Azure Feature Pack for SSIS가 SQL Server 2016용으로 릴리스됨](#AFP2016)
        
        -   [서비스 팩 1에 릴리스된 Microsoft Dynamics 온라인 리소스에 대한 지원](#dynamics)
        
        -   [Azure Data Lake Store에 대한 지원이 릴리스됨](#datalakestore)
        
        -   [Azure SQL Data Warehouse에 대한 지원이 릴리스됨](#sqldwupload)
  
-   **유용성 및 생산성**  
  
    -   설치 경험 향상  
  
        -   [SSISDB가 가용성 그룹에 속해 있을 경우 업그레이드 차단](#Upgrade)  
  
    -   디자인 환경 향상  
  
        -   [SSIS 디자이너에서 SQL Server 2016, 2014 또는 2012에 대한 패키지를 만들고 유지 관리](#OneDesigner)  
  
        -   여러 디자이너 향상 및 버그 수정  
  
    -   SQL Server Management Studio의 환경 관리 향상
  
        -   [SSIS 카탈로그 뷰에 대한 성능 향상](#CatViews)  
  
    -   기타 향상된 기능  
  
        -   [분산 데이터 배포자 변환이 이제 SSIS에 속함](#BDDinbox)  
  
        -   [데이터 피드 게시 구성 요소가 이제 SSIS에 속함](#ComplexFeedinbox)  
  
        -   [SQL Server 가져오기 및 내보내기 마법사에서 Azure Blob Storage에 대한 지원](#AzureBlob)  
  
        -   [Microsoft SQL Server 2016용 Change Data Capture Designer 및 Service for Oracle이 릴리스됨](#CDCOracle)  
  
        -   [CDC 구성 요소가 SQL Server 2016용으로 업데이트됨](#cdc2016)  
  
        -   [Analysis Services DDL 실행 태스크가 업데이트됨](#ASDDL)  
  
        -   [Analysis Services 작업에서 테이블 형식 모델 지원](#ssasrc0)  
  
        -   [기본 제공 R 서비스에 대한 지원](#builtinR)  
  
        -   [XML 태스크에서 풍부한 XML 유효성 검사 출력](#ValidateXML)  
  
## <a name="manageability"></a>관리 효율  

### <a name="better-deployment"></a>배포 향상

####  <a name="ssisdbupgrwiz"></a> SSISDB 업그레이드 마법사  
 데이터베이스가 SQL Server 인스턴스의 최신 버전보다 오래된 상태이면 SSISDB 업그레이드 마법사를 사용하여 SSIS 카탈로그 데이터베이스인 SSISDB를 업그레이드합니다. 다음 조건 중 하나에 해당하는 경우 이 업그레이드를 수행합니다.  
  
-   이전 버전의 SQL Server에서 데이터베이스를 복원한 경우  
  
-   SQL Server 인스턴스를 업그레이드하기 전에 Always On 가용성 그룹에서 데이터베이스를 제거하지 않은 경우. 이 경우 데이터베이스가 자동으로 업그레이드되지 않습니다. 자세한 내용은 [Upgrading SSISDB in an availability group](../integration-services/catalog/ssis-catalog.md#Upgrade)를 참조하십시오.  
  
 자세한 내용은 [SSIS 카탈로그&#40;SSISDB&#41;](../integration-services/catalog/ssis-catalog.md)를 참조하세요. 

####  <a name="AlwaysOn"></a> SSIS 카탈로그에서 Always On 지원  
 Always On 가용성 그룹 기능은 데이터베이스 미러링에 대한 엔터프라이즈 수준의 대안을 제공하는 고가용성 및 재해 복구 솔루션입니다. 가용성 그룹은 함께 장애 조치(Failover)되는 사용자 데이터베이스(가용성 데이터베이스라고 함)의 불연속 집합에 대한 장애 조치(Failover) 환경을 지원합니다. 자세한 내용은 [AlwaysOn 가용성 그룹](../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)을 참조하세요.  
  
 SQL Server 2016에서 SSIS에는 중앙 집중식 SSIS 카탈로그(즉, SSISDB 사용자 데이터베이스)로 쉽게 배포할 수 있는 기능이 새로 도입되었습니다. SSIS 데이터베이스 및 해당 콘텐츠(프로젝트, 패키지, 실행 로그 등)에 대한 고가용성을 제공하려는 경우에는 다른 사용자 데이터베이스와 같은 방식으로 SSISDB 데이터베이스를 AlwaysOn 가용성 그룹에 추가할 수 있습니다. 장애 조치(Failover)가 발생하면 보조 노드 중 하나가 자동으로 새 주 노드가 됩니다.  
  
 SSISDB용으로 AlwaysOn을 사용하도록 설정하는 단계별 지침과 상세 개요는 [SSIS 카탈로그](../integration-services/catalog/ssis-catalog.md)를 참조하세요.  

####  <a name="IncrementalDeployment"></a> 증분 패키지 배포  
증분 패키지 배포 기능을 사용하면 전체 프로젝트를 배포하지 않고 기존 프로젝트나 새 프로젝트에 하나 이상의 패키지를 배포할 수 있습니다. 다음과 같은 도구를 사용하여 증분 방식으로 패키지를 배포할 수 있습니다.  
  
-   배포 마법사  
  
-   SQL Server Management Studio(배포 마법사 사용)  
  
-   SQL Server Data Tools(Visual Studio)(배포 마법사도 사용)  
  
-   저장 프로시저  
  
-   MOM(관리 개체 모델) API  
  
 자세한 내용은 [Integration Services(SSIS) 프로젝트 및 패키지 배포](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)를 참조하세요.  

####  <a name="encrypted"></a> SSIS 카탈로그에서 항상 암호화 지원  
 SSIS는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 항상 암호화 기능을 이미 지원합니다. 자세한 내용은 다음 블로그 게시물을 참조하세요.  
  
-   [SSIS의 항상 암호화 기능](https://blogs.msdn.com/b/ssis/archive/2015/12/18/ssis-with-always.aspx)  
  
-   [항상 암호화된 조회 변환](https://blogs.msdn.com/b/ssis/archive/2015/12/18/lookup-transformation-with-always-encrypted.aspx)  

### <a name="better-debugging"></a>디버깅 향상

####  <a name="LogReader"></a> SSIS 카탈로그에서 새 ssis_logreader 데이터베이스 수준 역할  
 이전 버전의 SSIS 카탈로그에서는 역할이 **ssis_admin** 인 사용자만 로깅 출력이 포함된 보기에 액세스할 수 있습니다. 이제 새 **ssis_logreader** 데이터베이스 수준 역할을 사용하여 관리자가 아닌 사용자가 로깅 출력이 포함된 보기에 액세스할 수 있는 권한을 부여할 수 있습니다.  
  
 **ssis_monitor** 역할도 새로 추가되었습니다. 이 역할은 AlwaysOn을 지원하며 SSIS 카탈로그에 의해서만 내부에서 사용됩니다.  

####  <a name="RuntimeLineage"></a> SSIS 카탈로그에서 새 RuntimeLineage 로깅 수준  
 SSIS 카탈로그에서 새 **RuntimeLineage** 로깅 수준에서는 데이터 흐름의 계보 정보를 추적하는 데 필요한 데이터를 수집합니다. 이 계보 정보를 구문 분석하여 작업 간의 계보 관계를 매핑할 수 있습니다. ISV와 개발자가 이 정보로 사용자 지정 계보 매핑 도구를 빌드할 수 있습니다. 

####  <a name="CustomLogging"></a> SSIS 카탈로그에서 새 사용자 지정 로깅 수준  
 SSIS 카탈로그의 이전 버전을 사용하면 패키지를 실행할 때 다음 네 가지 기본 제공 로깅 수준에서 선택할 수 있습니다. **없음, 기본, 성능 또는 자세한 정보**. SQL Server 2016에서는 **RuntimeLineage** 로깅 수준을 추가합니다. 또한 이제 SSIS 카탈로그에서 사용자 지정된 로깅 수준을 여러 개 만들고 저장할 수 있으며, 패키지를 실행할 때마다 사용할 로깅 수준을 선택할 수 있습니다. 각 사용자 지정된 로깅 수준에 대해 캡처할 통계 및 이벤트를 선택합니다. 필요에 따라 변수 값, 연결 문자열 및 작업 속성을 표시하는 이벤트 컨텍스트를 포함합니다. 자세한 내용은 [SSIS 서버에서 패키지 실행에 대한 로깅 설정](../integration-services/performance/integration-services-ssis-logging.md#server_logging)를 참조하십시오. 

####  <a name="ErrorColumn"></a> 데이터 흐름의 오류에 대한 열 이름  
 오류 출력에 오류를 포함 하는 데이터 흐름에서 행을 리디렉션하는 경우 출력 오류가 발생 했지만 열 이름이 표시 되지 않는 열에 대 한 숫자 식별자를 포함 합니다. 이제 여러 가지 방법을 사용하여 오류가 발생할 때 열 이름을 찾아 표시할 수 있습니다.  
  
-   로깅을 구성할 때 로깅에 대해 **DiagnosticEx** 이벤트를 선택합니다. 이 이벤트는 로그에 데이터 흐름 열 지도를 작성합니다. 그런 다음 오류 출력에 의해 캡처된 열 식별자를 사용하여 이 열 지도에 열 이름을 조회할 수 있습니다. 자세한 내용은 [데이터 오류 처리](../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.  
  
-   고급 편집기에서 데이터 흐름 구성 요소의 입력 또는 출력 열 속성을 볼 때 업스트림 열에 대한 열 이름을 볼 수 있습니다.  
  
-   오류가 발생한 열의 이름을 보려면 오류 출력에 데이터 뷰어를 연결합니다.  데이터 뷰어는 이제 오류 설명 및 오류가 발생 한 열의 이름을 표시합니다.  
  
-   스크립트 구성 요소 또는 사용자 지정 데이터 흐름 구성 요소에서 IDTSComponentMetadata100 인터페이스의 새 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> 메서드를 호출합니다.  
  
 이러한 개선에 대한 자세한 내용은 SSIS 개발자 Bo Fan의 다음 블로그 게시물을 참조하세요. [SSIS 데이터 흐름에 대한 오류 열 개선](https://blogs.msdn.com/b/ssis/archive/2015/11/27/error-column-improvement-for-ssis-data-flow.aspx).  
  
> [!NOTE]  
>  (이 지원은 후속 릴리스에서 확장되었습니다. 자세한 내용은 [오류 열 이름에 대한 지원 확장](#getidstring) 및 [API의 새로운 IDTSComponentMetaData130 인터페이스](#CMD130)를 참조하세요.)  

####  <a name="getidstring"></a> 오류 열 이름에 대한 지원 확장  
 **DiagnosticEx** 이벤트에서는 계보 열뿐만 아니라 이제 모든 입력 및 출력 열에 대한 열 정보를 기록합니다. 따라서 이제는 파이프라인 계보 맵 대신 파이프라인 열 매핑 출력이라고 합니다.  
  
 GetIdentificationStringByLineageID 메서드 이름이 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A>에서 추가되거나 업데이트된 기능에 대해 설명합니다. 자세한 내용은 [데이터 흐름의 오류에 대한 열 이름](#ErrorColumn)를 참조하십시오.  
  
 이러한 변경 및 오류 열 개선에 대한 자세한 내용은 업데이트된 다음 블로그 게시물을 참조하세요. [Error Column Improvements for SSIS Data Flow (Updated for CTP3.3)](https://blogs.msdn.com/b/ssis/archive/2015/11/27/error-column-improvement-for-ssis-data-flow.aspx)  
  
> [!NOTE]  
>  RC0에서 이 메서드는 새 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130> 인터페이스로 이동되었습니다. 자세한 내용은 [API의 새로운 IDTSComponentMetaData130 인터페이스](#CMD130)를 참조하세요.  

####  <a name="ServerLogLevel"></a> 서버 차원의 기본 로깅 수준 지원  
 SQL Server **서버 속성**의 **서버 로깅 수준** 속성 아래에서 이제 기본 서버 차원의 로깅 수준을 선택할 수 있습니다. 기본 제공 로깅 수준인 기본, 없음, 자세한 정보 표시, 성능 또는 런타임 계보 중 하나에서 선택하거나 기존 사용자 지정된 로깅 수준을 선택할 수 있습니다. 선택한 로깅 수준은 SSIS 카탈로그에 배포하는 모든 패키지에 적용됩니다. 또한 SSIS 패키지를 실행하는 SQL 에이전트 작업 단계에 기본적으로 적용됩니다.  

####  <a name="CMD130"></a> API의 새로운 IDTSComponentMetaData130 인터페이스  
 SSIS 카탈로그에서 새 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130> 인터페이스는 SQL Server 2016의 새 기능, 특히 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 메서드를 기존 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> 인터페이스에 추가합니다. (**GetIdentificationStringByID** 메서드는 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 인터페이스에서 새 인터페이스로 이동되었습니다.) 또한 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInputColumn130> 및 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn130> 인터페이스도 새로 추가되었으며 두 인터페이스 모두 **LineageIdentificationString** 속성을 제공합니다. 자세한 내용은 [데이터 흐름의 오류에 대한 열 이름](#ErrorColumn)를 참조하십시오.  

### <a name="better-package-management"></a>패키지 관리 향상

####  <a name="ProjectUpgrade"></a> 프로젝트 업그레이드에 대한 경험 향상  
 SSIS 프로젝트를 이전 버전에서 현재 버전으로 업그레이드할 때 프로젝트 수준 연결 관리자는 예상한 대로 작업을 계속 수행하고 패키지 레이아웃 및 주석은 유지됩니다.  

####  <a name="BufferSize"></a> AutoAdjustBufferSize 속성에서 데이터 흐름에 대한 버퍼 크기를 자동으로 계산  
 새 **AutoAdjustBufferSize** 속성 값을 **true**로 설정하면 데이터 흐름 엔진에서 데이터 흐름에 대한 버퍼 크기를 자동으로 계산합니다. 자세한 내용은 [Data Flow Performance Features](../integration-services/data-flow/data-flow-performance-features.md)를 참조하십시오.  

####  <a name="Templates"></a> 재사용 가능한 제어 흐름 템플릿  
 일반적으로 사용되는 제어 흐름 태스크 또는 컨테이너를 독립 실행형 템플릿 파일에 저장하고 제어 흐름 템플릿을 사용하여 이 파일을 프로젝트의 하나 이상의 패키지에 여러 번 재사용합니다. 이 재사용 기능으로 인해 SSIS 패키지 디자인 및 유지 관리가 좀 더 간편해집니다. 자세한 내용은 [제어 흐름 패키지 파트를 사용하여 패키지에 대해 제어 흐름 재사용](../integration-services/reuse-control-flow-across-packages-by-using-control-flow-package-parts.md)을 참조하세요.  

####  <a name="Parts"></a> 새 템플릿의 이름을 파트로 변경  
 CTP 3.0에서 새로 릴리스된 재사용 가능 제어 흐름 템플릿 이름이 제어 흐름 파트나 패키지 파트로 바뀌었습니다. 이 기능에 대한 자세한 내용은 [제어 흐름 패키지 파트를 사용하여 패키지에 대해 제어 흐름 재사용](../integration-services/reuse-control-flow-across-packages-by-using-control-flow-package-parts.md)을 참조하세요.  

## <a name="connectivity"></a>연결  

### <a name="expanded-connectivity-on-premises"></a>온-프레미스에서 확장된 연결

####  <a name="ODatav4"></a> OData v4 데이터 원본 지원  
 OData 원본 및 OData 연결 관리자는 이제 OData v3 및 v4 프로토콜을 지원합니다.  
  
-   OData V3 프로토콜의 경우 구성 요소는 ATOM 및 JSON 데이터 형식을 지원합니다.  
  
-   OData V4 프로토콜의 경우 구성 요소는 JSON 데이터 형식을 지원합니다.  
  
 자세한 내용은 [OData Source](../integration-services/data-flow/odata-source.md)를 참조하십시오.  

####  <a name="Excel2013"></a> Excel 2013 데이터 원본에 대한 명시적 지원  
 Excel 연결 관리자, Excel 원본 및 Excel 대상, SQL Server 가져오기 및 내보내기 마법사가 이제 Excel 2013 데이터 원본에 대한 명시적 지원을 제공합니다. 

####  <a name="HDFS"></a> HDFS(Hadoop 파일 시스템) 지원  
 HDFS 지원에는 연결 관리자가 포함되어 있어 일반적인 HDFS 작업을 수행할 수 있도록 Hadoop 클러스터 및 작업에 연결합니다. 자세한 내용은 [Integration Services(SSIS)에서 Hadoop 및 HDFS 지원&#40;SSIS&#41;](../integration-services/hadoop-and-hdfs-support-in-integration-services-ssis.md)을 참조하세요.  

####  <a name="more_hadoop"></a> Hadoop과 HDFS에 대한 지원 확장  
  
-   Hadoop 연결 관리자는 이제 Basic과 Kerberos 인증을 지원합니다. 자세한 내용은 [Hadoop Connection Manager](../integration-services/connection-manager/hadoop-connection-manager.md)를 참조하십시오.  
  
-   HDFS 파일 원본 및 HDFS 파일 대상이 이제 텍스트와 Avro 형식을 모두 지원합니다. 자세한 내용은  [HDFS File Source](../integration-services/data-flow/hdfs-file-source.md) 및  [HDFS File Destination](../integration-services/data-flow/hdfs-file-destination.md)을 참조하세요.  
  
-   이제 Hadoop 파일 시스템 태스크는 CopyToHadoop 및 CopyFromHadoop 옵션 외에도 CopyWithinHadoop 옵션을 지원합니다. 자세한 내용은 [Hadoop File System Task](../integration-services/control-flow/hadoop-file-system-task.md)를 참조하십시오.  

####  <a name="hdfsORC"></a> HDFS 파일 대상에 이제 ORC 파일 형식 지원  
 HDFS 파일 대상에서는 이제 텍스트 및 Avro 외에도 ORC 파일 형식을 지원합니다. (HDFS 파일 원본은 텍스트 및 Avro만 지원합니다.) 이 구성 요소에 대한 자세한 내용은 [HDFS File Destination](../integration-services/data-flow/hdfs-file-destination.md)을 참조하세요.  

####  <a name="odbc2016"></a> ODBC 구성 요소가 SQL Server 2016용으로 업데이트됨  
 ODBC 원본 및 대상 구성 요소가 SQL Server 2016과의 완벽한 호환성을 제공할 수 있도록 업데이트되었습니다. 새로운 기능은 없고 동작에서 변경된 사항도 없습니다.  

####  <a name="Excel2016"></a> Excel 2016 데이터 원본에 대한 명시적 지원  
 Excel 연결 관리자, Excel 원본 및 Excel 대상에서 이제 Excel 2016 데이터 원본에 대한 명시적 지원을 제공합니다.  

####  <a name="SAPBW"></a> Connector for SAP BW for SQL Server 2016 릴리스됨  
 MicrosoftÂ® Connector for SAP BW for Microsoft SQL ServerÂ® 2016이 SQL Server 2016 Feature Pack의 일부로 릴리스되었습니다. 기능 팩의 구성 요소를 다운로드하려면 [MicrosoftÂ® SQL ServerÂ® 2016 Feature Pack](https://go.microsoft.com/fwlink/?LinkID=746297)(MicrosoftÂ® SQL ServerÂ® 2016 기능 팩)을 참조하세요.
 
#### <a name="oracleteradata"></a> Oracle 및 Teradata용 Connectors v4.0 릴리스됨
Oracle 및 Teradata용 Microsoft Connectors v4.0이 릴리스되었습니다. 커넥터를 다운로드하려면 [Microsoft Connectors v4.0 for Oracle and Teradata](https://www.microsoft.com/download/details.aspx?id=52950)(Oracle 및 Teradata용 Microsoft Connectors v4.0)를 참조하세요.

### <a name="pdwau5"></a> PDW(분석 플랫폼 시스템) 어플라이언스 업데이트 5용 커넥터 릴리스됨
PDW AU5로 데이터를 로드하기 위한 대상 어댑터가 릴리스되었습니다. 어댑터를 다운로드하려면 [분석 플랫폼 시스템 어플라이언스 업데이트 5 설명서 및 클라이언트 도구](https://www.microsoft.com/download/details.aspx?id=51610) 를 참조하세요.

### <a name="expanded-connectivity-to-the-cloud"></a>클라우드에 연결 확장

####  <a name="AFP2016"></a> Azure Feature Pack for SSIS가 SQL Server 2016용으로 릴리스됨  
 Integration Services용 Azure Feature Pack이 SQL Server 2016용으로 릴리스되었습니다. 기능 팩에는 연결 관리자가 포함되어 있어 일반적인 Azure 작업을 수행할 수 있도록 Azure 데이터 원본 및 작업에 연결합니다. 자세한 내용은 [Integration Services용 Azure 기능 팩&#40;SSIS&#41;](../integration-services/azure-feature-pack-for-integration-services-ssis.md)을 참조하세요.  

#### <a name="dynamics"></a> 서비스 팩 1에 릴리스된 Microsoft Dynamics 온라인 리소스에 대한 지원

SQL Server 2016 서비스 팩 1을 설치하면 이제 OData 원본 및 OData 연결 관리자가 Microsoft Dynamics AX Online 및 Microsoft Dynamics CRM Online의 OData 피드에 연결할 수 있습니다.

#### <a name="datalakestore"></a> Azure Data Lake Store에 대한 지원이 릴리스됨

최신 버전의 Azure 기능 팩에는 연결 관리자, Azure Data Lake Store에서 데이터를 이동할 원본 및 대상이 포함되어 있습니다. 자세한 내용은 [Integration Services용 Azure 기능 팩&#40;SSIS&#41;](../integration-services/azure-feature-pack-for-integration-services-ssis.md)을 참조하세요.

#### <a name="sqldwupload"></a>SSMS의 Azure SQL Data Warehouse 지원

최신 버전의 Azure 기능 팩에는 SQL Data Warehouse를 데이터로 채우기 위한 Azure SQL DW 업로드 작업이 포함되어 있습니다. 자세한 내용은 [Integration Services용 Azure 기능 팩&#40;SSIS&#41;](../integration-services/azure-feature-pack-for-integration-services-ssis.md)을 참조하세요.

## <a name="usability-and-productivity"></a>유용성 및 생산성  
 
### <a name="better-install-experience"></a>설치 경험 향상

####  <a name="Upgrade"></a> SSISDB가 가용성 그룹에 속해 있을 경우 업그레이드 차단  
 SSISDB(SSIS 카탈로그 데이터베이스)가 Always On 가용성 그룹에 속한 경우에는 가용성 그룹에서 SSISDB를 제거하고 SQL Server를 업그레이드한 다음 가용성 그룹에 SSISDB를 다시 추가해야 합니다. 자세한 내용은 [Upgrading SSISDB in an availability group](../integration-services/catalog/ssis-catalog.md#Upgrade)를 참조하십시오.  

### <a name="better-design-experience"></a>디자인 환경 향상

####  <a name="OneDesigner"></a> SSIS 디자이너에서 멀티 타기팅 및 다중 버전 지원  
 이제 Visual Studio 2015용 SSDT(SQL Server Data Tools)에서 SSIS 디자이너를 사용하여 SQL Server 2016, SQL Server 2014 또는 SQL Server 2012를 대상으로 하는 패키지를 만들고, 유지 관리하고, 실행할 수 있습니다. SSDT를 다운로드하려면 [최신 SQL Server Data Tools 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요. 

 솔루션 탐색기에서 Integration Services 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택하여 프로젝트에 대한 속성 페이지를 엽니다. **구성 속성** 의 **일반**탭에서 **TargetServerVersion** 속성을 선택하고 SQL Server 2016, SQL Server 2014 또는 SQL Server 2012를 선택합니다.  
   
 ![프로젝트 속성 대화 상자의 TargetServerVersion 속성](../integration-services/media/targetserverversion2.png "프로젝트 속성 대화 상자의 TargetServerVersion 속성")  

> [!IMPORTANT]
> SSIS용 사용자 지정 확장 프로그램을 개발하는 경우 [사용자 지정 구성 요소에서 멀티 타기팅 지원](../integration-services/extending-packages-custom-objects/support-multi-targeting-in-your-custom-components.md) 및 [SQL Server 2016용 SSDT 2015의 다중 버전 지원에서 SSIS 사용자 지정 확장 프로그램을 지원하도록 설정](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/) 을 참조하세요.  

### <a name="better-management-experience-in-sql-server-management-studio"></a>SQL Server Management Studio의 환경 관리 향상

####  <a name="CatViews"></a> SSIS 카탈로그 뷰에 대한 성능 향상  
 대부분의 SSIS 카탈로그 뷰는 ssis_admin 역할의 구성원인 사용자가 실행할 때 성능이 향상됩니다.  

### <a name="other-enhancements"></a>기타 향상된 기능

####  <a name="BDDinbox"></a> 분산 데이터 배포자 변환이 이제 SSIS에 속함  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 이전 버전에서 별도 다운로드가 필요했던 균형 있는 데이터 배포자 변환이 이제 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]를 설치할 때 함께 설치됩니다. 자세한 내용은 [Balanced Data Distributor Transformation](../integration-services/data-flow/transformations/balanced-data-distributor-transformation.md)를 참조하십시오.  
  
####  <a name="ComplexFeedinbox"></a> 데이터 피드 게시 구성 요소가 이제 SSIS에 속함  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 이전 버전에서 별도 다운로드가 필요했던 데이터 피드 게시 구성 요소가 이제 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]를 설치할 때 함께 설치됩니다. 자세한 내용은 [Data Streaming Destination](../integration-services/data-flow/data-streaming-destination.md)를 참조하십시오.  

####  <a name="AzureBlob"></a> SQL Server 가져오기 및 내보내기 마법사에서 Azure Blob Storage에 대한 지원  
 SQL Server 가져오기 및 내보내기 마법사에서 이제 Azure Blob Storage에서 데이터를 가져오고, Azure Blob Storage에 데이터를 저장합니다. 자세한 내용은 [데이터 원본 선택&#40;SQL Server 가져오기 및 내보내기 마법사&#41;](../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md) 및 [대상 선택&#40;SQL Server 가져오기 및 내보내기 마법사&#41;](../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)을 참조하세요. 

####  <a name="CDCOracle"></a> Microsoft SQL Server 2016용 Change Data Capture Designer 및 Service for Oracle이 릴리스됨  
 Microsoft SQL ServerÂ® 2016용 MicrosoftÂ® Change Data Capture Designer and Service for Oracle by Attunity가 SQL Server 2016 Feature Pack의 일부로 릴리스되었습니다.  이제 이러한 구성 요소는 클래식 설치에서 Oracle 12c를 지원합니다. 다중 테넌트 설치는 지원되지 않습니다. Feature Pack의 구성 요소를 다운로드하려면 [MicrosoftÂ® SQL ServerÂ® 2016 Feature Pack](https://go.microsoft.com/fwlink/?LinkID=746297)을 참조하세요.  
  
####  <a name="cdc2016"></a> CDC 구성 요소가 SQL Server 2016용으로 업데이트됨  
 CDC(변경 데이터 캡처) 제어 작업, 원본, 분할자 변환 구성 요소가 SQL Server 2016과의 완벽한 호환성을 제공할 수 있도록 업데이트되었습니다. 새로운 기능은 없고 동작에서 변경된 사항도 없습니다.  
  
####  <a name="ASDDL"></a> Analysis Services DDL 실행 태스크가 업데이트됨  
 테이블 형식 모델 스크립팅 언어 명령에 동의하도록 Analysis Services DDL 실행 태스크가 업데이트되었습니다.

####  <a name="ssasrc0"></a> Analysis Services 작업에서 테이블 형식 모델 지원  
 SQL Server 2016 테이블 형식 모델에서 SSAS(SQL Server Analysis Services)를 지원하는 SSIS 작업 및 대상을 이제 모두 사용할 수 있습니다. 다차원 개체 대신 테이블 형식 개체를 나타낼 수 있도록 SSIS 작업이 업데이트되었습니다. 예를 들어 처리할 개체를 선택하면 Analysis Services 처리 태스크에서는 자동으로 테이블 형식 모델을 검색하고 측정값 그룹 및 차원 대신 테이블 형식 개체의 목록이 표시됩니다. 파티션 처리 대상도 이제 테이블 형식 개체를 표시하고 파티션으로 데이터를 푸시하는 기능을 지원합니다.  
  
 차원 처리 대상은 SQL 2016 호환성 수준을 사용하는 테이블 형식 모델에 대해서는 작동하지 않습니다.  Analysis Services 처리 태스크 및 파티션 처리 대상만 있으면 테이블 형식 처리가 가능합니다. 

####  <a name="builtinR"></a> 기본 제공 R 서비스에 대한 지원  
 SSIS에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 기본 제공 R 서비스를 이미 지원합니다. 데이터를 추출하고 분석 출력을 로드하는 것뿐 아니라 R 모델을 빌드, 실행하고 주기적으로 보존하기 위해 SSIS를 사용할 수 있습니다. 자세한 내용은 다음 로그 게시물을 참조하세요. [SQL Server 2016 SSIS 및 R 서비스를 사용하여 기계 학습 프로젝트 운영](https://blogs.msdn.com/b/ssis/archive/2016/01/12/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services.aspx)합니다. 

####  <a name="ValidateXML"></a> XML 태스크에서 풍부한 XML 유효성 검사 출력  
 XML 태스크의 **ValidationDetails** 속성을 사용하도록 설정하여 XML 문서의 유효성을 검사하고 풍부한 오류 출력을 가져올 수 있습니다. **ValidationDetails** 속성을 사용할 수 있게 되기 전에 먼저 XML 태스크에 의해 수행된 XML 유효성 검사가 오류 또는 해당 위치에 대한 정보 없이 true 또는 false 결과만 반환했습니다. 이제 **ValidationDetails** 를 true로 설정할 경우 출력 파일에는 줄 번호 및 위치를 포함하여 모든 오류에 대한 자세한 정보가 포함됩니다. 이 정보를 사용하여 XML 문서의 오류를 이해하고, 찾고, 수정할 수 있습니다. 자세한 내용은 [Validate XML with the XML Task](../integration-services/control-flow/validate-xml-with-the-xml-task.md)를 참조하십시오.  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] 는 **서비스 팩 2에** ValidationDetails [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 속성을 도입했습니다. 이 새 속성은 당시에는 발표되거나 문서화되지 않았습니다. **ValidationDetails** 속성은 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 및 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]에서도 사용할 수 있습니다.   

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

## <a name="see-also"></a>참고 항목  
 [SQL Server 2016의 새로운 기능](../sql-server/what-s-new-in-sql-server-2016.md)   
 [SQL Server 2016의 버전과 지원하는 기능](../sql-server/editions-and-supported-features-for-sql-server-2016.md)
