---
title: mssqlctl 클러스터 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 클러스터 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 654888bc27fec43abb8a8f511b0de7a4972e4377
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66779259"
---
# <a name="mssqlctl-cluster"></a>mssqlctl 클러스터

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **클러스터** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl 클러스터 만들기](#mssqlctl-cluster-create) | 클러스터를 만듭니다.
[mssqlctl 클러스터 삭제](#mssqlctl-cluster-delete) | 클러스터를 삭제 합니다.
[mssqlctl cluster config](reference-mssqlctl-cluster-config.md) | 클러스터 구성 명령입니다.
[mssqlctl 클러스터 끝점](reference-mssqlctl-cluster-endpoint.md) | 끝점 명령입니다.
[mssqlctl 클러스터 상태](reference-mssqlctl-cluster-status.md) | 상태 명령입니다.
[mssqlctl 클러스터 디버그](reference-mssqlctl-cluster-debug.md) | 명령을 디버그 합니다.
[mssqlctl cluster storage-pool](reference-mssqlctl-cluster-storage-pool.md) | 클러스터 저장소 풀을 관리 합니다.
## <a name="mssqlctl-cluster-create"></a>mssqlctl 클러스터 만들기
SQL Server 빅 데이터 클러스터 만들기-kube 구성 ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD', 'DOCKER_USERNAME', 'DOCKER_PASSWORD', 'MSSQL_SA_PASSWORD', 'KNOX_PASSWORD'] 다음 환경 변수를 함께 시스템에 필요 합니다.
```bash
mssqlctl cluster create [--config-file -c] 
                        [--accept-eula -a]  
                        [--node-label -l]  
                        [--force -f]
```
### <a name="examples"></a>예
클러스터 배포 환경-단계별 필요한 값에 대 한 프롬프트가 나타납니다.
```bash
mssqlctl cluster create
```
인수를 사용 하 여 클러스터 배포입니다.
```bash
mssqlctl cluster create --accept-eula yes --config-file aks-dev-test.json
```
인수-프롬프트 없이 사용 하 여 클러스터 배포 플래그가 사용 됩니다.--force로 제공 됩니다.
```bash
mssqlctl cluster create --accept-eula yes --config-file aks-dev-test.json --force
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--config-file -c`
구성 프로필, 클러스터를 배포 하는 데 클러스터: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-개발-test.json']
#### `--accept-eula -a`
사용 약관 수락 하 시겠습니까? [yes/no]. '예'로 ACCEPT_EULA 환경 변수를 설정할 수 있습니다이 인수를 사용.
#### `--node-label -l`
클러스터 노드 레이블에 배포할 노드를 지정 하는 데 사용 합니다.
#### `--force -f`
강제 값에 대 한 사용자를 묻지 않습니다를 만들고, stderr의 일환으로 모든 문제가 표시 됩니다.
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
## <a name="mssqlctl-cluster-delete"></a>mssqlctl 클러스터 삭제
SQL Server 빅 데이터 클러스터를 삭제-kube 구성 ['CONTROLLER_USERNAME', 'CONTROLLER_PASSWORD'] 다음 환경 변수를 함께 시스템에 필요 합니다.
```bash
mssqlctl cluster delete --name -n 
                        [--force -f]
```
### <a name="examples"></a>예
컨트롤러 사용자 이름 및 암호 설정 되어 있는 이미 시스템 환경의 클러스터 삭제 합니다.
```bash
mssqlctl cluster delete --name <cluster_name>
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
Kubernetes 네임 스페이스에 대해 사용 되는 클러스터 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--force -f`
강제 삭제 클러스터입니다.
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

다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다. 설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.
