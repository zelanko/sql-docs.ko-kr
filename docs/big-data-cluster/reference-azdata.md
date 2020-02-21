---
title: azdata 참조
titleSuffix: SQL Server big data clusters
description: azdata 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 94adabb2ace2f5619abd700b2652aa7d88f3e1aa
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74822348"
---
# <a name="azdata"></a>azdata

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

이 참조 문서에서는 `azdata` 명령에 대해 설명합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
|[azdata bdc](reference-azdata-bdc.md) | SQL Server 빅 데이터 클러스터를 선택, 관리, 운영합니다. |
|[azdata app](reference-azdata-app.md) | 애플리케이션을 만들고, 삭제, 실행, 관리합니다. |
[azdata login](#azdata-login) | 클러스터의 컨트롤러 엔드포인트에 로그인하고 네임스페이스를 활성 컨텍스트로 설정합니다. 로그인 시 암호를 사용하려면 AZDATA_PASSWORD 환경 변수를 설정해야 합니다.
[azdata logout](#azdata-logout) | 클러스터에서 로그아웃합니다.
|[azdata context](reference-azdata-context.md) | 컨텍스트 관리 명령입니다. |
|[azdata control](reference-azdata-control.md) | 컨트롤 플레인을 만들고, 삭제하고, 관리합니다. |
|[azdata sql](reference-azdata-sql.md) | SQL DB CLI를 사용하여 사용자가 T-SQL을 통해 SQL Server를 조작할 수 있습니다. |
|[azdata notebook](reference-azdata-notebook.md) | 터미널에서 Notebook을 보고, 실행, 관리하기 위한 명령입니다. |
## <a name="azdata-login"></a>azdata login
클러스터가 배포된 경우 배포 중에 컨트롤러 엔드포인트가 나열됩니다. 이 엔드포인트를 사용하여 로그인해야 합니다.  컨트롤러 엔드포인트를 모르는 경우 시스템의 기본 위치인 <user home>/.kube/config에 클러스터의 kube 구성을 저장하여 로그인하거나, KUBECONFIG 환경 변수를 사용할 수 있습니다(즉, export KUBECONFIG=path/to/.kube/config).  로그인하면 이 클러스터의 네임스페이스가 활성 컨텍스트로 설정됩니다.
```bash
azdata login [--auth] 
             [--endpoint -e]  
             [--accept-eula -a]  
             [--namespace -n]  
             [--username -u]  
             [--principal -p]
```
### <a name="examples"></a>예
기본 인증을 사용하여 로그인합니다.
```bash
azdata login --auth basic --username johndoe --endpoint https://<ip or domain name>:30080            
```
Active Directory를 사용하여 로그인합니다.
```bash
azdata login --auth ad --endpoint https://<ip or domain name>:30080                
```
명시적 보안 주체가 있는 Active Directory를 사용하여 로그인합니다.
```bash
azdata login --auth ad --principal johndoe@COSTOSO.COM --endpoint https://<ip or domain name>:30080
```
대화형으로 로그인합니다. 인수로 지정하지 않은 경우 클러스터 이름을 묻는 메시지가 항상 표시됩니다. 시스템에 AZDATA_USERNAME, AZDATA_PASSWORD 및 ACCEPT_EULA 환경 변수가 설정되어 있으면 이러한 메시지가 표시되지 않습니다. 시스템에 kube 구성이 있거나 KUBECONFIG 환경 변수를 사용하여 구성 경로를 지정하면, 대화형 환경에서 먼저 구성을 사용하려고 하며, 구성이 실패할 경우 사용자에게 확인 메시지를 표시합니다.
```bash
azdata login
```
비대화형으로 로그인합니다. 클러스터 이름, 컨트롤러 사용자 이름, 컨트롤러 엔드포인트 및 EULA 동의를 인수로 설정하여 로그인합니다. AZDATA_PASSWORD 환경 변수를 설정해야 합니다.  컨트롤러 엔드포인트를 지정하지 않으려면 해당 머신의 기본 위치인 <user home>/.kube/config에 kube 구성을 저장하거나, KUBECONFIG 환경 변수를 사용합니다(즉, export KUBECONFIG=path/to/.kube/config).
```bash
azdata login --namespace ClusterName --username johndoe@contoso.com  --endpoint https://<ip or domain name>:30080 --accept-eula yes
```
머신에 kube 구성을 저장하고 AZDATA_USERNAME, AZDATA_PASSWORD 및 ACCEPT_EULA 환경 변수를 설정하여 로그인합니다.
```bash
azdata login -n ClusterName
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--auth`
인증 전략입니다. 기본 또는 Active Directory 인증입니다. 기본값은 "기본" 인증입니다.
#### `--endpoint -e`
클러스터 컨트롤러 엔드포인트 “https://host:port ”입니다. 이 인수를 사용하지 않으려면 해당 머신의 kube 구성을 사용할 수 있습니다. 구성이 기본 위치인 <user home>/.kube/config에 있는지 확인하거나, KUBECONFIG 환경 변수를 사용합니다.
#### `--accept-eula -a`
사용 조건에 동의하시겠습니까? [예/아니요]. 이 인수를 사용하지 않으려면 ACCEPT_EULA 환경 변수를 ‘yes’로 설정하면 됩니다. 이 제품의 사용 조건은 https://aka.ms/eula-azdata-en 에서 볼 수 있습니다.
#### `--namespace -n`
클러스터 컨트롤 플레인의 네임스페이스입니다.
#### `--username -u`
계정 사용자입니다. 이 인수를 사용하지 않으려면 AZDATA_USERNAME 환경 변수를 설정하면 됩니다.
#### `--principal -p`
Kerberos 영역입니다. 대부분의 경우 Kerberos 영역은 도메인 이름(대문자)입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
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
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.

## <a name="next-steps"></a>다음 단계

다른 `azdata` 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요. `azdata` 도구를 설치하는 방법에 대한 자세한 내용은 [azdata를 설치하여 SQL Server 2019 빅 데이터 클러스터 관리](deploy-install-azdata.md)를 참조하세요.
