---
title: "기능 &#39; s 2017 SQL Server에서 Integration Services의 새로운 | Microsoft Docs"
ms.custom: 
ms.date: 07/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 2d47d1bb82b586890e3bfc250cf09e929a64fb25
ms.contentlocale: ko-kr
ms.lasthandoff: 08/23/2017

---
# <a name="what39s-new-in-integration-services-in-sql-server-2017"></a>기능 &#39; s 2017 SQL Server에서 Integration Services의 새로운
이 항목에서는 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 추가되거나 업데이트된 기능에 대해 설명합니다.

>   [!NOTE]
> SQL Server 2017 SQL Server 2016의 기능 및 SQL Server 2016 업데이트에 추가 된 기능에도 포함 되어 있습니다. SQL Server 2016의 새로운 SSIS기능에 대한 자세한 내용은 [SQL Server 2016 Integration Services의 새로운 기능](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)을 참조하세요.

## <a name="highlights-of-this-release"></a>이 릴리스의 주요 내용

SQL Server 2017에 대 한 Integration Services에서 가장 중요 한 새로운 기능을 다음과 같습니다.

-   **확장할**합니다. SSIS 패키지 실행이 여러 작업자 컴퓨터 보다 쉽게 배포 하 고 단일 마스터 컴퓨터에서 실행 및 작업자를 관리 합니다. 자세한 내용은 참조 하십시오. [Integration Services 스케일 아웃](../integration-services/scale-out/integration-services-ssis-scale-out.md)합니다.

-   **Linux에서 integration Services**합니다. Linux 컴퓨터에서 SSIS 패키지를 실행 합니다. 자세한 내용은 참조 하십시오. [추출, 변환 및 SSIS와 Linux에서 데이터 로드](../linux/sql-server-linux-migrate-ssis.md)합니다.

-   **연결 개선**합니다. 업데이트 된 OData 구성 요소와 Microsoft Dynamics AX Online 및 Microsoft Dynamics CRM Online OData 피드에 연결 합니다. 

## <a name="new-in-the-azure-feature-pack"></a>Azure 기능 팩의 새로운 기능

SQL Server에서 연결 개선 사항 외에도 Azure에 대 한 Integration Services 기능 팩에는 Azure 데이터 레이크 저장소에 대 한 지원을 추가 했습니다. 자세한 내용은 참조 하십시오. [Integration Services (SSIS)에 대 한 Azure 기능 팩](azure-feature-pack-for-integration-services-ssis.md)합니다.

## <a name="new-in-sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)의 새로운 기능

