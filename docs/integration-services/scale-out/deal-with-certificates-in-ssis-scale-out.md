---
title: "Sql Server Integration Services 스케일 아웃에 인증서를 다루는 | Microsoft Docs"
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2970b2b2cc7cf30c18a203ebbb92b5418bfc9be5
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="deal-with-certificates-in-sql-server-integration-services-scale-out"></a>SQL Server Integration Services 스케일 아웃의 인증서로 처리 합니다.

스케일 아웃 마스터 및 스케일 아웃 작업자 간의 통신을 보호 하려면 두 개의 인증서는 스케일 아웃 마스터 인증서 및 스케일 아웃 작업자 인증서 즉, 스케일 아웃에 사용 됩니다. 

## <a name="scale-out-master-certificate"></a>스케일 아웃 마스터 인증서

대부분의 경우에서 스케일 아웃 마스터 인증서는 스케일 아웃 마스터의 설치 중 구성 됩니다.

에 **Integration Services 스케일 아웃 구성-마스터 노드** 페이지 SQL Server 설치 마법사의 새 자체 서명 된 SSL 인증서를 만들거나 기존 SSL 인증서를 사용 하도록 선택할 수 있습니다.

![마스터 구성](media/master-config.PNG)

인증서에 특별 한 요구 사항이 없다면 새 자체 서명 된 SSL 인증서를 만들 수 있습니다. 인증서의 Cn을 추가로 지정할 수 있습니다. 나중에 스케일 아웃 작업자에서 사용 하는 마스터 끝점의 호스트 이름을 Cn에 연결 되어 있는지 확인 합니다. 기본적으로 컴퓨터 이름 및 ip 마스터 노드의 포함 됩니다. 

기존 인증서를 사용 하기로 선택한 경우 클릭에서 SSL 인증서를 선택 하려면 "찾아보기..." **루트** 로컬 컴퓨터의 인증서 저장소입니다.

### <a name="change-scale-out-master-certificate"></a>스케일 아웃 마스터 인증서 변경

인증서가 만료 또는 다른 이유로 인해 스케일 아웃 마스터 인증서를 변경 수 있습니다. 다음 단계를 수행 합니다.

#### <a name="1-create-a-ssl-certificate"></a>1. SSL 인증서를 만듭니다.
만들고 마스터에서 SSL 인증서를 설치 합니다. 다음 명령 사용 하 여 노드:
```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
예:
```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-master-port"></a>2. 마스터에 인증서 바인딩 포트
명령 사용 하 여 원래 바인딩을 확인 합니다.
```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```
예:
```dos
netsh http show sslcert ipport=0.0.0.0:8391
```
원래 바인딩을 삭제 하 고 다음 명령 사용 하 여 새 바인딩을 설정 합니다.
```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```
예:
```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```
#### <a name="3-update-scale-out-master-service-configuration-file"></a>3. 스케일 아웃 마스터 서비스 구성 파일 업데이트
서비스 구성 파일을 스케일 아웃 마스터 업데이트 \<드라이버\>: files\microsoft SQL Server\140\DTS\Binn\MasterSettings.config 마스터 노드. 업데이트 **SSLCertThumbprint** 새 SSL 인증서의 지문을 합니다.

#### <a name="4-restart-scale-out-master-service"></a>4. 스케일 아웃 마스터 서비스를 다시 시작

#### <a name="5-reconnect-scale-out-worker-to-scale-out-master"></a>5. 작업자 마스터 확장의 확장을 다시 연결
각 스케일 아웃 작업자에 대해 작업자를 삭제 하거나 고이 사용 하 여 다시 추가할 [스케일 아웃 관리자](integration-services-ssis-scale-out-manager.md) 하거나 아래 5.1을 5.3 단계를 수행 합니다.

5.1 작업자 노드에서 로컬 컴퓨터의 루트 저장소에 클라이언트 SSL 인증서 설치

5.2 작업자 서비스 구성 파일 업데이트 작업자 스케일 아웃 서비스 구성 파일을 Out 배율 업데이트 \<드라이버\>: files\microsoft SQL Server\140\DTS\Binn\WorkerSettings.config 작업자 노드. 업데이트 **MasterHttpsCertThumbprint** 새 SSL 인증서의 지문을 합니다.

5.3 작업자 서비스 소수 자릿수를 다시 시작


## <a name="scale-out-worker-certificate"></a>스케일 아웃 작업자 인증서

스케일 아웃 작업자 인증서의 스케일 아웃 Worker가 설치 하는 동안 자동으로 생성 됩니다. 

### <a name="change-scale-out-worker-certificate"></a>스케일 아웃 작업자 인증서 변경

스케일 아웃 작업자 인증서를 변경 하려는 경우 다음 단계를 수행 합니다.

#### <a name="1-create-a-certificate"></a>1. 인증서 만들기
페이지를 만들고 다음 명령을 사용 하 여 인증서를 설치 합니다.
```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
예:
```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
#### <a name="2-install-the-client-certificate-to-the-root-store-of-local-machine-on-worker-node"></a>2. 작업자 노드에 로컬 컴퓨터의 루트 저장소에 클라이언트 인증서를 설치 합니다.

#### <a name="3-give-service-access-to-the-certificate"></a>3. 인증서 귀하에 게 서비스 액세스
이전 인증서를 삭제 하 고 명령 사용 하 여 새 인증서로 스케일 아웃 작업자 서비스 액세스 권한을 부여 합니다.
```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```
예:
```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```
#### <a name="4-update-scale-out-worker-configuration-file"></a>4. 스케일 아웃 작업자 구성 파일 업데이트
서비스 구성 파일을 스케일 아웃 작업자 업데이트 \<드라이버\>: files\microsoft SQL Server\140\DTS\Binn\WorkerSettings.config 작업자 노드. 업데이트 **WorkerHttpsCertThumbprint** 새 인증서의 지문을 합니다.

#### <a name="5-install-the-client-certificate-to-the-root-store-of-local-machine-on-master-node"></a>5. 마스터 로컬 컴퓨터의 루트 저장소에 클라이언트 인증서를 설치 합니다. 노드

#### <a name="6-restart-scale-out-worker-service"></a>6. 스케일 아웃 작업자 서비스를 다시 시작

