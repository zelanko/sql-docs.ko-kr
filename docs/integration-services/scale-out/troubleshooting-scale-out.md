---
title: "SSIS(SQL Server Integration Services) Scale Out 문제 해결 | Microsoft Docs"
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
ms.openlocfilehash: 56d61bc6ba76514ba2291243002a7423ec8e265c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="troubleshooting-scale-out"></a>Scale Out 문제 해결

SSIS Scale Out에는 SSISDB, Scale Out 마스터 서비스 및 Scale Out 작업자 서비스 사이의 통신이 포함됩니다. 경우에 따라 구성 실수, 액세스 권한 부족 및 기타 이유로 인해 통신이 끊어질 수 있습니다. 이 문서는 Scale Out 구성 문제를 해결하는 데 도움이 됩니다.

발생한 증상을 조사하려면 문제가 해결될 때까지 아래 단계를 하나씩 수행합니다.

### <a name="symptoms"></a>**증상** 
Scale Out 마스터에서 SSISDB에 연결할 수 없습니다. 

Scale Out 관리자에서 마스터 속성이 표시되지 않습니다.

마스터 속성이 [SSISDB].[catalog].[master_properties]에 입력되지 않습니다.

### <a name="solution"></a>**해결 방법**
1단계: Scale Out이 사용하도록 설정되어 있는지 확인합니다.

SSMS의 [개체 탐색기]에서 **SSISDB** 노드를 마우스 오른쪽 단추로 클릭하고 **Scale Out 기능이 사용하도록 설정됨**을 선택합니다.

![사용하도록 설정된 Scale Out](media\isenabled.PNG)

속성 값이 False이면 [SSISDB].[catalog].[enable_scaleout] 저장 프로시저를 호출하여 Scale Out을 사용하도록 설정합니다.

2단계: Scale Out 마스터 구성 파일에 지정된 SQL Server 이름이 올바른지 확인하고 Scale Out 마스터 서비스를 다시 시작합니다.

### <a name="symptoms"></a>**증상** 
Scale Out 작업자에서 Scale Out 마스터에 연결할 수 없습니다.

Scale Out 관리자에서 Scale Out 작업자를 추가한 후에 이 Scale Out 작업자가 표시되지 않습니다.

[SSISDB].[catalog].[worker_agents]에서 Scale Out 작업자가 표시되지 않습니다.

Scale Out 작업자 서비스가 실행되고 있지만 Scale Out 작업자는 오프라인 상태에 있습니다.

### <a name="solutions"></a>**솔루션** 
\<드라이버 \>:\ Users\\*[작업자 서비스를 실행하는 계정]*\AppData\Local\SSIS\Cluster\Agent에 있는 Scale Out 작업자 서비스 로그의 오류 메시지를 확인합니다.

**사례** 

System.ServiceModel.EndpointNotFoundException: 메시지를 수락할 수 있는 https://*[컴퓨터 이름]:[포트]*/ClusterManagement/에서 수신 대기 중인 엔드포인트가 없습니다.

1단계: Scale Out 마스터 서비스 구성 파일에 지정된 포트 번호가 올바른지 확인하고 Scale Out 마스터 서비스를 다시 시작합니다. 

2단계: Scale Out 작업자 서비스 구성에 지정된 마스터 엔드포인트가 올바른지 확인하고 Scale Out 작업자 서비스를 다시 시작합니다.

3단계: Scale Out 마스터 노드에서 방화벽 포트가 열려 있는지 확인합니다.

4단계: Scale Out 마스터 노드와 Scale Out 작업자 노드 사이의 다른 모든 연결 문제를 해결합니다.

**사례**

System.ServiceModel.Security.SecurityNegotiationException: '*[컴퓨터 이름]:[포트]*' 권한이 있는 SSL/TLS 보안 채널에 대해 트러스트 관계를 설정할 수 없습니다. ---> System.Net.WebException: 기본 연결이 닫혔습니다. SSL/TLS 보안 채널에 대한 트러스트 관계를 설정할 수 없습니다. ---> System.Security.Authentication.AuthenticationException: 유효성 검사 절차에 따르면 원격 인증서가 잘못되었습니다.

1단계: 아직 설치하지 않은 경우 Scale Out 작업자 노드에 있는 로컬 컴퓨터의 루트 인증서 저장소에 Scale Out 마스터 인증서를 설치하고 Scale Out 작업자 서비스를 다시 시작합니다.

2단계: 마스터 엔드포인트의 호스트 이름이 Scale Out 마스터 인증서의 CN에 포함되어 있는지 확인합니다. 그렇지 않으면 Scale Out 작업자 구성 파일에서 마스터 엔드포인트를 다시 설정하고 Scale Out 작업자 서비스를 다시 시작합니다. 

> [!Note]
> DNS 설정으로 인해 마스터 엔드포인트의 호스트 이름을 변경할 수 없는 경우 Scale Out 마스터 인증서를 변경해야 합니다. [SSIS Scale Out에서 인증서 처리](deal-with-certificates-in-ssis-scale-out.md)를 참조하세요.

3단계: Scale Out 작업자 구성에 지정된 마스터 지문이 Scale Out 마스터 인증서의 지문과 일치하는지 확인합니다. 

**사례**

