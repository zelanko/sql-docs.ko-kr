---
description: SQL Server 2017 Integration Services의 새로운 기능
title: SQL Server 2017 Integration Services의 새로운 기능 | Microsoft Docs
ms.custom: ''
ms.date: 09/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3275ee19e271c6d9d98e7ad432ad3a772283b583
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "92193728"
---
# <a name="what39s-new-in-integration-services-in-sql-server-2017"></a>SQL Server 2017 Integration Services의 새로운 기능

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


이 토픽에서는 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 추가되거나 업데이트된 기능에 대해 설명합니다.

> [!NOTE]
> 또한 SQL Server 2017에는 SQL Server 2016의 기능과 SQL Server 2016 업데이트에 추가된 기능도 포함되어 있습니다. SQL Server 2016의 새로운 SSIS기능에 대한 자세한 내용은 [SQL Server 2016 Integration Services의 새로운 기능](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)을 참조하세요.

## <a name="highlights-of-this-release"></a>이 릴리스의 주요 내용

다음은 SQL Server 2017 Integration Services에서 가장 중요한 새로운 기능입니다.

-   **Scale Out** - SSIS 패키지 실행을 여러 작업자 컴퓨터에 더 쉽게 배포하고, 단일 마스터 컴퓨터에서 실행 및 작업자를 관리할 수 있습니다. 자세한 내용은 [Integration Services Scale Out](../integration-services/scale-out/integration-services-ssis-scale-out.md)을 참조하세요.

-   **Linux의 Integration Services** - Linux 컴퓨터에서 SSIS 패키지를 실행합니다. 자세한 내용은 [Linux에서 SSIS를 사용하여 데이터 추출, 변환 및 로드](../linux/sql-server-linux-migrate-ssis.md)를 참조하세요.

-   **향상된 연결성** - 업데이트된 OData 구성 요소를 사용하여 Microsoft Dynamics AX Online 및 Microsoft Dynamics CRM Online의 OData 피드에 연결합니다. 

## <a name="new-in-azure-data-factory"></a>Azure Data Factory의 새로운 기능

2017년 9월 Azure Data Factory 버전 2의 공개 미리 보기에서 이제 다음과 같은 작업을 수행할 수 있습니다.
-   Azure SQL Database의 SSISDB(SSIS 카탈로그 데이터베이스)에 패키지를 배포합니다.
-   Azure SSIS Integration Runtime에서 Azure에 배포된 패키지 및 Azure Data Factory 버전 2의 구성 요소를 실행합니다.

자세한 내용은 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)를 참조하세요.

이러한 새로운 기능을 사용하려면 SSDT(SQL Server Data Tools) 버전 17.2 이상이 필요하지만, SQL Server 2017 또는 SQL Server 2016은 필요하지 않습니다. Azure에 패키지를 배포할 때 패키지 배포 마법사는 항상 패키지를 최신 패키지 형식으로 업그레이드합니다.

## <a name="new-in-the-azure-feature-pack"></a>Azure Feature Pack의 새로운 기능

