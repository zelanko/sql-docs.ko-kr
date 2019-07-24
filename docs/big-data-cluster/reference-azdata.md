---
title: azdata 참조
titleSuffix: SQL Server big data clusters
description: Azdata 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8136c85f8c32e08423f3d199a021d4f60353b39
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68425993"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 [SQL Server 2019 빅 데이터 클러스터 (미리 보기)](big-data-cluster-overview.md)에 대 한 **azdata** 도구에 대 한 참조를 제공 합니다. **Azdata** 도구를 설치 하는 방법에 대 한 자세한 내용은 [install azdata to manage SQL Server 2019 빅 data 클러스터](deploy-install-azdata.md)를 참조 하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
|[azdata 앱](reference-azdata-app.md) | 응용 프로그램을 만들고, 삭제 하 고, 실행 하 고, 관리 합니다. |
|[azdata bdc](reference-azdata-bdc.md) | 빅 데이터 클러스터 SQL Server를 선택, 관리 및 작동 합니다. |
|[azdata 노트북](reference-azdata-notebook.md) | 터미널에서 노트북을 보고 실행 하 고 관리 하기 위한 명령입니다. |
[azdata 로그인](#azdata-login) | 클러스터의 컨트롤러 끝점에 로그인 합니다.
[azdata 로그 아웃](#azdata-logout) | 클러스터에서 로그 아웃 합니다.
|[azdata sql](reference-azdata-sql.md) | 사용자는 SQL DB CLI를 사용 하 여 T-sql을 통해 SQL Server와 상호 작용할 수 있습니다. |
## <a name="azdata-login"></a>azdata 로그인
클러스터가 배포 되 면 배포 중에 컨트롤러 끝점이 나열 됩니다 .이 끝점은 로그인 하는 데 사용 해야 합니다.  컨트롤러 끝점을 모르는 경우 시스템에서/.kube/config의 <user home>기본 위치에 클러스터의 kube config를 사용 하거나 KUBECONFIG env var (예: export KUBECONFIG = path/to/kube/config)를 사용 하 여 로그인 할 수 있습니다.
```bash
azdata login [--cluster-name -n] 
             [--controller-username -u]  
             [--controller-endpoint -e]  
             [--accept-eula -a]
```
### <a name="examples"></a>예
대화형으로 로그인 합니다. 인수로 지정 하지 않은 경우 클러스터 이름에는 항상에 대 한 메시지가 표시 됩니다. 시스템에 CONTROLLER_USERNAME, CONTROLLER_PASSWORD 및 ACCEPT_EULA env 변수가 설정 되어 있는 경우 이러한 변수를 묻는 메시지가 표시 되지 않습니다. 시스템에 kube 구성이 있거나 KUBECONFIG env var을 사용 하 여 구성에 대 한 경로를 지정 하는 경우 대화형 환경에서는 먼저 구성을 사용한 다음 구성에 실패 하는 경우 메시지를 표시 합니다.
```bash
azdata login
```
로그인 (비 대화형) 클러스터 이름, 컨트롤러 사용자 이름, 컨트롤러 끝점 및 EULA 승인 집합을 인수로 사용 하 여 로그인 합니다. 환경 변수 CONTROLLER_PASSWORD를 설정 해야 합니다.  컨트롤러 끝점을 지정 하지 않으려면 컴퓨터의 기본 위치 <user home>/.kube/config에 kube config를 지정 하거나 KUBECONFIG env var (예: export KUBECONFIG = path/to/kube/config)를 사용 하세요.
```bash
azdata login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
컴퓨터의 kube config와 CONTROLLER_USERNAME, CONTROLLER_PASSWORD 및 ACCEPT_EULA에 대 한 env var set를 사용 하 여 로그인 합니다.
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--cluster-name -n`
클러스터 이름입니다.
#### `--controller-username -u`
계정 사용자입니다. 이 인수를 사용 하지 않으려는 경우 환경 변수 CONTROLLER_USERNAME를 설정할 수 있습니다.
#### `--controller-endpoint -e`
클러스터 컨트롤러 끝점 "https://host:port ". 이 인수를 사용 하지 않으려는 경우 컴퓨터에서 kube 구성을 사용할 수 있습니다. 구성이/.kube/config의 <user home>기본 위치에 있는지 확인 하거나 KUBECONFIG env var을 사용 하십시오.
#### `--accept-eula -a`
사용 조건에 동의 하나요? [예/아니요]. 이 인수를 사용 하지 않으려면 환경 변수 ACCEPT_EULA을 ' y e s '로 설정할 수 있습니다. 이 제품에 대 한 사용 조건은에서 https://aka.ms/azdata-eula 볼 수 있습니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시 합니다.
#### `--help -h`
이 도움말 메시지를 표시 하 고 종료 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, table, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 [http://jmespath.org/](http://jmespath.org/]) 내용 및 예제는를 참조 하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그에--debug를 사용 합니다.
## <a name="azdata-logout"></a>azdata 로그 아웃
클러스터에서 로그 아웃 합니다.
```bash
azdata logout 
```
### <a name="examples"></a>예
이 사용자를 로그 아웃 합니다.
```bash
azdata logout
```
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시 합니다.
#### `--help -h`
이 도움말 메시지를 표시 하 고 종료 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, table, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 [http://jmespath.org/](http://jmespath.org/]) 내용 및 예제는를 참조 하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그에--debug를 사용 합니다.

## <a name="next-steps"></a>다음 단계

**Azdata** 도구를 설치 하는 방법에 대 한 자세한 내용은 [install azdata to manage SQL Server 2019 빅 data 클러스터](deploy-install-azdata.md)를 참조 하세요.