System.ServiceModel.Security.SecurityNegotiationException: '*[컴퓨터 이름]:[포트]*' 권한을 가진 SSL/TLS에 대한 보안 채널을 설정할 수 없습니다. ---> System.Net.WebException: 요청이 중단되었습니다, SSL/TLS 보안 채널을 만들 수 없습니다.

1단계: 아래 명령으로 Scale Out 작업자 서비스를 실행하는 계정에 Scale Out 작업자 인증서에 대한 액세스 권한이 있는지 확인합니다.

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

계정에 액세스 권한이 없는 경우 아래 명령으로 권한을 부여하고 Scale Out 작업자 서비스를 다시 시작합니다.

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

**사례**

System.ServiceModel.Security.MessageSecurityException: HTTP 요청이 클라이언트 인증 구성표 'Anonymous'에서 금지되었습니다. ---> System.Net.WebException: 원격 서버에서 (403) 권한 없음 오류를 반환했습니다.

1단계: 아직 설치하지 않은 경우 Scale Out 마스터 노드에 있는 로컬 컴퓨터의 루트 인증서 저장소에 Scale Out 작업자 인증서를 설치하고 Scale Out 작업자 서비스를 다시 시작합니다.

2단계: Scale Out 마스터 노드에 있는 로컬 컴퓨터의 루트 인증서 저장소에서 쓸모 없는 인증서를 정리합니다.

3단계: Scale Out 마스터 노드에서 아래의 레지스트리 항목을 추가하여 TLS/SSL 핸드셰이크 프로세스에서 신뢰할 수 있는 루트 인증 기관 목록을 더 이상 보내지 않도록 Schannel을 구성합니다.

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

값 이름: SendTrustedIssuerList 

값 형식: REG_DWORD 

값 데이터: 0(False)

**사례**

System.ServiceModel.CommunicationException: https://*[컴퓨터 이름]:[포트]*/ClusterManagement/에 대한 HTTP 요청을 수행하는 동안 오류가 발생했습니다. 이것은 HTTPS 경우에 서버 인증서가 HTTP.SYS로 제대로 구성되지 않았기 때문일 수 있습니다. 또한 클라이언트와 서버 사이에 보안 바인딩이 불일치하기 때문일 수 있습니다. 

1단계: 아래 명령을 사용하여 Scale Out 마스터 인증서가 마스터 노드에 있는 마스터 엔드포인트의 포트에 올바르게 바인딩되어 있는지 확인합니다. 표시된 인증서 해시가 Scale Out 마스터 인증서 지문과 일치하는지 확인합니다.

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

바인딩이 올바르지 않은 경우 다음 명령을 사용하여 바인딩을 다시 설정하고 Scale Out 작업자 서비스를 다시 시작합니다.

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root appid={random guid}
```

### <a name="symptoms"></a>**증상**
Scale Out 관리자에서 Scale Out 작업자와 Scale Out 마스터를 연결할 때 "컴퓨터에서 인증서 저장소를 열 수 없음"이라는 오류 메시지와 함께 유효성 검사가 실패했습니다.

### <a name="solution"></a>**해결 방법**

1단계: Scale Out 관리자를 관리자 권한으로 실행합니다. SSMS를 사용하여 여는 경우 SSMS를 관리자 권한으로 실행해야 합니다.

2단계: 실행되고 있지 않으면 원격 레지스트리 서비스를 시작합니다.

### <a name="symptoms"></a>**증상**
Scale Out에서 실행이 시작되지 않습니다.

### <a name="solution"></a>**해결 방법**

[SSISDB].[catalog].[worker_agents]에서 패키지를 실행하기 위해 선택한 컴퓨터의 상태를 확인합니다. 하나 이상의 작업자가 온라인 상태여야 하며 사용하도록 설정되어 있어야 합니다.

### <a name="symptoms"></a>**증상** 
패키지가 성공적으로 실행되었지만 로그 메시지가 없습니다.

### <a name="solution"></a>**해결 방법**

SSISDB를 호스팅하는 SQL Server에서 SQL Server 인증을 허용하는지 확인합니다.

> [!Note]  
> Scale Out 로깅에 대한 계정을 변경한 경우 [Scale Out 로깅에 대한 계정 변경](change-logdb-account.md)을 참조하고 로깅에 사용된 연결 문자열을 확인합니다.

### <a name="symptoms"></a>**증상**
패키지 실행 보고서의 오류 메시지는 문제를 해결하는 데 충분하지 않습니다.

### <a name="solution"></a>**해결 방법**
더 많은 실행 로그는 WorkerSettings.config에 구성된 TasksRootFolder에서 찾을 수 있습니다. 기본적으로 이 폴더는 \<드라이버\>:\Users\\*[계정]*\AppData\Local\SSIS\ScaleOut\Tasks입니다. *[계정]*은 기본값인 SSISScaleOutWorker140을 사용하여 Scale Out 작업자 서비스를 실행하는 계정입니다.

*[execution id]*를 사용하여 패키지 실행 로그를 찾으려면 아래의 T-SQL 명령을 실행하여 *[task id]*를 가져옵니다. 그런 다음 TasksRootFolder 아래에서 *[task id]*로 명명된 하위 폴더를 찾습니다.<sup>1<sup>

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```
<sup>1</sup> 이 쿼리는 문제 해결을 위한 용도로만 사용되며, 나중에 Scale Out 작업자에 대한 로깅/진단 시나리오가 향상될 때 변경됩니다. 
