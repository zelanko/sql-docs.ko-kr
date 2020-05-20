---
title: azdata bdc 참조
titleSuffix: SQL Server big data clusters
description: azdata bdc 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d5d5cb5256f4a1b8389d882300a89f0ee0012a99
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74820980"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

다음 문서에서는 `azdata` 도구의 `bdc` 명령에 대한 참조를 제공합니다. 다른 `azdata` 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc create](#azdata-bdc-create) | 빅 데이터 클러스터를 만듭니다.
[azdata bdc delete](#azdata-bdc-delete) | 빅 데이터 클러스터를 삭제합니다.
[azdata bdc upgrade](#azdata-bdc-upgrade) | SQL Server 빅 데이터 클러스터의 각 컨테이너에 배포된 이미지를 업데이트합니다.
[azdata bdc config](reference-azdata-bdc-config.md) | 구성 명령입니다.
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | 엔드포인트 명령입니다.
[azdata bdc debug](reference-azdata-bdc-debug.md) | 디버그 명령입니다.
[azdata bdc status](reference-azdata-bdc-status.md) | BDC 상태 명령입니다.
[azdata bdc control](reference-azdata-bdc-control.md) | 제어 서비스 명령입니다.
[azdata bdc sql](reference-azdata-bdc-sql.md) | Sql 서비스 명령입니다.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | Hdfs 서비스 명령입니다.
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark 서비스 명령입니다.
[azdata bdc gateway](reference-azdata-bdc-gateway.md) | 게이트웨이 서비스 명령입니다.
[azdata bdc app](reference-azdata-bdc-app.md) | 앱 서비스 명령입니다.
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark 명령을 통해 사용자가 세션, 문, 일괄 처리를 만들고 관리하여 Spark 시스템을 조작할 수 있습니다.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | HDFS 모듈은 HDFS 파일 시스템에 액세스하기 위한 명령을 제공합니다.
## <a name="azdata-bdc-create"></a>azdata bdc create
SQL Server 빅 데이터 클러스터 만들기 - 시스템에 Kubernetes 구성과 환경 변수 ['AZDATA_USERNAME', 'AZDATA_PASSWORD']가 필요합니다.
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  [--accept-eula -a]  
                  [--node-label -l]  
                  [--force -f]
```
### <a name="examples"></a>예
안내에 따른 BDC 배포 환경 - 필요한 값에 대한 프롬프트가 표시됩니다.
```bash
azdata bdc create
```
인수를 사용하는 BDC 배포
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test
```
프로필의 기본 이름 대신 지정된 이름을 사용하는 BDC 배포
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test --force
```
인수를 사용하는 BDC 배포 - --force 플래그를 사용하므로 프롬프트가 제공되지 않습니다.
```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--name -n`
Kubernetes 네임스페이스에 사용되는 빅 데이터 클러스터 이름입니다.
#### `--config-profile -c`
클러스터를 배포하는 데 사용되는 빅 데이터 클러스터 구성 프로필입니다. ['kubeadm-dev-test', 'kubeadm-prod', 'aks-dev-test', 'aks-dev-test-ha']
#### `--accept-eula -a`
사용 조건에 동의하시겠습니까? [예/아니요]. 이 인수를 사용하지 않으려면 ACCEPT_EULA 환경 변수를 ‘yes’로 설정하면 됩니다. azdata 사용 조건은 https://aka.ms/eula-azdata-en 에서 볼 수 있고, 빅 데이터 클러스터 사용 조건은 Enterprise: https://go.microsoft.com/fwlink/?linkid=2104292 ,Standard: https://go.microsoft.com/fwlink/?linkid=2104294 ,Developer: https://go.microsoft.com/fwlink/?linkid=2104079 에서 볼 수 있습니다.
#### `--node-label -l`
배포할 노드를 지정하는 데 사용되는 빅 데이터 클러스터 노드 레이블입니다.
#### `--force -f`
강제로 만듭니다. 사용자에게 값을 입력하라는 메시지가 표시되지 않으며 모든 이슈가 stderr의 일부로 출력됩니다.
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
## <a name="azdata-bdc-delete"></a>azdata bdc delete
SQL Server 빅 데이터 클러스터 삭제 - 시스템에 Kubernetes 구성이 필요합니다.
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>예
BDC 삭제.
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
Kubernetes 네임스페이스에 사용되는 빅 데이터 클러스터 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--force -f`
빅 데이터 클러스터를 강제로 삭제합니다.
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
## <a name="azdata-bdc-upgrade"></a>azdata bdc upgrade
SQL Server 빅 데이터 클러스터의 각 컨테이너에 배포된 이미지를 업데이트합니다. 업데이트되는 이미지는 전달된 Docker 이미지에 따라 달라집니다. 업데이트되는 이미지가 현재 배포된 이미지와 다른 Docker 이미지 리포지토리에 있는 경우, “repository” 매개 변수도 필요합니다.
```bash
azdata bdc upgrade --name -n 
                   --tag -t  
                   [--repository -r]
```
### <a name="examples"></a>예
동일한 리포지토리에서 새 이미지 태그 “cu2”로 BDC를 업그레이드합니다.
```bash
azdata bdc upgrade -t cu2
```
새 리포지토리 “foo/bar/baz”에서 태그 “cu2”로 BDC를 새 이미지로 업그레이드합니다.
```bash
azdata bdc upgrade -t cu2 -r foo/bar/baz
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
Kubernetes 네임스페이스에 사용되는 빅 데이터 클러스터 이름입니다.
#### `--tag -t`
클러스터에 있는 모든 컨테이너를 업그레이드할 대상 Docker 이미지 태그입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--repository -r`
클러스터에 있는 모든 컨테이너가 이미지를 가져올 Docker 리포지토리입니다.
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
