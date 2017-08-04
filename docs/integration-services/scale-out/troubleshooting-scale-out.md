---
title: "SQL Server 통합 문제 해결 (SSIS) 확장을 서비스 | Microsoft Docs"
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
ms.openlocfilehash: 41bb853dd08591596f6f5baa918e174d0c26a6b5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="troubleshooting-scale-out"></a>규모 확장 문제 해결

SSIS 스케일 아웃 SSISDB, 스케일 아웃 마스터 서비스와 스케일 아웃 작업자 서비스 간에 communtication 포함 됩니다. 경우에 따라 통신 구성 실수, 액세스 권한이 부족 및 기타 이유로 인해 손상 되었습니다. 이 문서를 사용 하면 스케일 아웃 구성 문제를 해결 합니다.

문제가 해결 될 때까지 발생 하는 현상을 조사 하려면 하나씩 아래 단계를 수행 합니다.

### <a name="symptoms"></a>**증상** 
스케일 아웃 마스터 SSISDB에 연결할 수 없습니다. 

스케일 아웃 관리자에서 마스터 속성을 표시할 수 없습니다.

마스터 속성 [SSISDB] 입력 되지 됩니다. [catalog]입니다. [master_properties]

### <a name="solution"></a>**해결 방법**
1 단계: 스케일 아웃을 사용할 수 있는지 확인 합니다.

마우스 오른쪽 단추로 클릭 **SSISDB** 확인 하 고 SSMS의 개체 탐색기의 노드 **범위 확장 기능을 사용할 수**합니다.

![범위 확장 사용 여부](media\isenabled.PNG)

저장된 프로시저 [SSISDB]를 호출 하 여 범위 확장 속성 값이 False 인 경우 사용 하도록 설정 합니다. [catalog]입니다. [enable_scaleout]입니다.

2 단계: 스케일 아웃 마스터 구성 파일에 지정 된 Sql Server 이름이 올바른지 확인 하 고 스케일 아웃 마스터 서비스를 다시 시작 합니다.

### <a name="symptoms"></a>**증상** 
스케일 아웃 작업자 스케일 아웃 마스터에 연결할 수 없습니다.

스케일 아웃 관리자에 추가한 후 스케일 아웃 작업자는 표시 되지 않습니다.

스케일 아웃 작업자 [SSISDB]에 표시 되지 않습니다. [catalog]입니다. [worker_agents]

스케일 아웃 Worker 서비스가 실행 되 고, 스케일 아웃 작업자 오프 라인 상태인 동안

### <a name="solutions"></a>**솔루션** 
스케일 아웃 작업자 서비스 로그에 오류 메시지를 확인 \<드라이버\>: \Users\\*[worker 서비스를 실행 하는 계정]*\AppData\Local\SSIS\Cluster\Agent 합니다.

**대/소문자** 

System.ServiceModel.EndpointNotFoundException: https://에서 수신 대기 중인 끝점이 없습니다*[MachineName]: [Port]*/ClusterManagement/ 메시지를 수락할 수 있는 합니다.

1 단계: 스케일 아웃 마스터 서비스 구성 파일에서 지정한 포트 번호가 올바른지 확인 하 고 스케일 아웃 마스터 서비스를 다시 시작 합니다. 

2 단계: 스케일 아웃 작업자 서비스 구성에 지정 된 마스터 끝점 올바른지 확인 하 고 스케일 아웃 작업자 서비스를 다시 시작 합니다.

3 단계: 방화벽 포트 스케일 아웃 마스터 노드에서 열려 있는지 확인 합니다.

4 단계: 스케일 아웃 마스터 노드 및 스케일 아웃 작업자 노드 사이의 모든 다른 연결 문제를 해결 합니다.

**대/소문자**

System.ServiceModel.Security.SecurityNegotiationException: 기관과 SSL/TLS 보안 채널에 대 한 트러스트 관계를 설정할 수 없습니다 '*[컴퓨터 이름]: [Port]*'. System.Net.WebException--->: 기본 연결이 닫혔습니다: SSL/TLS 보안 채널에 대 한 트러스트 관계를 설정할 수 없습니다. System.Security.Authentication.AuthenticationException--->: 원격 인증서 유효성 검사 절차에 따라 올바르지 않습니다.

1 단계: 설치 스케일 아웃 마스터 노드 스케일 아웃 작업자에서 로컬 컴퓨터의 루트 인증서 저장소에 인증서 하지 않은 경우 아직 설치 및 스케일 아웃 Worker 서비스를 다시 시작 하십시오.

2 단계: 마스터 끝점에 있는 호스트 이름과 Cn 스케일 아웃 마스터의 인증서에 포함 되어 있는지 확인 합니다. 그렇지 않은 경우에 스케일 아웃 작업자 구성 파일에서 마스터 끝점을 다시 설정 하 고 스케일 아웃 작업자 서비스를 다시 시작 합니다. 

> [!Note]
> DNS 설정으로 인해 마스터 끝점의 호스트 이름을 변경할 수 없는 경우에 스케일 아웃 마스터 인증서를 변경 해야 합니다. 참조 [SSIS 스케일 아웃에 인증서를 다루는](deal-with-certificates-in-ssis-scale-out.md)합니다.

