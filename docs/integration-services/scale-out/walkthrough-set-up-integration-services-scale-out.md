---
title: "연습: 설정 Sql Server Integration Services 확장 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9cc5c653fe454b45148583f2e17654657a85b0a5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="walkthrough-set-up-integration-services-scale-out"></a>연습: Integration Services 규모 확장 설치
설정 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 다음과 같은 작업을 완료 하 여 스케일 아웃 합니다. 

> [!NOTE]
> 한 컴퓨터에서 스케일 아웃 설치 하는 경우 스케일 아웃 마스터 및 스케일 아웃 작업자 기능을 동시에 설치 합니다. 이 기능을 동시에 설치하면 규모 확장 마스터에 연결하는 끝점이 자동으로 생성됩니다. 

* [규모 확장 마스터 설치](#InstallMaster)

* [규모 확장 작업자 설치](#InstallWorker)

* [규모 확장 작업자 클라이언트 인증서 설치](#InstallCert)

* [방화벽 포트 열기](#Firewall)

* [SQL Server 규모 확장 마스터 및 작업자 서비스 시작](#Start)

* [규모 확장 마스터를 사용하도록 설정](#EnableMaster)

* [SQL Server 인증 모드를 사용하도록 설정](#EnableAuth)

* [규모 확장 작업자를 사용하도록 설정](#EnableWorker)

## <a name="InstallMaster"></a> 규모 확장 마스터 설치

스케일 아웃 마스터의 기능을 사용 하도록 설정 하려면 데이터베이스 엔진 서비스를 설치 해야 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)], 및의 스케일 아웃 마스터 기능을 설정할 때 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 

데이터베이스 엔진 서비스 및 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 설치에 대한 자세한 내용은 [SQL Server 데이터베이스 엔진 설치](../../database-engine/install-windows/install-sql-server-database-engine.md) 및 [Integration Services 설치](../install-windows/install-integration-services.md)를 참조하세요.
> [!NOTE]
> 스케일 아웃 실행 로깅에 대 한 기본 SQL 인증 계정을 사용 하려면 데이터베이스 엔진 설치 하는 동안 데이터베이스 엔진 구성 페이지에서 인증 모드에 대해 혼합 모드를 선택 합니다. 참조 [범위 확장 로깅에 대 한 계정을 변경](change-logdb-account.md) 자세한 정보에 대 한 합니다.

**규모 확장 마스터 기능을 설치하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 마법사나 명령 프롬프트를 사용합니다.**

- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 마법사의 단계
  1.  에 **기능 선택** 페이지에서 **스케일 아웃 마스터**, 아래에 나열 된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]합니다.   
  ![기능 선택 마스터](media/feature-select-master.PNG)
  
  2.  **서버 구성** 페이지에서 **SQL Server Integration Services 규모 확장 마스터 서비스** 를 실행할 계정을 선택하고 **시작 유형**을 선택합니다.  
  ![서버 구성](media/server-config.PNG)
  3.  **Integration Services 규모 확장 마스터 구성** 페이지에서 규모 확장 마스터가 규모 확장 작업자와 통신하는 데 사용하는 포트 번호를 지정합니다. 기본 포트 번호는 8391입니다.  
  ![마스터 구성](media/master-config.PNG "마스터 구성")
  4.  다음 중 하나를 수행 하 여 스케일 아웃 마스터 및 스케일 아웃 작업자 간의 통신을 보호 하는 데 사용 된 SSL 인증서를 지정 합니다.
    * 설치 프로세스를 클릭 하 여 기본적으로 자체 서명 된 SSL 인증서를 만들 **새 SSL 인증서를 만들**합니다.  기본 인증서는 신뢰할 수 있는 루트 인증 기관, 로컬 컴퓨터에 아래에 설치됩니다. 이 인증서의 Cn을 지정할 수 있습니다. 마스터 끝점의 호스트 이름 Cn에 포함 되어야 합니다. 기본적으로 컴퓨터 이름 및 ip 마스터 노드의 포함 됩니다.
    * 클릭 하 여 로컬 컴퓨터에는 기존 SSL 인증서를 선택 **기존 SSL 인증서를 사용 하 여** 클릭 한 다음 **찾아보기** 는 인증서를 선택 합니다. 인증서의 지문이 텍스트 상자에 나타납니다. **찾아보기** 를 클릭하면 신뢰할 수 있는 루트 인증 기관, 로컬 컴퓨터에 저장된 인증서가 표시됩니다. 선택한 인증서는 여기에 저장되어야 합니다.       
![마스터 구성 2](media/master-config-2.PNG "마스터 구성 2")
  5.  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치를 마칩니다.
- 명령 프롬프트의 단계

    [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)의 지침에 따릅니다. 다음을 수행하여 규모 확장 마스터 관련 매개 변수를 설정합니다.
  1.  /FEATURES 매개 변수에 IS_Master를 추가합니다.
  2.  다음 매개 변수 및 해당 값을 지정 하 여 스케일 아웃 마스터 구성: /ISMASTERSVCACCOUNT, /ISMASTERSVCPASSWORD, /ISMASTERSVCSTARTUPTYPE, /ISMASTERSVCPORT, /ISMasterSVCSSLCertCN(optional), /ISMASTERSVCTHUMBPRINT(optional) 합니다.

> [!Note]
> 스케일 아웃 마스터 데이터베이스 엔진을 함께 설치 되어 있지 않습니다 데이터베이스 엔진이 명명 된 인스턴스인 경우 SqlServerName을 스케일 아웃 마스터 서비스 구성 파일에서 설치 후 구성 해야 합니다. 참조 [스케일 아웃 마스터](integration-services-ssis-scale-out-master.md) 대 한 자세한 내용은 합니다.

## <a name="InstallWorker"></a> 규모 확장 작업자 설치
 
규모 확장 작업자의 기능을 사용하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 시 [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] 및 해당 규모 확장 작업자 기능을 설치해야 합니다.

**규모 확장 작업자 기능을 설치하려면 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 마법사나 명령 프롬프트를 사용합니다.**

- [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치 마법사의 단계
  1.  에 **기능 선택** 페이지에서 **스케일 아웃 작업자**, 아래에 나열 된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]합니다.   
  ![기능 선택 작업자](media/feature-select-worker.PNG)
  2. **서버 구성** 페이지에서 **SQL Server Integration Services 규모 확장 작업자 서비스** 를 실행할 계정을 선택하고 **시작 유형**을 선택합니다.    
  ![서버 구성 2](media/server-config-2.PNG "서버 구성 2")
  3. **Integration Services 규모 확장 작업자 구성** 페이지에서 규모 확장 마스터에 연결하는 끝점을 지정합니다. 
      > [!Note]
      > 스케일 아웃 마스터와 스케일 아웃 작업자 연결을 여기 작업자 노드 구성 (단계 3 및 4 단계)를 건너뛰고 [스케일 아웃 관리자](integration-services-ssis-scale-out-manager.md) 설치 후 합니다.

    - 에 대 한는 **한 컴퓨터** 환경에서 끝점에는 스케일 아웃 마스터 및 스케일 아웃 작업자 동시에 설치 되 면 자동으로 생성 됩니다. 
    - 에 대 한는 **여러 컴퓨터** 스케일 아웃 마스터 설치 및 스케일 아웃 마스터 설치 시 지정한 포트 번호가 중 이름 또는 컴퓨터의 IP 환경에서는 끝점 구성입니다.    
   ![작업자 Config 1](media/worker-config.PNG "작업자 구성 1")    

  4. 에 대 한는 **여러 컴퓨터** 환경에서는 스케일 아웃 마스터의 유효성을 검사 하는 데 사용 되는 클라이언트 SSL 인증서를 지정 합니다. 에 대 한는 **한 컴퓨터** 환경에서는 클라이언트 SSL 인증서를 지정할 필요가 없습니다. 
  
     > [!NOTE]
     > 스케일 아웃 마스터에서 사용 하는 SSL 인증서가 자체 서명 된 경우 해당 클라이언트 SSL 인증서가 스케일 아웃 작업자를 사용 하 여 컴퓨터에 설치 하는 데 필요 합니다. 클라이언트 SSL 인증서에 대 한 파일 경로 제공 하는 경우는 **Integration Services 스케일 아웃 작업자 구성** 페이지에서 인증서를 자동으로 설치 됩니다. 즉, 나중에 수동으로 인증서를 설치 하 합니다. 
     
     **찾아보기** 를 클릭하여 인증서 파일(*.cer)을 찾습니다. 기본 SSL 인증서를 사용 하려면 아래에 있는 SSISScaleOutMaster.cer 파일 선택 \<드라이브\>: files\microsoft SQL Server\140\DTS\Binn 스케일 아웃 마스터가 설치 된 컴퓨터에 있습니다.   
   ![작업자 Config 2](media/worker-config-2.PNG "작업자 구성 2")
  5. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 설치를 마칩니다.
- 명령 프롬프트의 단계

    [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)의 지침에 따릅니다. 다음을 수행하여 규모 확장 작업자 관련 매개 변수를 설정합니다.
    1.  /FEATURES 매개 변수에 IS_Worker를 추가합니다.
    2. 스케일 아웃 Worker 구성 다음 매개 변수 및 해당 값을 지정: /ISWORKERSVCACCOUNT, /ISWORKERSVCPASSWORD, /ISWORKERSVCSTARTUPTYPE, /ISWORKERSVCMASTER(optional), /ISWORKERSVCCERT(optional) 합니다.

 
## <a name="InstallCert"></a> 규모 확장 작업자 클라이언트 인증서 설치

스케일 아웃 Worker가 설치 하는 동안 작업자 인증서를 자동으로 생성 되며 컴퓨터에 설치 합니다. 또한 해당 클라이언트 인증서 SSISScaleOutWorker.cer은 \<드라이버\>:\Program Files\Microsoft SQL Server\140\DTS\Binn 아래에 설치됩니다. 스케일 아웃 마스터를 스케일 아웃 작업자 인증에 대 한 스케일 아웃 마스터와 로컬 컴퓨터의 루트 저장소에이 클라이언트 인증서를 추가 해야 합니다.
  
루트 저장소에 클라이언트 인증서를 추가하려면 .cer 파일을 두 번 클릭한 다음 [인증서] 대화 상자에서 **인증서 설치** 를 클릭합니다. **인증서 가져오기 마법사** 가 표시됩니다.  

## <a name="Firewall"></a> 방화벽 포트 열기

스케일 아웃 마스터 설치 및 포트의 SQL Server (기본적으로: 1433)를 하는 동안 지정 된 포트 열기 스케일 아웃 마스터 컴퓨터에서 Windows 방화벽을 사용 합니다.
    
## <a name="Start"></a> SQL Server 규모 확장 마스터 및 작업자 서비스 시작

서비스의 시작 유형을 자동으로 설치 하는 동안 설정 하지 않으면 서비스를 시작: SQL Server Integration Services 스케일 아웃 마스터 14.0 (SSISScaleOutMaster140) 및 SQL Server Integration Services 스케일 아웃 작업자 14.0 (SSISScaleOutWorker140). 

> [!Note]
> 방화벽 포트를 연 후에 또한 스케일 아웃 Worker 서비스를 다시 시작 해야.
   
## <a name="EnableMaster"></a> 규모 확장 마스터를 사용하도록 설정

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)]에서 SSISDB 카탈로그를 만들 때 **카탈로그 만들기** 대화 상자에서 **이 서버를 SSIS 규모 확장 마스터로 사용**을 클릭합니다. 또한, 스케일 아웃 마스터를 사용할 수 있습니다 [스케일 아웃 관리자](integration-services-ssis-scale-out-manager.md) 카탈로그 만들어지면 합니다.

## <a name="EnableAuth"></a> SQL Server 인증 모드를 사용하도록 설정
경우 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 에서 SQL Server 인증 모드를 사용 하도록 설정, 데이터베이스 엔진 설치 하는 동안 인증을 해제는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] SSISDB 카탈로그를 호스팅하는 인스턴스에 있습니다. 

SQL Server 인증을 사용하지 않는 경우 패키지 실행이 차단되지 않습니다. 그러나 실행 로그는 SSISDB에 쓸 수 없습니다.

## <a name="EnableWorker"></a> 규모 확장 작업자를 사용하도록 설정

스케일 아웃 작업자를 통해 사용할 수 있습니다 [스케일 아웃 관리자](integration-services-ssis-scale-out-manager.md); GUI를 제공 하는, 또는 저장된 프로시저를 통해 사용 하도록 설정 아래를 참조 하십시오.

규모 확장 작업자를 사용하도록 설정하려면 *WorkerAgentId* 를 매개 변수로 사용하여 **[catalog].[enable_worker_agent]** 저장 프로시저를 실행합니다. 

규모 확장 작업자가 규모 확장 마스터에 등록된 후 SSISDB의 **[catalog].[worker_agents]** 데이터베이스 뷰에서 *WorkerAgentId* 값을 가져옵니다. 규모 확장 마스터 및 작업자 서비스가 시작된 다음에 등록하려면 몇 분 정도 걸립니다.

#### <a name="example"></a>예제
이 예에서는 컴퓨터 a에서 스케일 아웃 작업자를 설정 합니다.
```tsql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName  --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    computerA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```
## <a name="next-steps"></a>다음 단계
규모 확장 기능의 설치가 완료되었습니다. 범위 확장에서 이제 패키지를 실행할 수 있습니다. 자세한 내용은 [Integration Services(SSIS) 규모 확장에서 패키지 실행](run-packages-in-integration-services-ssis-scale-out.md)을 참조하세요.
