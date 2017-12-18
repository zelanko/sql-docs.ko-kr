---
title: "연습: SQL Server Integration Services Scale Out 설정 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ec9744a1efb0e78aca55e85e7f9f3eca007de5a2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="walkthrough-set-up-integration-services-scale-out"></a>연습: Integration Services 규모 확장 설치
다음 작업을 수행하여 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] Scale Out을 설정합니다. 

> [!NOTE]
> 한 컴퓨터에 Scale Out을 설치하는 경우 Scale Out 마스터 및 Scale Out 작업자 기능을 동시에 설치합니다. 이 기능을 동시에 설치하면 규모 확장 마스터에 연결하는 끝점이 자동으로 생성됩니다. 

* [규모 확장 마스터 설치](#InstallMaster)

* [규모 확장 작업자 설치](#InstallWorker)

* [규모 확장 작업자 클라이언트 인증서 설치](#InstallCert)

* [방화벽 포트 열기](#Firewall)

* [SQL Server 규모 확장 마스터 및 작업자 서비스 시작](#Start)

* [규모 확장 마스터를 사용하도록 설정](#EnableMaster)

* [SQL Server 인증 모드를 사용하도록 설정](#EnableAuth)

* [규모 확장 작업자를 사용하도록 설정](#EnableWorker)

## <a name="InstallMaster"></a> 규모 확장 마스터 설치

Scale Out 마스터 기능을 사용하도록 설정하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]를 설치할 때 데이터베이스 엔진 서비스, [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 및 해당 Scale Out 마스터 기능을 설치해야 합니다. 

데이터베이스 엔진 서비스 및 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 설치에 대한 자세한 내용은 [SQL Server 데이터베이스 엔진 설치](../../database-engine/install-windows/install-sql-server-database-engine.md) 및 [Integration Services 설치](../install-windows/install-integration-services.md)를 참조하세요.
> [!NOTE]
> Scale Out 로깅에 기본 SQL 인증 계정을 사용하려면 데이터베이스 엔진을 설치하는 동안 [데이터베이스 엔진 구성] 페이지에서 인증 모드로 [혼합 모드]를 선택합니다. 자세한 내용은 [Scale Out 로깅에 대한 계정 변경](change-logdb-account.md)을 참조하세요.

**규모 확장 마스터 기능을 설치하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 마법사나 명령 프롬프트를 사용합니다.**

- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 마법사의 단계
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
- 명령 프롬프트의 단계

    [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)의 지침에 따릅니다. 다음을 수행하여 규모 확장 마스터 관련 매개 변수를 설정합니다.
  1.  /FEATURES 매개 변수에 IS_Master를 추가합니다.
  2.  /ISMASTERSVCACCOUNT, /ISMASTERSVCPASSWORD, /ISMASTERSVCSTARTUPTYPE, /ISMASTERSVCPORT, /ISMasterSVCSSLCertCN(선택 사항), /ISMASTERSVCTHUMBPRINT(선택 사항) 매개 변수와 해당 값을 지정하여 Scale Out 마스터를 구성합니다.

> [!Note]
> Scale Out 마스터가 데이터베이스 엔진과 함께 설치되지 않고 데이터베이스 엔진이 명명된 인스턴스인 경우, 설치한 후에 SqlServerName을 Scale Out 마스터 서비스 구성 파일에 구성해야 합니다. 자세한 내용은 [Scale Out 마스터](integration-services-ssis-scale-out-master.md)를 참조하세요.

## <a name="InstallWorker"></a> 규모 확장 작업자 설치
 
규모 확장 작업자의 기능을 사용하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 시 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 및 해당 규모 확장 작업자 기능을 설치해야 합니다.

**규모 확장 작업자 기능을 설치하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 마법사나 명령 프롬프트를 사용합니다.**

- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 마법사의 단계
  1.  **기능 선택** 페이지에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 아래에 나열된 **Scale Out 작업자**를 선택합니다.   
  ![기능 선택 작업자](media/feature-select-worker.PNG)
  2. **서버 구성** 페이지에서 **SQL Server Integration Services 규모 확장 작업자 서비스** 를 실행할 계정을 선택하고 **시작 유형**을 선택합니다.    
  ![서버 구성 2](media/server-config-2.PNG "서버 구성 2")
  3. **Integration Services 규모 확장 작업자 구성** 페이지에서 규모 확장 마스터에 연결하는 끝점을 지정합니다. 
      > [!Note]
      > 설치한 후에 작업자 노드 구성(3단계 및 4단계)을 건너뛰고 [Scale Out 관리자](integration-services-ssis-scale-out-manager.md)를 사용하여 Scale Out 작업자를 Scale Out 마스터에 연결할 수 있습니다.

    - **단일 컴퓨터** 환경의 경우 Scale Out 마스터와 Scale Out 작업자를 동시에 설치하면 엔드포인트가 자동으로 생성됩니다. 
    - **여러 컴퓨터** 환경의 경우 엔드포인트는 Scale Out 마스터가 설치된 컴퓨터의 이름 또는 IP 및 Scale Out 마스터 설치 중에 지정된 포트 번호로 구성됩니다.    
   ![작업자 구성 1](media/worker-config.PNG "작업자 구성 1")    

  4. **여러 컴퓨터** 환경의 경우 Scale Out 마스터의 유효성을 검사하는 데 사용되는 클라이언트 SSL 인증서를 지정합니다. **단일 컴퓨터** 환경의 경우 클라이언트 SSL 인증서를 지정할 필요가 없습니다. 
  
     > [!NOTE]
     > Scale Out 마스터에서 사용되는 SSL 인증서가 자체 서명된 경우 해당 클라이언트 SSL 인증서가 Scale Out 작업자와 함께 컴퓨터에 설치되어 있어야 합니다. **Integration Services Scale Out 작업자 구성** 페이지에서 클라이언트 SSL 인증서의 파일 경로를 제공하는 경우 인증서가 자동으로 설치됩니다. 그렇지 않은 경우 나중에 인증서를 수동으로 설치해야 합니다. 
     
     **찾아보기** 를 클릭하여 인증서 파일(*.cer)을 찾습니다. 기본 SSL 인증서를 사용하려면 Scale Out 마스터가 설치된 컴퓨터의 \<드라이브\>:\Program Files\Microsoft SQL Server\140\DTS\Binn에 있는 SSISScaleOutMaster.cer 파일을 선택합니다.   
   ![작업자 구성 2](media/worker-config-2.PNG "작업자 구성 2")
  5. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치를 마칩니다.
- 명령 프롬프트의 단계

    [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)의 지침에 따릅니다. 다음을 수행하여 규모 확장 작업자 관련 매개 변수를 설정합니다.
    1.  /FEATURES 매개 변수에 IS_Worker를 추가합니다.
    2. /ISWORKERSVCACCOUNT, /ISWORKERSVCPASSWORD, /ISWORKERSVCSTARTUPTYPE, /ISWORKERSVCMASTER(선택 사항), /ISWORKERSVCCERT(선택 사항) 매개 변수 및 해당 값을 지정하여 Scale Out 작업자를 구성합니다.

 
## <a name="InstallCert"></a> 규모 확장 작업자 클라이언트 인증서 설치

Scale Out 작업자를 설치하는 동안 작업자 인증서가 자동으로 생성되어 컴퓨터에 설치됩니다. 또한 해당 클라이언트 인증서 SSISScaleOutWorker.cer은 \<드라이버\>:\Program Files\Microsoft SQL Server\140\DTS\Binn 아래에 설치됩니다. Scale Out 마스터가 Scale Out 작업자를 인증하려면 이 클라이언트 인증서를 Scale Out 마스터가 있는 로컬 컴퓨터의 루트 저장소에 추가해야 합니다.
  
루트 저장소에 클라이언트 인증서를 추가하려면 .cer 파일을 두 번 클릭한 다음 [인증서] 대화 상자에서 **인증서 설치** 를 클릭합니다. **인증서 가져오기 마법사** 가 표시됩니다.  

## <a name="Firewall"></a> 방화벽 포트 열기

Scale Out 마스터 컴퓨터에서 Windows 방화벽을 사용하여 Scale Out 마스터 설치 중에 지정한 포트와 SQL Server 포트(기본적으로 1433)를 엽니다.
    
## <a name="Start"></a> SQL Server 규모 확장 마스터 및 작업자 서비스 시작

설치 중에 서비스의 시작 유형이 [자동]으로 설정되지 않은 경우 SQL Server Integration Services Scale Out 마스터 14.0(SSISScaleOutMaster140) 및 SQL Server Integration Services Scale Out 작업자 14.0(SSISScaleOutWorker140) 서비스를 시작합니다. 

> [!Note]
> 방화벽 포트를 연 후에도 Scale Out 작업자 서비스를 다시 시작해야 합니다.
   
## <a name="EnableMaster"></a> 규모 확장 마스터를 사용하도록 설정

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)]에서 SSISDB 카탈로그를 만들 때 **카탈로그 만들기** 대화 상자에서 **이 서버를 SSIS 규모 확장 마스터로 사용**을 클릭합니다. 또는 Scale Out 마스터는 카탈로그를 만든 후에 [Scale Out 관리자](integration-services-ssis-scale-out-manager.md)를 통해 사용하도록 설정할 수 있습니다.

## <a name="EnableAuth"></a> SQL Server 인증 모드를 사용하도록 설정
데이터베이스 엔진을 설치하는 동안 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인증을 사용할 수 없는 경우 SSISDB 카탈로그를 호스팅하는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스에서 SQL Server 인증 모드를 사용하도록 설정합니다. 

SQL Server 인증을 사용하지 않는 경우 패키지 실행이 차단되지 않습니다. 그러나 실행 로그는 SSISDB에 쓸 수 없습니다.

## <a name="EnableWorker"></a> 규모 확장 작업자를 사용하도록 설정

Scale Out 작업자는 GUI를 제공하는 [Scale Out 관리자](integration-services-ssis-scale-out-manager.md) 또는 저장 프로시저를 통해 사용하도록 설정할 수 있습니다(아래 참조).

규모 확장 작업자를 사용하도록 설정하려면 *WorkerAgentId* 를 매개 변수로 사용하여 **[catalog].[enable_worker_agent]** 저장 프로시저를 실행합니다. 

규모 확장 작업자가 규모 확장 마스터에 등록된 후 SSISDB의 **[catalog].[worker_agents]** 데이터베이스 뷰에서 *WorkerAgentId* 값을 가져옵니다. 규모 확장 마스터 및 작업자 서비스가 시작된 다음에 등록하려면 몇 분 정도 걸립니다.

#### <a name="example"></a>예제
이 예제에서는 computerA에서 Scale Out 작업자를 사용하도록 설정합니다.
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
규모 확장 기능의 설치가 완료되었습니다. 이제 Scale Out에서 패키지를 실행할 수 있습니다. 자세한 내용은 [Integration Services(SSIS) 규모 확장에서 패키지 실행](run-packages-in-integration-services-ssis-scale-out.md)을 참조하세요.
