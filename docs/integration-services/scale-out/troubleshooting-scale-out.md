---
title: SSIS(SQL Server Integration Services) Scale Out 문제 해결 | Microsoft Docs
ms.description: This article describes how to troubleshoot common issues with SSIS Scale Out
ms.custom: ''
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: scale-out
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e3d2408a91ed36358ab3683163dae47ff09b0f1c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="troubleshoot-scale-out"></a>Scale Out 문제 해결

SSIS Scale Out에는 SSIS 카탈로그 데이터베이스인 `SSISDB`, Scale Out 마스터 서비스 및 Scale Out 작업자 서비스 사이의 통신이 포함됩니다. 경우에 따라 구성 실수, 액세스 권한 부족 및 기타 이유로 인해 통신이 끊어질 수 있습니다. 이 문서는 Scale Out 구성 문제를 해결하는 데 도움이 됩니다.

발생한 증상을 조사하려면 문제가 해결될 때까지 아래 단계를 하나씩 수행합니다.

## <a name="scale-out-master-fails"></a>Scale Out 마스터 실패

### <a name="symptoms"></a>증상 
-   Scale Out 마스터에서 SSISDB에 연결할 수 없습니다. 

-   Scale Out 관리자에서 마스터 속성이 표시되지 않습니다.

-   마스터 속성이 `[catalog].[master_properties]` 보기에 채워지지 않습니다.

### <a name="solution"></a>해결 방법
1.  Scale Out이 사용하도록 설정되어 있는지 확인합니다.

    SSMS의 개체 탐색기에서 **SSISDB**를 마우스 오른쪽 단추로 클릭하고 **Scale Out 기능이 사용하도록 설정됨**을 선택합니다.

    ![사용하도록 설정된 Scale Out](media\isenabled.PNG)

    속성 값이 False이면 `[catalog].[enable_scaleout]` 저장 프로시저를 호출하여 Scale Out을 사용하도록 설정합니다.

2.  Scale Out 마스터 구성 파일에 지정된 SQL Server 이름이 올바른지 확인하고 Scale Out 마스터 서비스를 다시 시작합니다.

## <a name="scale-out-worker-fails"></a>Scale Out 작업자 실패

### <a name="symptoms"></a>증상 
-   Scale Out 작업자에서 Scale Out 마스터에 연결할 수 없습니다.

-   Scale Out 관리자에서 Scale Out 작업자를 추가한 후에 이 Scale Out 작업자가 표시되지 않습니다.

-   Scale Out 작업자가 `[catalog].[worker_agents]` 보기에 표시되지 않습니다.

-   Scale Out 작업자 서비스가 실행되고 있지만 Scale Out 작업자는 오프라인 상태에 있습니다.

### <a name="solution"></a>해결 방법
`\<drive\>:\Users\\*[account running worker service]*\AppData\Local\SSIS\Cluster\Agent`에서 Scale Out 작업자 서비스 로그의 오류 메시지를 확인합니다.

## <a name="no-endpoint-listening"></a>수신 대기 중인 엔드포인트가 없음

### <a name="symptoms"></a>증상

*"System.ServiceModel.EndpointNotFoundException: 메시지를 수락할 수 있는 https://*[컴퓨터 이름]:[포트]*/ClusterManagement/에서 수신 대기 중인 엔드포인트가 없습니다."*

### <a name="solution"></a>해결 방법

1.  Scale Out 마스터 서비스 구성 파일에 지정된 포트 번호가 올바른지 확인하고 Scale Out 마스터 서비스를 다시 시작합니다. 

2.  Scale Out 작업자 서비스 구성 파일에 지정된 마스터 엔드포인트가 올바른지 확인하고 Scale Out 작업자 서비스를 다시 시작합니다.

3.  Scale Out 마스터 노드에서 방화벽 포트가 열려 있는지 확인합니다.

4.  Scale Out 마스터 노드와 Scale Out 작업자 노드 사이의 다른 연결 문제가 있으면 모두 해결합니다.

## <a name="could-not-establish-trust-relationship"></a>트러스트 관계를 설정할 수 없는 경우

### <a name="symptoms"></a>증상
*"System.ServiceModel.Security.SecurityNegotiationException: '[컴퓨터 이름]:[포트]' 권한이 있는 SSL/TLS 보안 채널에 대해 트러스트 관계를 설정할 수 없습니다."*