이제 Visual Studio 2015 또는 Visual Studio 2017에 2017 통해 SQL Server 버전 2012를 대상으로 하는 패키지 및 SSIS 프로젝트를 개발할 수 있습니다. 자세한 내용은 [SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요.

## <a name="new-in-ssis-in-sql-server-2017-rc1"></a>SSIS의 SQL Server 2017 r c 1의 새로운 기능

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>SSIS 용 스케일 아웃에 새로운 기능과 변경 된 기능

-   Scale Out Master에서 이제 고가용성을 지원합니다. Always On SSISDB에 대 한를 호스팅하는 스케일 아웃 마스터 서비스 Windows Server 장애 조치 서버에 대 한 클러스터링을 설정 합니다. 스케일 아웃 마스터에이 변경 내용을 적용 하 여 단일 실패 지점 방지 하 고 전체 범위 확장 배포에 대해 고가용성을 제공 합니다.
-   Scale Out Worker에서 실행 로그의 장애 조치(failover) 처리가 향상되었습니다. 실행 로그는 스케일 아웃 작업자 예기치 않게 중지 되는 경우 로컬 디스크에 유지 됩니다. 이상에서는 작업자를 다시 시작 되 면 지속형된 로그를 다시 로드 하 고 SSISDB에 저장 계속 됩니다.
-   일관성과 가독성을 향상하기 위해 저장 프로시저 **[catalog].[create_execution]**의 *runincluster* 매개 변수 이름이 *runinscaleout*으로 변경되었습니다. 이 매개 변수 이름이 변경을 다음과 같은 영향이:
    -   매개 변수 이름을 변경 해야 하는 스케일 아웃에서 패키지를 실행할 기존 스크립트를 사용 하도록 설정한 경우 *runincluster* 를 *runinscaleout* r c 1에서 작동 하는 스크립트에 있도록 합니다.
    -   SQL Server Management Studio (SSMS) 17.1 및 이전 버전의 r c 1에서 스케일 아웃 패키지 실행을 트리거할 수 없습니다. 오류 메시지: “*@runincluster*은(는) 프로시저 **create_execution**의 매개 변수가 아닙니다.” 이 문제는 다음 릴리스인 SSMS 버전 17.2에서 해결됩니다. SSMS는 17.2 이상 버전에서 범위 확장 새 매개 변수 이름 및 패키지 실행을 지원 합니다. SSMS 버전 17.2 문제를 해결 하려면 있을 때까지는 패키지 실행 스크립트를 생성 하 여 기존 버전의 SSMS 사용 하 여 다음의 이름을 변경할 수 있습니다는 *runincluster* 매개 변수를 *runinscaleout* 에서 스크립트 및 스크립트를 실행 합니다.
-   SSIS 카탈로그에 SSIS 패키지를 실행하기 위한 기본 모드를 지정하는 새 전역 속성이 있습니다. 호출 하는 경우이 새 속성이 적용 된 **[catalog]. [ create_execution]** 함께 저장 프로시저는 *runinscaleout* 매개 변수가 null로 설정 합니다. 이 모드는 SSIS SQL 에이전트 작업에도 적용 됩니다. SSMS에서 또는 다음 명령을 사용 하 여 SSISDB 노드에 대 한 속성 대화 상자에서 새 전역 속성을 설정할 수 있습니다.
    ```sql
    EXEC [catalog].[configure_catalog] @property_name=N'DEFAULT_EXECUTION_MODE', @property_value=1
    ```

## <a name="new-in-ssis-in-sql-server-2017-ctp-21"></a>SSIS의 SQL Server 2017 CTP 2.1의 새로운 기능

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>SSIS 용 스케일 아웃에 새로운 기능과 변경 된 기능

-   이제 사용할 수 있습니다는 **Use32BitRuntime** 범위 확장의 실행을 트리거할 때 매개 변수입니다.
-   SSISDB 스케일 아웃에 패키지 실행에 대 한 로깅의 성능이 향상 되었습니다. 이벤트 메시지 및 메시지 컨텍스트 로그 대신 하나씩 일괄 처리 모드에서 이제 SSISDB에 기록 됩니다. 이러한 향상에 대 한 추가 참고 사항이 몇 가지는 다음과 같습니다.        
    - 현재 SQL Server Management Studio (SSMS)의 현재 버전에서 일부 보고서에서 범위 확장 실행에 대 한 이러한 로그를 표시 하지 않습니다. 예상 SSMS의 다음 릴리스에서 지원 됩니다. 영향을 받는 보고서에 포함 됩니다는 *모든 연결* 보고서는 *오류 컨텍스트* , 보고서 및 *연결 정보* 통합 서비스 대시보드 섹션.
    - 새 열 **event_message_guid** 추가 되었습니다. 이 열을 사용 하 여 가입 [catalog]. 보기 [event_message_context] 및 [catalog]. [event_messages]를 사용 하는 대신 볼 **event_message_id** 범위 확장에 실행이 로그를 쿼리할 때.
-   Out에 SSIS 눈금에 대 한 관리 응용 프로그램을 가져올 [SQL Server Management Studio (SSMS)를 다운로드](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.1 이상.

## <a name="new-in-ssis-in-sql-server-2017-ctp-20"></a>SSIS의 SQL Server 2017 CTP 2.0의 새로운 기능

SQL Server 2017 CTP 2.0에는 없는 새로운 SSIS 기능 있습니다.

## <a name="new-in-ssis-in-sql-server-2017-ctp-14"></a>SSIS의 SQL Server 2017 CTP 1.4의 새로운 기능

SQL Server 2017 CTP 1.4의 새로운 SSIS 기능 없는 있습니다.

## <a name="new-in-ssis-in-sql-server-2017-ctp-13"></a>SSIS의 SQL Server 2017 1.3 CTP의 새로운 기능

SQL Server 2017 CTP 1.3에 없는 새로운 SSIS 기능 있습니다.

## <a name="new-in-ssis-in-sql-server-2017-ctp-12"></a>SSIS의 SQL Server 2017 CTP 1.2의 새로운 기능

SQL Server 2017 CTP 1.2에 없는 새로운 SSIS 기능 있습니다.

## <a name="new-in-ssis-in-sql-server-2017-ctp-11"></a>SSIS의 SQL Server 2017 CTP 1.1의 새로운 기능

SQL Server 2017 CTP 1.1에 없는 새로운 SSIS 기능 있습니다.

## <a name="new-in-ssis-in-sql-server-2017-ctp-10"></a>SSIS의 SQL Server 2017 CTP 1.0의 새로운 기능

### <a name="scale-out-for-ssis"></a>SSIS용 규모 확장

규모 확장 기능을 사용하면 여러 컴퓨터에서 훨씬 더 쉽게 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 를 실행할 수 있습니다. 
   
규모 확장 마스터 및 작업자를 설치한 후 패키지를 배포하여 다른 작업자에서 자동으로 실행할 수 있습니다. 실행이 예기치 않게 종료되는 경우 실행이 자동으로 다시 시도됩니다. 또한 모든 실행 및 작업자는 마스터를 사용하여 중앙에서 관리할 수 있습니다.
   
자세한 내용은 [Integration Services 규모 확장](../integration-services/scale-out/integration-services-ssis-scale-out.md)을 참조하세요.
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Microsoft Dynamics Online 리소스 지원

이제 OData 원본 및 OData 연결 관리자가 Microsoft Dynamics AX Online 및 Microsoft Dynamics CRM Online의 OData 피드에 연결할 수 있습니다.


