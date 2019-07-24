---
title: azdata bdc 참조
titleSuffix: SQL Server big data clusters
description: Azdata bdc 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 488394cbf4b52a952ffc46ab2ec6c9a273466bd5
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426043"
---
# <a name="azdata-bdc"></a>azdata bdc

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **azdata** 도구의 **bdc** 명령에 대 한 참조를 제공 합니다. 다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md)를 참조 하세요.

## <a name="commands"></a>명령

|     |     |
| --- | --- |
[azdata bdc 만들기](#azdata-bdc-create) | 빅 데이터 클러스터를 만듭니다.
[azdata bdc 삭제](#azdata-bdc-delete) | 빅 데이터 클러스터를 삭제 합니다.
[azdata bdc 구성](reference-azdata-bdc-config.md) | 구성 명령입니다.
[azdata bdc 끝점](reference-azdata-bdc-endpoint.md) | 끝점 명령입니다.
[azdata bdc 상태](reference-azdata-bdc-status.md) | 상태 명령입니다.
[azdata bdc 디버그](reference-azdata-bdc-debug.md) | 디버그 명령입니다.
[azdata bdc 컨트롤](reference-azdata-bdc-control.md) | 제어 명령입니다.
[azdata bdc 풀](reference-azdata-bdc-pool.md) | 풀 명령입니다.
[azdata bdc hdfs](reference-azdata-bdc-hdfs.md) | HDFS 모듈은 HDFS 파일 시스템에 액세스 하는 명령을 제공 합니다.
[azdata bdc spark](reference-azdata-bdc-spark.md) | Spark 명령을 사용 하면 사용자가 세션, 문 및 일괄 처리를 만들고 관리 하 여 Spark 시스템과 상호 작용할 수 있습니다.
## <a name="azdata-bdc-create"></a>azdata bdc 만들기
Kube config는 다음과 같은 환경 변수 [' CONTROLLER_USERNAME ', ' CONTROLLER_PASSWORD ', ' MSSQL_SA_PASSWORD ', ' KNOX_PASSWORD ']와 함께 시스템에서 SQL Server 빅 데이터 클러스터를 만듭니다.
```bash
azdata bdc create [--name -n] 
                  [--config-profile -c]  
                  [--accept-eula -a]  
                  [--node-label -l]  
                  [--force -f]
```
### <a name="examples"></a>예

단계별 BDC 배포 환경-필요한 값에 대 한 프롬프트를 받게 됩니다.

```bash
azdata bdc create
```

인수를 포함 하는 BDC 배포.

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test
```
프로필에서 기본 이름 대신 지정 된 이름을 사용 하는 BDC 배포
```bash
azdata bdc create --name <cluster_name> --accept-eula yes --config-profile aks-dev-test --force
```

인수를 사용 하 여 BDC 배포--force 플래그가 사용 되므로 프롬프트가 표시 되지 않습니다.

```bash
azdata bdc create --accept-eula yes --config-profile aks-dev-test --force
```

### <a name="optional-parameters"></a>선택적 매개 변수
#### `--name -n`
Kubernetes 네임 스페이스에 사용 되는 빅 데이터 클러스터 이름입니다.
#### `--config-profile -c`
클러스터를 배포 하는 데 사용 되는 빅 데이터 클러스터 구성 프로필: [' aks ', ' kubeadm ', ' minikube ']
#### `--accept-eula -a`
사용 조건에 동의 하나요? [예/아니요]. 이 인수를 사용 하지 않으려면 환경 변수 ACCEPT_EULA을 ' y e s '로 설정할 수 있습니다. 이 제품에 대 한 사용 조건은 및 https://aka.ms/azdata-eula https://go.microsoft.com/fwlink/?LinkId=2002534 에서 볼 수 있습니다.
#### `--node-label -l`
배포할 노드를 지정 하는 데 사용 되는 빅 데이터 클러스터 노드 레이블입니다.
#### `--force -f`
강제로 만들려면 사용자에 게 값을 입력 하 라는 메시지가 표시 되지 않으며 모든 문제가 stderr의 일부로 인쇄 됩니다.
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
## <a name="azdata-bdc-delete"></a>azdata bdc 삭제
Kube config는 다음 환경 변수 [' CONTROLLER_USERNAME ', ' CONTROLLER_PASSWORD ']와 함께 시스템에서 SQL Server 빅 데이터 클러스터를 삭제 해야 합니다.
```bash
azdata bdc delete --name -n 
                  [--force -f]
```
### <a name="examples"></a>예
시스템 환경에 컨트롤러 사용자 이름 및 암호가 이미 설정 된 BDC를 삭제 합니다.
```bash
azdata bdc delete --name <cluster_name>
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
Kubernetes 네임 스페이스에 사용 되는 빅 데이터 클러스터 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--force -f`
빅 데이터 클러스터를 강제로 삭제 합니다.
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

다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md)를 참조 하세요. **Azdata** 도구를 설치 하는 방법에 대 한 자세한 내용은 [install azdata to manage SQL Server 2019 빅 data 클러스터](deploy-install-azdata.md)를 참조 하세요.
