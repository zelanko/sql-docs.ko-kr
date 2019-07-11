---
title: mssqlctl 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a30f78b24a85f85b85beb914dc0f26af652242fd
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728538"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **mssqlctl** 에 대 한 도구 [SQL Server 2019 빅 데이터 클러스터 (미리 보기)](big-data-cluster-overview.md)합니다. 설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
|[mssqlctl 앱](reference-mssqlctl-app.md) | 만들기, 삭제, 실행 및 응용 프로그램을 관리 합니다. |
|[mssqlctl bdc](reference-mssqlctl-bdc.md) | 선택 하 고, 관리 및 SQL Server 빅 데이터 클러스터에 작동 합니다. |
|[mssqlctl hdfs](reference-mssqlctl-hdfs.md) | HDFS 모듈 HDFS에 액세스 하는 명령 파일 시스템을 제공 합니다. |
[mssqlctl login](#mssqlctl-login) | 클러스터의 컨트롤러 끝점에 로그인 합니다.
[mssqlctl logout](#mssqlctl-logout) | 로그 아웃 클러스터 합니다.
|[mssqlctl sql](reference-mssqlctl-sql.md) | SQL DB CLI T-SQL을 통해 SQL Server와 상호 작용할 수가 있습니다. |
## <a name="mssqlctl-login"></a>mssqlctl 로그인
사용 해야 하는 배포 하는 동안 컨트롤러 끝점을 나열 하는 클러스터에 배포 하는 경우 로그인 합니다.  할 컨트롤러 끝점을 알 수 없는 경우 로그인의 기본 위치에 시스템에서 클러스터 kube 구성 함으로써 <user home>/.kube/config 또는 KUBECONFIG env var을 사용 하 여, 즉 KUBECONFIG=path/to/.kube/config를 내보냅니다.
```bash
mssqlctl login [--cluster-name -n] 
               [--controller-username -u]  
               [--controller-endpoint -e]  
               [--accept-eula -a]
```
### <a name="examples"></a>예
대화형으로 로그인 합니다. 클러스터 이름은 항상 묻는 메시지가 표시 되지 않으면 될 인수로 서 지정. CONTROLLER_USERNAME, CONTROLLER_PASSWORD, 및 ACCEPT_EULA 환경 변수를 시스템에서 설정에 있는 경우 이러한 하지 묻는 합니다. Kube 구성 시스템에 있거나 있습니다 KUBECONFIG env var을 사용 하 여 구성에 대 한 경로 지정 하는 경우 대화형 환경을 먼저 시도 구성을 사용 하 고 다음을 구성 하지 못하면 묻는 합니다.
```bash
mssqlctl login
```
(비 대화형)에 로그인 합니다. 클러스터 이름, 컨트롤러 사용자 이름, 컨트롤러 끝점 및 EULA 동의 인수로 로그인 합니다. 환경 변수 CONTROLLER_PASSWORD 설정 되어야 합니다.  컨트롤러 끝점을 지정 하지 않을 경우 하세요 미치는 kube 구성 컴퓨터의 기본 위치에서 <user home>/.kube/config 또는 KUBECONFIG env var을 사용 하 여, 즉 KUBECONFIG=path/to/.kube/config를 내보냅니다.
```bash
mssqlctl login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
컴퓨터 및 env var CONTROLLER_USERNAME, CONTROLLER_PASSWORD, 및 ACCEPT_EULA 설정 kube 구성으로 로그인 합니다.
```bash
mssqlctl login -n ClusterName
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--cluster-name -n`
클러스터 이름입니다.
#### `--controller-username -u`
사용자 계정입니다. 이 인수를 사용 하지 않을 경우 CONTROLLER_USERNAME 환경 변수를 설정할 수 있습니다.
#### `--controller-endpoint -e`
클러스터 컨트롤러 끝점 "https://host:port"입니다. 이 인수를 사용 하지 않을 경우 kube 구성 컴퓨터에 사용할 수 있습니다. 기본 위치 구성에 위치한를 확인 하세요 <user home>/.kube/config 또는 KUBECONFIG env 변수에 사용
#### `--accept-eula -a`
사용 약관 수락 하 시겠습니까? [yes/no]. '예'로 ACCEPT_EULA 환경 변수를 설정할 수 있습니다이 인수를 사용.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.
## <a name="mssqlctl-logout"></a>mssqlctl 로그 아웃
로그 아웃 클러스터 합니다.
```bash
mssqlctl logout 
```
### <a name="examples"></a>예
이 사용자를 로그 아웃이 있습니다.
```bash
mssqlctl logout
```
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.

## <a name="next-steps"></a>다음 단계

설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.