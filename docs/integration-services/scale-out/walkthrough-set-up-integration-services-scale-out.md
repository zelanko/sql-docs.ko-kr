---
title: '연습: SSIS Scale Out 설정 | Microsoft Docs'
description: 이 문서에서는 SSIS Scale Out의 설정 및 구성을 연습합니다.
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
author: HaoQian-MS
ms.author: haoqian
ms.openlocfilehash: c1f2a7670913f2df948201b29f26e0283f27f698
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79288747"
---
# <a name="walkthrough-set-up-integration-services-ssis-scale-out"></a>연습: Integration Services(SSIS) Scale Out 설정

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


다음 작업을 수행하여 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)](SSIS) Scale Out을 설정합니다. 

> [!TIP]
> 단일 컴퓨터에 Scale Out을 설치하는 경우 Scale Out 마스터 및 Scale Out 작업자 기능을 동시에 설치합니다. 이 기능을 동시에 설치하면 규모 확장 마스터에 연결하는 엔드포인트가 자동으로 생성됩니다. 

* [규모 확장 마스터 설치](#InstallMaster)

* [규모 확장 작업자 설치](#InstallWorker)

* [규모 확장 작업자 클라이언트 인증서 설치](#InstallCert)

* [방화벽 포트 열기](#Firewall)

* [SQL Server 규모 확장 마스터 및 작업자 서비스 시작](#Start)

* [규모 확장 마스터를 사용하도록 설정](#EnableMaster)

* [SQL Server 인증 모드 사용](#EnableAuth)

* [규모 확장 작업자를 사용하도록 설정](#EnableWorker)

## <a name="InstallMaster"></a> 규모 확장 마스터 설치

Scale Out 마스터를 설정하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]를 설정할 때 SSIS의 데이터베이스 엔진 서비스, [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 및 해당 Scale Out 마스터 기능을 설치해야 합니다. 

데이터베이스 엔진 및 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)]를 설정하는 방법에 대한 자세한 내용은 [SQL Server 데이터베이스 엔진 설치](../../database-engine/install-windows/install-sql-server-database-engine.md) 및 [Integration Services 설치](../install-windows/install-integration-services.md)를 참조하세요.

> [!NOTE]
> Scale Out 로깅에 기본 SQL Server 인증 계정을 사용하려면 데이터베이스 엔진을 설치하는 동안 **데이터베이스 엔진 구성** 페이지에서 인증 모드로 혼합 모드를 선택합니다. 자세한 내용은 [Scale Out 로깅에 대한 계정 변경](change-logdb-account.md)을 참조하세요.

Scale Out 마스터 기능을 설치하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 마법사나 명령 프롬프트를 사용합니다.

### <a name="install-scale-out-master-with-the-sql-server-installation-wizard"></a>SQL Server 설치 마법사로 Scale Out 마스터 설치
1.  **기능 선택** 페이지에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 아래에 나열된 **Scale Out 마스터**를 선택합니다.   
  
    ![기능 선택 마스터](media/feature-select-master.PNG)
  
2.  **서버 구성** 페이지에서 **SQL Server Integration Services 규모 확장 마스터 서비스** 를 실행할 계정을 선택하고 **시작 유형**을 선택합니다.  
    ![서버 구성](media/server-config.PNG)

3.  **Integration Services 규모 확장 마스터 구성** 페이지에서 규모 확장 마스터가 규모 확장 작업자와 통신하는 데 사용하는 포트 번호를 지정합니다. 기본 포트 번호는 8391입니다.  

    ![마스터 구성](media/master-config.PNG "마스터 구성")

4.  다음 중 하나를 수행하여 Scale Out 마스터와 Scale Out 작업자 간의 통신을 보호하는 데 사용되는 SSL 인증서를 지정합니다.
    * 설치 프로세스에서 **새 SSL 인증서 만들기**를 클릭하여 자체 서명된 기본 SSL 인증서를 만들도록 합니다.  기본 인증서는 신뢰할 수 있는 루트 인증 기관, 로컬 컴퓨터에 아래에 설치됩니다. 이 인증서에 CN을 지정할 수 있습니다. 마스터 엔드포인트의 호스트 이름은 CN에 포함되어야 합니다. 기본적으로 마스터 노드의 컴퓨터 이름과 IP가 포함됩니다.
    * **기존 SSL 인증서 사용**을 클릭한 다음 **찾아보기**를 클릭하여 인증서를 선택함으로써 로컬 컴퓨터의 기존 SSL 인증서를 선택합니다. 인증서의 지문이 텍스트 상자에 나타납니다. **찾아보기** 를 클릭하면 신뢰할 수 있는 루트 인증 기관, 로컬 컴퓨터에 저장된 인증서가 표시됩니다. 선택한 인증서는 여기에 저장되어야 합니다.       

    ![마스터 구성 2](media/master-config-2.PNG "마스터 구성 2")
  
5.  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치를 마칩니다.

### <a name="install-scale-out-master-from-the-command-prompt"></a>명령 프롬프트에서 Scale Out 마스터 설치

[명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)의 지침에 따릅니다. 다음을 수행하여 Scale Out 마스터의 매개 변수를 설정합니다.
 
1.  매개 변수 `/FEATURES`에 `IS_Master` 추가

2.  다음 매개 변수 및 값을 지정하여 Scale Out 마스터를 구성합니다.
    -   `/ISMASTERSVCACCOUNT`
    -   `/ISMASTERSVCPASSWORD`
    -   `/ISMASTERSVCSTARTUPTYPE`
    -   `/ISMASTERSVCPORT`
    -   `/ISMasterSVCSSLCertCN`(선택 사항)
    -   `/ISMASTERSVCTHUMBPRINT`(선택 사항)

    > [!NOTE]
    > Scale Out 마스터가 데이터베이스 엔진과 함께 설치되지 않고 데이터베이스 엔진 인스턴스가 명명된 인스턴스인 경우, 설치한 후에 `SqlServerName`을 Scale Out 마스터 서비스 구성 파일에 구성해야 합니다. 자세한 내용은 [Scale Out 마스터](integration-services-ssis-scale-out-master.md)를 참조하세요.

## <a name="InstallWorker"></a> 규모 확장 작업자 설치
 
Scale Out 작업자를 설정하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설정 시 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 및 해당 Scale Out 작업자 기능을 설치해야 합니다.

Scale Out 작업자 기능을 설치하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 마법사나 명령 프롬프트를 사용합니다.

### <a name="install-scale-out-worker-with-the-sql-server-installation-wizard"></a>SQL Server 설치 마법사로 Scale Out 작업자 설치

1.  **기능 선택** 페이지에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 아래에 나열된 **Scale Out 작업자**를 선택합니다.

    ![기능 선택 작업자](media/feature-select-worker.PNG)

2.  **서버 구성** 페이지에서 **SQL Server Integration Services 규모 확장 작업자 서비스** 를 실행할 계정을 선택하고 **시작 유형**을 선택합니다.

    ![서버 구성 2](media/server-config-2.PNG "서버 구성 2")

3.  **Integration Services 규모 확장 작업자 구성** 페이지에서 규모 확장 마스터에 연결하는 엔드포인트를 지정합니다. 

    - **단일 컴퓨터** 환경의 경우 Scale Out 마스터와 Scale Out 작업자를 동시에 설치하면 엔드포인트가 자동으로 생성됩니다. 

    - **여러 컴퓨터** 환경의 경우 엔드포인트는 Scale Out 마스터가 설치된 컴퓨터의 이름 또는 IP 및 Scale Out 마스터 설치 중에 지정된 포트 번호로 구성됩니다.
   
    ![작업자 구성 1](media/worker-config.PNG "작업자 구성 1")    

    > [!NOTE]
    > 설치한 후에 이 시점에서 작업자 구성을 건너뛰고 [Scale Out 관리자](integration-services-ssis-scale-out-manager.md)를 사용하여 Scale Out 작업자를 Scale Out 마스터에 연결할 수 있습니다.

4. **여러 컴퓨터** 환경의 경우 Scale Out 마스터의 유효성을 검사하는 데 사용되는 클라이언트 SSL 인증서를 지정합니다. **단일 컴퓨터** 환경의 경우 클라이언트 SSL 인증서를 지정할 필요가 없습니다. 
  
    **찾아보기** 를 클릭하여 인증서 파일(*.cer)을 찾습니다. 기본 SSL 인증서를 사용하려면 Scale Out 마스터가 설치된 컴퓨터에서 `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn` 아래에 있는 `SSISScaleOutMaster.cer` 파일을 선택합니다.   

    ![작업자 구성 2](media/worker-config-2.PNG "작업자 구성 2")

    > [!NOTE]
    > Scale Out 마스터에서 사용되는 SSL 인증서가 자체 서명된 경우 해당 클라이언트 SSL 인증서가 Scale Out 작업자와 함께 컴퓨터에 설치되어 있어야 합니다. **Integration Services Scale Out 작업자 구성** 페이지에서 클라이언트 SSL 인증서의 파일 경로를 제공하는 경우 인증서가 자동으로 설치됩니다. 그렇지 않은 경우 나중에 인증서를 수동으로 설치해야 합니다. 
     
5. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치를 마칩니다.

### <a name="install-scale-out-worker-from-the-command-prompt"></a>명령 프롬프트에서 Scale Out 작업자 설치

[명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)의 지침에 따릅니다. 다음을 수행하여 Scale Out 작업자의 매개 변수를 설정합니다.

1.  `/FEATURES` 매개 변수에 IS_Worker를 추가합니다.

2. 다음 매개 변수 및 값을 지정하여 Scale Out 작업자를 구성합니다.
    -   `/ISWORKERSVCACCOUNT`
    -   `/ISWORKERSVCPASSWORD`
    -   `/ISWORKERSVCSTARTUPTYPE`
    -   `/ISWORKERSVCMASTER`(선택 사항)
    -   `/ISWORKERSVCCERT`(선택 사항)
 
## <a name="InstallCert"></a> 규모 확장 작업자 클라이언트 인증서 설치

Scale Out 작업자를 설치하는 동안 작업자 인증서가 자동으로 생성되어 컴퓨터에 설치됩니다. 또한 해당 클라이언트 인증서 SSISScaleOutWorker.cer은 `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn` 아래에 설치됩니다. Scale Out 마스터가 Scale Out 작업자를 인증하려면 이 클라이언트 인증서를 Scale Out 마스터가 있는 로컬 컴퓨터의 루트 저장소에 추가해야 합니다.
  
루트 저장소에 클라이언트 인증서를 추가하려면 .cer 파일을 두 번 클릭한 다음 인증서 대화 상자에서 **인증서 설치**를 클릭합니다. **인증서 가져오기 마법사**가 열립니다.  

## <a name="Firewall"></a> 방화벽 포트 열기

Scale Out 마스터 컴퓨터의 Windows 방화벽에서 Scale Out 마스터 설치 중에 지정한 포트와 SQL Server 포트(기본적으로 1433)를 엽니다.

> [!Note]
> 방화벽 포트를 연 후에도 Scale Out 작업자 서비스를 다시 시작해야 합니다.
    
## <a name="Start"></a> SQL Server 규모 확장 마스터 및 작업자 서비스 시작

설치하는 동안 서비스의 시작 유형을 **자동**으로 설정하지 않은 경우 다음과 같은 서비스를 시작합니다.

-   SQL Server Integration Services Scale Out 마스터 14.0(SSISScaleOutMaster140)

-   SQL Server Integration Services Scale Out 작업자 14.0(SSISScaleOutWorker140) 구성

## <a name="EnableMaster"></a> 규모 확장 마스터를 사용하도록 설정

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)]에서 SSISDB 카탈로그를 만들 때 **카탈로그 만들기** 대화 상자에서 **이 서버를 SSIS Scale Out 마스터로 사용**을 클릭합니다.

카탈로그를 만든 후에 [Scale Out 관리자](integration-services-ssis-scale-out-manager.md)를 사용하여 Scale Out 마스터를 사용하도록 설정할 수 있습니다.

## <a name="EnableAuth"></a> SQL Server 인증 모드를 사용하도록 설정
데이터베이스 엔진을 설치하는 동안 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인증을 사용하도록 설정하지 않은 경우 SSISDB 카탈로그를 호스팅하는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스에서 SQL Server 인증 모드를 사용하도록 설정합니다. 

SQL Server 인증을 사용하지 않는 경우 패키지 실행이 차단되지 않습니다. 하지만 실행 로그는 SSISDB 데이터베이스에 쓸 수 없습니다.

## <a name="EnableWorker"></a> 규모 확장 작업자를 사용하도록 설정

그래픽 사용자 인터페이스를 제공하는 [Scale Out 관리자](integration-services-ssis-scale-out-manager.md) 또는 저장 프로시저를 사용하여 Scale Out 작업자를 사용하도록 설정할 수 있습니다.

저장 프로시저를 사용하여 Scale Out 작업자를 사용하도록 설정하려면 **WorkerAgentId**를 매개 변수로 사용하여 `[catalog].[enable_worker_agent]` 저장 프로시저를 실행합니다. 

Scale Out 작업자가 Scale Out 마스터에 등록된 후 SSISDB의 `[catalog].[worker_agents]` 보기에서 **WorkerAgentId** 값을 가져옵니다. Scale Out 마스터 및 작업자 서비스가 시작된 다음에 등록하려면 몇 분 정도 걸립니다.

#### <a name="example"></a>예제
다음 예제에서는 `computerA`에서 Scale Out 작업자를 사용하도록 설정합니다.

```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName  --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    computerA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## <a name="next-steps"></a>다음 단계
-   [Integration Services(SSIS) Scale Out에서 패키지 실행](run-packages-in-integration-services-ssis-scale-out.md).
