---
title: azdata 참조
titleSuffix: SQL Server big data clusters
description: azdata 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8136c85f8c32e08423f3d199a021d4f60353b39
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68425993"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 [SQL Server 2019 빅 데이터 클러스터(미리 보기)](big-data-cluster-overview.md)의 **azdata** 도구에 대한 참조를 제공합니다. **azdata** 도구를 설치하는 방법에 대한 자세한 내용은 [azdata를 설치하여 SQL Server 2019 빅 데이터 클러스터 관리](deploy-install-azdata.md)를 참조하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
|[azdata app](reference-azdata-app.md) | 애플리케이션을 만들고, 삭제, 실행, 관리합니다. |
|[azdata bdc](reference-azdata-bdc.md) | SQL Server 빅 데이터 클러스터를 선택, 관리, 운영합니다. |
|[azdata notebook](reference-azdata-notebook.md) | 터미널에서 Notebook을 보고, 실행, 관리하기 위한 명령입니다. |
[azdata login](#azdata-login) | 클러스터의 컨트롤러 엔드포인트에 로그인합니다.
[azdata logout](#azdata-logout) | 클러스터에서 로그아웃합니다.
|[azdata sql](reference-azdata-sql.md) | SQL DB CLI를 사용하여 사용자가 T-SQL을 통해 SQL Server를 조작할 수 있습니다. |
## <a name="azdata-login"></a>azdata login
클러스터가 배포된 경우 배포 중에 컨트롤러 엔드포인트가 나열됩니다. 이 엔드포인트를 사용하여 로그인해야 합니다.  컨트롤러 엔드포인트를 모르는 경우 시스템의 기본 위치인 <user home>/.kube/config에 클러스터의 kube 구성을 저장하여 로그인하거나, KUBECONFIG 환경 변수를 사용할 수 있습니다(즉, export KUBECONFIG=path/to/.kube/config).
```bash
azdata login [--cluster-name -n] 
             [--controller-username -u]  
             [--controller-endpoint -e]  
             [--accept-eula -a]
```
### <a name="examples"></a>예
대화형으로 로그인합니다. 인수로 지정하지 않은 경우 클러스터 이름을 묻는 메시지가 항상 표시됩니다. 시스템에 CONTROLLER_USERNAME, CONTROLLER_PASSWORD 및 ACCEPT_EULA 환경 변수가 설정되어 있으면 이러한 메시지가 표시되지 않습니다. 시스템에 kube 구성이 있거나 KUBECONFIG 환경 변수를 사용하여 구성 경로를 지정하면, 대화형 환경에서 먼저 구성을 사용하려고 하며, 구성이 실패할 경우 사용자에게 확인 메시지를 표시합니다.
```bash
azdata login
```
비대화형으로 로그인합니다. 클러스터 이름, 컨트롤러 사용자 이름, 컨트롤러 엔드포인트 및 EULA 동의를 인수로 설정하여 로그인합니다. CONTROLLER_PASSWORD 환경 변수를 설정해야 합니다.  컨트롤러 엔드포인트를 지정하지 않으려면 해당 머신의 기본 위치인 <user home>/.kube/config에 kube 구성을 저장하거나, KUBECONFIG 환경 변수를 사용합니다(즉, export KUBECONFIG=path/to/.kube/config).
```bash
azdata login --cluster-name ClusterName --controller-user johndoe@contoso.com  --controller-endpoint https://<ip>:30080 --accept-eula yes
```
머신에 kube 구성을 저장하고 CONTROLLER_USERNAME, CONTROLLER_PASSWORD 및 ACCEPT_EULA 환경 변수를 설정하여 로그인합니다.
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--cluster-name -n`
클러스터 이름입니다.
#### `--controller-username -u`
계정 사용자입니다. 이 인수를 사용하지 않으려면 CONTROLLER_USERNAME 환경 변수를 설정하면 됩니다.
#### `--controller-endpoint -e`
클러스터 컨트롤러 엔드포인트 “https://host:port ”입니다. 이 인수를 사용하지 않으려면 해당 머신의 kube 구성을 사용할 수 있습니다. 구성이 기본 위치인 <user home>/.kube/config에 있는지 확인하거나, KUBECONFIG 환경 변수를 사용합니다.
#### `--accept-eula -a`
사용 조건에 동의하시겠습니까? [예/아니요]. 이 인수를 사용하지 않으려면 ACCEPT_EULA 환경 변수를 ‘yes’로 설정하면 됩니다. 이 제품의 사용 조건은 https://aka.ms/azdata-eula 에서 볼 수 있습니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-logout"></a>azdata logout
클러스터에서 로그아웃합니다.
```bash
azdata logout 
```
### <a name="examples"></a>예
이 사용자를 로그아웃합니다.
```bash
azdata logout
```
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.

## <a name="next-steps"></a>다음 단계

**azdata** 도구를 설치하는 방법에 대한 자세한 내용은 [azdata를 설치하여 SQL Server 2019 빅 데이터 클러스터 관리](deploy-install-azdata.md)를 참조하세요.
