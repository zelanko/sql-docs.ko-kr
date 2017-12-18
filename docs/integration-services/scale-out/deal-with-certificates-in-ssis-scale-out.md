---
title: "SQL Server Integration Services Scale Out의 인증서 처리 | Microsoft Docs"
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
ms.openlocfilehash: e09fec1fcf9cf0221dad50d708adef773b297237
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="deal-with-certificates-in-sql-server-integration-services-scale-out"></a>SQL Server Integration Services Scale Out의 인증서 처리

Scale Out 마스터와 Scale Out 작업자 사이의 통신을 보호하기 위해 Scale Out에는 Scale Out 마스터 인증서와 Scale Out 작업자 인증서라는 두 개의 인증서가 사용됩니다. 

## <a name="scale-out-master-certificate"></a>Scale Out 마스터 인증서

대부분의 경우 Scale Out 마스터 인증서는 Scale Out 마스터 설치 중에 구성됩니다.

SQL Server 설치 마법사의 **Integration Services Scale Out 구성 - 마스터 노드** 페이지에서 자체 서명 SSL 인증서를 새로 만들거나 기존 SSL 인증서를 사용하도록 선택할 수 있습니다.

![마스터 구성](media/master-config.PNG)

인증서에 특별한 요구 사항이 없는 경우 자체 서명 SSL 인증서를 새로 만들도록 선택할 수 있습니다. 인증서의 CN을 더 지정할 수 있습니다. 나중에 Scale Out 작업자에 사용되는 마스터 엔드포인트의 호스트 이름이 CN에 포함되어야 합니다. 기본적으로 컴퓨터 이름과 마스터 노드의 IP가 포함됩니다. 

기존 인증서를 사용하도록 선택하는 경우 로컬 컴퓨터의 **루트** 인증서 저장소에서 "찾아보기..."를 클릭하여 SSL 인증서를 선택합니다.

### <a name="change-scale-out-master-certificate"></a>Scale Out 마스터 인증서 변경

인증서 만료 또는 다른 이유로 인해 Scale Out 마스터 인증서를 변경할 수 있습니다. 다음 단계를 수행합니다.

#### <a name="1-create-a-ssl-certificate"></a>1. SSL 인증서를 만듭니다.
다음 명령을 사용하여 마스터 노드에 SSL 인증서를 만들고 설치합니다.
```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
예:
```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-master-port"></a>2. 인증서를 마스터 포트에 바인딩
다음 명령으로 원래 바인딩을 확인합니다.
```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```
예:
```dos
netsh http show sslcert ipport=0.0.0.0:8391
```
다음 명령을 사용하여 원래 바인딩을 삭제하고 새 바인딩을 설정합니다.
```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```
예:
```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```
#### <a name="3-update-scale-out-master-service-configuration-file"></a>3. Scale Out 마스터 서비스 구성 파일 업데이트
마스터 노드에서 Scale Out 마스터 서비스 구성 파일인 \<드라이버\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config를 업데이트합니다. **SSLCertThumbprint**를 새 SSL 인증서의 지문으로 업데이트합니다.

#### <a name="4-restart-scale-out-master-service"></a>4. Scale Out 마스터 서비스 다시 시작

#### <a name="5-reconnect-scale-out-worker-to-scale-out-master"></a>5. Scale Out 작업자를 Scale Out 마스터에 다시 연결
각 Scale Out 작업자에 대해 작업자를 삭제하고 [Scale Out 관리자](integration-services-ssis-scale-out-manager.md)로 다시 추가하거나 아래에서 5.1~5.3 단계를 수행합니다.

5.1 작업자 노드에서 로컬 컴퓨터의 루트 저장소에 클라이언트 SSL 인증서 설치

5.2 Scale Out 작업자 구성 파일 업데이트 작업자 노드에서 Scale Out 작업자 서비스 구성 파일인 \<드라이버\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config를 업데이트합니다. **MasterHttpsCertThumbprint**를 새 SSL 인증서의 지문으로 업데이트합니다.

5.3 Scale Out 작업자 서비스 다시 시작


## <a name="scale-out-worker-certificate"></a>Scale Out 작업자 인증서

Scale Out 작업자 인증서는 Scale Out 작업자를 설치하는 동안 자동으로 생성됩니다. 

### <a name="change-scale-out-worker-certificate"></a>Scale Out 작업자 인증서 변경

Scale Out 작업자 인증서를 변경하려는 경우 다음 단계를 수행합니다.

#### <a name="1-create-a-certificate"></a>1. 인증서 만들기
다음 명령을 사용하여 인증서를 만들고 설치합니다.
```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
예:
```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
#### <a name="2-install-the-client-certificate-to-the-root-store-of-local-machine-on-worker-node"></a>2. 작업자 노드에서 로컬 컴퓨터의 루트 저장소에 클라이언트 인증서 설치

#### <a name="3-give-service-access-to-the-certificate"></a>3. 인증서에 서비스 액세스 권한 부여
다음 명령을 사용하여 이전 인증서를 삭제하고 새 인증서에 Scale Out 작업자 서비스에 대한 액세스 권한을 부여합니다.
```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```
예:
```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```
#### <a name="4-update-scale-out-worker-configuration-file"></a>4. Scale Out 작업자 구성 파일 업데이트
작업자 노드에서 Scale Out 작업자 서비스 구성 파일인 \<드라이버\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config를 업데이트합니다. **WorkerHttpsCertThumbprint**를 새 인증서의 지문으로 업데이트합니다.

#### <a name="5-install-the-client-certificate-to-the-root-store-of-local-machine-on-master-node"></a>5. 마스터 노드에서 로컬 컴퓨터의 루트 저장소에 클라이언트 인증서 설치

#### <a name="6-restart-scale-out-worker-service"></a>6. Scale Out 작업자 서비스 다시 시작