3 단계: 스케일 아웃 작업자 구성에 지정 된 마스터 지문 스케일 아웃 마스터 인증서의 지문이 일치 하는지 확인 합니다. 

**대/소문자**

System.ServiceModel.Security.SecurityNegotiationException: 설정할 수 없습니다 보안 채널에 대 한 SSL/TLS 기관과 '*[컴퓨터 이름]: [Port]*'. System.Net.WebException--->: 요청이 중단 되었습니다: SSL/TLS 보안 채널을 만들 수 없습니다.

1 단계: 스케일 아웃 Worker 서비스를 실행 하는 계정 아래의 명령에 의해 스케일 아웃 작업자 인증서에 대 한 액세스를에 있는지 확인 합니다.

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

계정에 액세스 하는 경우 아래 명령에 의해 부여 하 고 스케일 아웃 작업자 서비스를 다시 시작 합니다.

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

**대/소문자**

System.ServiceModel.Security.MessageSecurityException: HTTP 요청이 클라이언트 인증 구성표 '익명' 금지 되었습니다. System.Net.WebException--->: 원격 서버에 오류가 반환 되었습니다: (403) 사용할 수 없음.

1 단계: 스케일 아웃 작업자 설치 스케일 아웃 마스터 노드에서 로컬 컴퓨터의 루트 인증서 저장소에 인증서 하지 않은 경우 아직 설치 및 스케일 아웃 작업자 서비스를 다시 시작 합니다.

2 단계: 스케일 아웃 마스터 노드에서 로컬 컴퓨터의 루트 인증서 저장소에 사용할 인증서를 정리 합니다.

3 단계: 스케일 아웃 마스터 노드 아래의 레지스트리 항목을 추가 하 여 TLS/SSL 핸드셰이크 과정에서 신뢰할 수 있는 루트 인증 기관의 목록의 더 이상 보낼 Schannel을 구성 합니다.

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

값 이름: SendTrustedIssuerList 

값 형식: REG_DWORD 

값 데이터: 0 (False)

**대/소문자**

System.ServiceModel.CommunicationException: https://에 HTTP 요청을 만드는 동안 오류가 발생 했습니다*[컴퓨터 이름]: [Port]*  /ClusterManagement/합니다. 이 수 때문을 HTTP로 서버 인증서를 제대로 구성 되지 않았습니다. HTTPS의 경우 SYS입니다. 이 클라이언트와 서버 사이 보안 바인딩이 불일치로 인해 발생할 수 또한 수 없습니다. 

1 단계: 스케일 아웃 마스터 인증서에 바인딩됩니다 마스터 끝점의 포트를 올바르게 아래 명령 사용 하 여 마스터 노드를 확인 합니다. 인증서 해시 표시 스케일 아웃 마스터 인증서 지문이과 일치 하는 경우를 확인 합니다.

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

바인딩이 잘못 된 경우 다음 명령을 사용 하 여 다시 설정 하 고 스케일 아웃 Worker 서비스를 다시 시작 합니다.

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root appid={random guid}
```

### <a name="symptoms"></a>**증상**
범위 확장의 실행이 시작 되지 않습니다.

### <a name="solution"></a>**해결 방법**

[SSISDB]에서 패키지를 실행 하기 위해 선택한 컴퓨터의 상태를 확인 합니다. [catalog]입니다. [worker_agents]입니다. 하나 이상의 작업자는 온라인 상태이 고 사용 하도록 설정 해야 합니다.

### <a name="symptoms"></a>**증상** 
패키지는 성공적으로 실행 되지만 로그 메시지가 없습니다.

### <a name="solution"></a>**해결 방법**

SQL Server 인증 허용 된 경우 Sql Server에서 SSISDB를 호스팅 확인 합니다.

> [!Note]  
> 스케일 아웃 로깅에 대 한 계정을 변경 되 면 참조 [스케일 아웃 로깅에 대 한 계정을 변경](change-logdb-account.md) 로깅용으로 사용 되는 연결 문자열을 확인 하 고 있습니다.

### <a name="symptoms"></a>**증상**
패키지 실행 보고서에서 오류 메시지 문제 해결을 위한 충분 한 되지 않습니다.

### <a name="solution"></a>**해결 방법**
더 많은 실행 로그 TasksRootFolder WorkerSettings.config에 구성에서 찾을 수 있습니다. 기본적으로는 \<드라이버\>: \Users\\*[계정]*\AppData\Local\SSIS\ScaleOut\Tasks 합니다. *[계정]* 기본값 SSISScaleOutWorker140 스케일 아웃 작업자 서비스를 실행 하는 계정입니다.

사용 하 여 패키지 실행에 대 한 로그를 찾을 *[실행 id]*를 가져오려는 아래 T-SQL 명령을 실행 하는 *[작업 id]*합니다. 그런 다음 명명 된 하위 폴더를 찾을 *[작업 id]* TasksRootFolder 아래.<sup> 1<sup>

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```
<sup>1</sup> 이 쿼리는 문제 해결 목적 한정 되 고 열기 스케일 아웃 작업자에 대 한 진단 로깅/시나리오는 나중에 향상 된 때를 변경 합니다. 