*"System.Net.WebException: 기본 연결이 닫혔습니다. SSL/TLS 보안 채널에 대한 트러스트 관계를 설정할 수 없습니다."*

*"System.Security.Authentication.AuthenticationException: 유효성 검사 절차에 따르면 원격 인증서가 잘못되었습니다."*

### <a name="solution"></a>해결 방법
1.  인증서가 아직 설치되지 않은 경우 Scale Out 작업자 노드에서 로컬 컴퓨터의 루트 인증서 저장소에 Scale Out 마스터 인증서를 설치하고 Worker Scale 작업자 서비스를 다시 시작합니다.

2.  마스터 엔드포인트의 호스트 이름이 Scale Out 마스터 인증서의 CN에 포함되어 있는지 확인합니다. 그렇지 않으면 Scale Out 작업자 구성 파일에서 마스터 엔드포인트를 다시 설정하고 Scale Out 작업자 서비스를 다시 시작합니다. 

    > [!NOTE]
    > DNS 설정으로 인해 마스터 엔드포인트의 호스트 이름을 변경할 수 없는 경우 Scale Out 마스터 인증서를 변경해야 합니다. [SSIS Scale Out에 대한 인증서 관리](deal-with-certificates-in-ssis-scale-out.md)를 참조하세요.

3.  Scale Out 작업자 구성에 지정된 마스터 지문이 Scale Out 마스터 인증서의 지문과 일치하는지 확인합니다. 

## <a name="could-not-establish-secure-channel"></a>보안 채널을 설정할 수 없는 경우

### <a name="symptoms"></a>증상

*"System.ServiceModel.Security.SecurityNegotiationException: '[컴퓨터 이름]:[포트]' 권한이 있는 SSL/TLS에 대한 보안 채널을 설정할 수 없습니다."*

*"System.Net.WebException: 요청이 중단되었습니다, SSL/TLS 보안 채널을 만들 수 없습니다."*

### <a name="solution"></a>해결 방법
아래 명령으로 Scale Out 작업자 서비스를 실행하는 계정에 Scale Out 작업자 인증서에 대한 액세스 권한이 있는지 확인합니다.

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

계정에 액세스 권한이 없는 경우 다음 명령을 실행하여 액세스 권한을 부여하고 Scale Out 작업자 서비스를 다시 시작합니다.

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

## <a name="http-request-forbidden"></a>HTTP 요청이 금지된 경우

### <a name="symptoms"></a>증상

*"System.ServiceModel.Security.MessageSecurityException: HTTP 요청이 클라이언트 인증 체계 'Anonymous'에서 금지되었습니다."*

*"System.Net.WebException: 원격 서버에서 (403) 사용할 수 없음 오류를 반환했습니다."*

### <a name="solution"></a>해결 방법
1.  인증서가 아직 설치되지 않은 경우 Scale Out 마스터 노드에서 로컬 컴퓨터의 루트 인증서 저장소에 Scale Out 작업자 인증서를 설치하고 Worker Scale 작업자 서비스를 다시 시작합니다.

2.  Scale Out 마스터 노드에 있는 로컬 컴퓨터의 루트 인증서 저장소에서 쓸모 없는 인증서를 정리합니다.

