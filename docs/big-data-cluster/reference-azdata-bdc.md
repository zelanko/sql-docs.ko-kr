---
title: azdata bdc 참조
titleSuffix: SQL Server big data clusters
description: azdata bdc 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 488394cbf4b52a952ffc46ab2ec6c9a273466bd5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68426043"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **azdata** 도구의 **bdc** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|     |     |
| --- | --- |
[azdata bdc create](#azdata-bdc-create) | 빅 데이터 클러스터를 만듭니다.
[azdata bdc delete](#azdata-bdc-delete) | 빅 데이터 클러스터를 삭제합니다.
[azdata bdc config](reference-azdata-bdc-config.md) | 구성 명령입니다.
[azdata bdc endpoint](reference-azdata-bdc-endpoint.md) | 엔드포인트 명령입니다.
[azdata bdc status](reference-azdata-bdc-status.md) | 상태 명령입니다.
[azdata bdc debug](reference-azdata-bdc-debug.md) | 디버그 명령입니다.
[azdata bdc control](reference-azdata-bdc-control.md) | 제어 명령입니다.
[azdata bdc pool](reference-azdata-bdc-pool.md) | 풀 명령입니다.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | HDFS 모듈은 HDFS 파일 시스템에 액세스하기 위한 명령을 제공합니다.
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark 명령을 통해 사용자가 세션, 문, 일괄 처리를 만들고 관리하여 Spark 시스템을 조작할 수 있습니다.
## <a name="azdata-bdc-create"></a>azdata bdc create
SQL Server 빅 데이터 클러스터를 만듭니다. [‘CONTROLLER_USERNAME’, ‘CONTROLLER_PASSWORD’, ‘MSSQL_SA_PASSWORD’, ‘KNOX_PASSWORD’] 등의 환경 변수와 함께 시스템에 kube 구성이 있어야 합니다.
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
클러스터를 배포하는 데 사용되는 빅 데이터 클러스터 구성 프로필입니다. 예: [’aks-dev-test’, ‘kubeadm-dev-test’, ‘minikube-dev-test’]
#### `--accept-eula -a`
사용 조건에 동의하시겠습니까? [예/아니요]. 이 인수를 사용하지 않으려면 ACCEPT_EULA 환경 변수를 ‘yes’로 설정하면 됩니다. 이 제품의 사용 조건은 https://aka.ms/azdata-eula 및 https://go.microsoft.com/fwlink/?LinkId=2002534 에서 볼 수 있습니다.
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
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-delete"></a>azdata bdc delete
SQL Server 빅 데이터 클러스터를 삭제합니다. [‘CONTROLLER_USERNAME’, ‘CONTROLLER_PASSWORD’] 등의 환경 변수와 함께 시스템에 kube 구성이 있어야 합니다.
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>예
시스템 환경에 컨트롤러 사용자 이름 및 암호가 이미 설정되어 있는 경우의 BDC 삭제
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
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.

## <a name="next-steps"></a>다음 단계

다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요. **azdata** 도구를 설치하는 방법에 대한 자세한 내용은 [azdata를 설치하여 SQL Server 2019 빅 데이터 클러스터 관리](deploy-install-azdata.md)를 참조하세요.