Azure용 Integration Services 기능 팩에는 SQL Server의 향상된 연결성 외에도 Azure Data Lake Store에 대한 지원이 추가되었습니다. 자세한 내용은 [ADLS 연결성을 강화하는 새로운 Azure Feature Pack 릴리스](https://blogs.msdn.microsoft.com/ssis/2017/08/29/new-azure-feature-pack-release-strengthening-adls-connectivity/) 블로그 게시물을 참조하세요. [Integration Services(SSIS)용 Azure Feature Pack](azure-feature-pack-for-integration-services-ssis.md)도 참조하세요.

## <a name="new-in-sql-server-data-tools-ssdt"></a>SSDT(SQL Server Data Tools)의 새로운 기능

이제 Visual Studio 2017 또는 Visual Studio 2015에서 SQL Server 버전 2012-2017을 대상으로 하는 SSIS 프로젝트 및 패키지를 개발할 수 있습니다. 자세한 내용은 [SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요.

## <a name="new-in-ssis-in-sql-server-2017-rc1"></a>SQL Server 2017 RC1 SSIS의 새로운 기능

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>SSIS Scale Out의 새로운 기능 및 변경된 기능

-   Scale Out Master에서 이제 고가용성을 지원합니다. SSISDB용 Always On을 사용하도록 설정하고, Scale Out 마스터 서비스를 호스팅하는 서버에 대한 Windows Server 장애 조치 클러스터링을 설정할 수 있습니다. 이 변경된 기능을 Scale Out 마스터에 적용하면 단일 장애 지점을 방지하고 전체 Scale Out 배포에 고가용성을 제공할 수 있습니다.
-   Scale Out Worker에서 실행 로그의 장애 조치(failover) 처리가 향상되었습니다. Scale Out 작업자가 예기치 않게 중지되는 경우 실행 로그가 로컬 디스크에 유지됩니다. 나중에 작업자가 다시 시작되면 지속형 로그를 다시 로드하고 SSISDB에 계속 저장합니다.
-   일관성과 가독성을 향상하기 위해 저장 프로시저 **[catalog].[create_execution]** 의 *runincluster* 매개 변수 이름이 *runinscaleout* 으로 변경되었습니다. 이러한 매개 변수 이름의 변경으로 인해 미치는 영향은 다음과 같습니다.
    -   Scale Out에서 패키지를 실행하는 기존 스크립트가 있는 경우 매개 변수 이름을 *runincluster* 에서 *runinscaleout* 으로 변경해야만 RC1에서 스크립트가 작동합니다.
    -   SSMS(SQL Server Management Studio) 17.1 및 이전 버전은 RC1의 Scale Out에서 패키지 실행을 트리거할 수 없습니다. 오류 메시지: “ *@runincluster* 은(는) 프로시저 **create_execution** 의 매개 변수가 아닙니다.” 이 문제는 다음 릴리스인 SSMS 버전 17.2에서 해결됩니다. SSMS 17.2 이상 버전은 Scale Out에서 새 매개 변수 이름 및 패키지 실행을 지원합니다. 해결 방법으로, SSMS 버전 17.2를 제공할 때까지 기존 버전의 SSMS를 사용하여 패키지 실행 스크립트를 생성한 다음 스크립트에서 *runincluster* 매개 변수의 이름을 *runinscaleout* 으로 변경하여 해당 스크립트를 실행하면 됩니다.
-   SSIS 카탈로그에 SSIS 패키지를 실행하기 위한 기본 모드를 지정하는 새 전역 속성이 있습니다. 이 새 속성은 null로 설정된 *runinscaleout* 매개 변수를 사용하여 **[catalog].[create_execution]** 저장 프로시저를 호출할 때 적용됩니다. 이 모드는 SSIS SQL 에이전트 작업에도 적용됩니다. SSMS의 SSISDB 노드에 대한 [속성] 대화 상자에서 또는 다음 명령을 사용하여 새 전역 속성을 설정할 수 있습니다.
    ```sql
    EXEC [catalog].[configure_catalog] @property_name=N'DEFAULT_EXECUTION_MODE', @property_value=1
    ```

## <a name="new-in-ssis-in-sql-server-2017-ctp-21"></a>SQL Server 2017 CTP 2.1 SSIS의 새로운 기능

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>SSIS Scale Out의 새로운 기능 및 변경된 기능

-   이제 Scale Out에서 실행을 트리거할 때 **Use32BitRuntime** 매개 변수를 사용할 수 있습니다.
-   Scale Out의 패키지 실행에 대해 SSISDB에 로깅하는 성능이 향상되었습니다. 이제 이벤트 메시지 및 메시지 컨텍스트 로그가 하나씩 기록되는 대신 일괄 처리 모드로 SSISDB에 기록됩니다. 이 향상된 기능에 대한 몇 가지 추가 참고 사항은 다음과 같습니다.        
    - SSMS(SQL Server Management Studio) 현재 버전의 일부 보고서에는 현재 Scale Out의 실행에 대한 이러한 로그가 표시되지 않습니다. SSMS의 다음 릴리스에서 지원될 예정됩니다. 영향을 받는 보고서로 Integration Services 대시보드의 *모든 연결* 보고서, *오류 컨텍스트* 보고서 및 *연결 정보* 섹션이 있습니다.
    - 새로운 **event_message_guid** 열이 추가되었습니다. Scale Out에서 이러한 실행 로그를 쿼리할 때 **event_message_id** 를 사용하는 대신 [catalog]. [event_message_context] 뷰 및 [catalog]. [event_messages] 뷰에 이 열을 조인합니다.
-   SSIS Scale Out에 대한 관리 애플리케이션을 가져오려면 [SSMS(SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md) 17.1 이상을 다운로드합니다.

## <a name="new-in-ssis-in-sql-server-2017-ctp-20"></a>SQL Server 2017 CTP 2.0 SSIS의 새로운 기능

SQL Server 2017 CTP 2.0에는 새로운 SSIS 기능이 없습니다.

## <a name="new-in-ssis-in-sql-server-2017-ctp-14"></a>SQL Server 2017 CTP 1.4 SSIS의 새로운 기능

SQL Server 2017 CTP 1.4에는 새로운 SSIS 기능이 없습니다.

## <a name="new-in-ssis-in-sql-server-2017-ctp-13"></a>SQL Server 2017 CTP 1.3 SSIS의 새로운 기능

SQL Server 2017 CTP 1.3에는 새로운 SSIS 기능이 없습니다.

## <a name="new-in-ssis-in-sql-server-2017-ctp-12"></a>SQL Server 2017 CTP 1.2 SSIS의 새로운 기능

SQL Server 2017 CTP 1.2에는 새로운 SSIS 기능이 없습니다.

## <a name="new-in-ssis-in-sql-server-2017-ctp-11"></a>SQL Server 2017 CTP 1.1 SSIS의 새로운 기능

SQL Server 2017 CTP 1.1에는 새로운 SSIS 기능이 없습니다.

## <a name="new-in-ssis-in-sql-server-2017-ctp-10"></a>SQL Server 2017 CTP 1.0 SSIS의 새로운 기능

### <a name="scale-out-for-ssis"></a>SSIS용 규모 확장

규모 확장 기능을 사용하면 여러 컴퓨터에서 훨씬 더 쉽게 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 를 실행할 수 있습니다. 
   
규모 확장 마스터 및 작업자를 설치한 후 패키지를 배포하여 다른 작업자에서 자동으로 실행할 수 있습니다. 실행이 예기치 않게 종료되는 경우 실행이 자동으로 다시 시도됩니다. 또한 모든 실행 및 작업자는 마스터를 사용하여 중앙에서 관리할 수 있습니다.
   
자세한 내용은 [Integration Services 규모 확장](../integration-services/scale-out/integration-services-ssis-scale-out.md)을 참조하세요.
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Microsoft Dynamics Online 리소스 지원

이제 OData 원본 및 OData 연결 관리자가 Microsoft Dynamics AX Online 및 Microsoft Dynamics CRM Online의 OData 피드에 연결할 수 있습니다.