3.  Scale Out 마스터 노드에서 다음 레지스트리 항목을 추가하여 TLS/SSL 핸드셰이크 프로세스 중에 신뢰할 수 있는 루트 인증 기관 목록을 더 이상 보내지 않도록 Schannel을 구성합니다.

    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL`

    값 이름: **SendTrustedIssuerList** 

    값 형식: **REG_DWORD** 

    값 데이터: **0(False)**

4.  2단계에서 자체 서명되지 않은 모든 인증서를 정리할 수 없는 경우 3단계에서 레지스트리 키 값을 2로 설정합니다.

## <a name="http-request-error"></a>HTTP 요청 오류

### <a name="symptoms"></a>증상

*"System.ServiceModel.CommunicationException: https://[컴퓨터 이름]:[포트]/ClusterManagement/에 대한 HTTP 요청을 수행하는 동안 오류가 발생했습니다. 이것은 HTTPS 경우에 서버 인증서가 HTTP.SYS로 제대로 구성되지 않았기 때문일 수 있습니다. 클라이언트와 서버 사이에 보안 바인딩이 불일치하기 때문일 수도 있습니다."*

### <a name="solution"></a>해결 방법
1.  다음 명령을 실행하여 Scale Out 마스터 인증서가 마스터 노드의 마스터 엔드포인트의 포트에 올바르게 바인딩되어 있는지 확인합니다.

    ```dos
    netsh http show sslcert ipport=0.0.0.0:{Master port}
    ```

    표시된 인증서 해시가 Scale Out 마스터 인증서 지문과 일치하는지 확인합니다. 바인딩이 올바르지 않은 경우 다음 명령을 실행하여 바인딩을 다시 설정하고 Scale Out 작업자 서비스를 다시 시작합니다.

    ```dos
    netsh http delete sslcert ipport=0.0.0.0:{Master port}
    netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root  appid={random guid}
    ```

## <a name="cannot-open-certificate-store"></a>인증서 저장소를 열 수 없는 경우

### <a name="symptoms"></a>증상
Scale Out 관리자에서 Scale Out 작업자를 Scale Out 마스터에 연결할 때 *"컴퓨터에서 인증서 저장소를 열 수 없음"* 이라는 오류 메시지와 함께 유효성 검사가 실패했습니다.

### <a name="solution"></a>해결 방법

1.  Scale Out 관리자를 관리자 권한으로 실행합니다. SSMS로 Scale Out 관리자를 열면 관리자로 SSMS를 실행해야 합니다.

2.  실행되고 있지 않으면 컴퓨터에서 원격 레지스트리 서비스를 시작합니다.

## <a name="execution-doesnt-start"></a>실행이 시작되지 않는 경우

### <a name="symptoms"></a>증상
Scale Out에서 실행이 시작되지 않습니다.

### <a name="solution"></a>해결 방법

`[catalog].[worker_agents]` 보기에서 패키지를 실행하도록 선택한 컴퓨터의 상태를 확인합니다. 하나 이상의 작업자가 온라인 상태여야 하며 사용하도록 설정되어 있어야 합니다.

## <a name="no-log"></a>로그가 없음

### <a name="symptoms"></a>증상 
패키지가 성공적으로 실행되었지만 메시지가 기록되지 않았습니다.

### <a name="solution"></a>해결 방법

SSISDB를 호스팅하는 SQL Server 인스턴스에서 SQL Server 인증이 허용되는지 확인합니다.

> [!NOTE]  
> Scale Out 로깅에 대한 계정을 변경한 경우 [Scale Out 로깅에 대한 계정 변경](change-logdb-account.md)을 참조하고 로깅에 사용된 연결 문자열을 확인합니다.

## <a name="error-messages-arent-helpful"></a>오류 메시지가 도움이 되지 않는 경우

### <a name="symptoms"></a>증상
패키지 실행 보고서의 오류 메시지가 문제를 해결하는 데 충분하지 않습니다.

### <a name="solution"></a>해결 방법
`WorkerSettings.config`에 구성된 `TasksRootFolder`에서 더 많은 실행 로그를 찾을 수 있습니다. 기본적으로 이 폴더는 `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Tasks`입니다. *[계정]* 은 기본값인 `SSISScaleOutWorker140`을 사용하여 Scale Out 작업자 서비스를 실행하는 계정입니다.

*[execution id]* 를 사용하여 패키지 실행 로그를 찾으려면 다음 Transact-SQL 명령을 실행하여 *[task id]* 를 가져옵니다. 그런 다음 `TasksRootFolder`에서 *[task ID]* 가 포함된 하위 폴더 이름을 찾습니다.

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```

> [!WARNING]
> 이 쿼리는 문제 해결 목적으로만 사용됩니다. 쿼리에서 참조되는 내부 보기는 앞으로 변경됩니다. 

## <a name="next-steps"></a>다음 단계
자세한 내용은 SSIS Scale Out 설정 및 구성에 대한 다음 문서를 참조하세요.
-   [단일 컴퓨터에서 Integration Services(SSIS) Scale Out 시작](get-started-with-ssis-scale-out-onebox.md)
-   [연습: Integration Services(SSIS) Scale Out 설정](walkthrough-set-up-integration-services-scale-out.md)