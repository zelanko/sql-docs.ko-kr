---
title: azdata arc dc 참조
titleSuffix: SQL Server big data clusters
description: azdata arc dc 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6f4f9c414221bc6eab400416d6ea09e692031aa5
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358781"
---
# <a name="azdata-arc-dc"></a>azdata arc dc

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]에 적용됩니다.

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|명령|설명|
| --- | --- |
[azdata arc dc create](#azdata-arc-dc-create) | 데이터 컨트롤러를 만듭니다.
[azdata arc dc delete](#azdata-arc-dc-delete) | 데이터 컨트롤러를 삭제합니다.
[azdata arc dc endpoint](reference-azdata-arc-dc-endpoint.md) | 엔드포인트 명령입니다.
[azdata arc dc status](reference-azdata-arc-dc-status.md) | 상태 명령입니다.
[azdata arc dc config](reference-azdata-arc-dc-config.md) | 구성 명령입니다.
[azdata arc dc debug](reference-azdata-arc-dc-debug.md) | 디버그 명령입니다.
[azdata arc dc export](#azdata-arc-dc-export) | 메트릭, 로그 또는 사용량을 내보냅니다.
[azdata arc dc upload](#azdata-arc-dc-upload) | 내보낸 데이터 파일을 업로드합니다.
## <a name="azdata-arc-dc-create"></a>azdata arc dc create
데이터 컨트롤러를 만듭니다. 시스템에 kube 구성과 [‘AZDATA_USERNAME’, ‘AZDATA_PASSWORD’] 환경 변수가 있어야 합니다.
```bash
azdata arc dc create --namespace -ns 
                     --name -n  
                     
--connectivity-mode  
                     
--resource-group -g  
                     
--location -l  
                     
--subscription -s  
                     
[--profile-name]  
                     
[--path -p]  
                     
[--storage-class -sc]
```
### <a name="examples"></a>예
데이터 컨트롤러 배포입니다.
```bash
azdata arc dc create
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--namespace -ns`
데이터 컨트롤러를 배포할 Kubernetes 네임스페이스입니다. 이미 있으면 해당 네임스페이스가 사용됩니다. 네임스페이스가 없으면 먼저 만들려고 시도합니다.
#### `--name -n`
데이터 컨트롤러의 이름입니다.
#### `--connectivity-mode`
데이터 컨트롤러를 실행할 Azure 연결(간접 또는 직접)입니다.
#### `--resource-group -g`
데이터 컨트롤러 리소스를 추가할 Azure 리소스 그룹입니다.
#### `--location -l`
데이터 컨트롤러 메타데이터를 저장할 Azure 위치(예: eastus)입니다.
#### `--subscription -s`
데이터 컨트롤러 리소스를 추가할 Azure 구독 ID입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--profile-name`
기존 구성 프로필의 이름입니다. `azdata arc dc config list`를 실행하여 사용 가능한 옵션을 확인합니다. [‘azure-arc-aks-premium-storage’, ‘azure-arc-ake’, ‘azure-arc-openshift’, ‘azure-arc-gke’, ‘azure-arc-aks-default-storage’, ‘azure-arc-kubeadm’, ‘azure-arc-eks’, ‘azure-arc-azure-openshift’, ‘azure-arc-aks-hci’] 중 하나입니다.
#### `--path -p`
사용할 사용자 지정 구성 프로필이 포함된 디렉터리의 경로입니다. `azdata arc dc config init`를 실행하여 사용자 지정 구성 프로필을 만듭니다.
#### `--storage-class -sc`
볼륨이 필요한 모든 데이터 컨트롤러 Pod의 모든 영구적 데이터 및 로그 볼륨에 사용할 스토리지 클래스입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-arc-dc-delete"></a>azdata arc dc delete
데이터 컨트롤러를 삭제합니다. 시스템에 kube 구성이 있어야 합니다.
```bash
azdata arc dc delete --name -n 
                     --namespace -ns  
                     
[--force -f]
```
### <a name="examples"></a>예
데이터 컨트롤러 배포입니다.
```bash
azdata arc dc delete
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
데이터 컨트롤러 이름입니다.
#### `--namespace -ns`
데이터 컨트롤러가 있는 Kubernetes 네임스페이스입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--force -f`
데이터 컨트롤러를 강제로 삭제합니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-arc-dc-export"></a>azdata arc dc export
메트릭, 로그 또는 사용량을 파일로 내보냅니다.
```bash
azdata arc dc export --type -t 
                     --path -p  
                     
[--force -f]
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--type -t`
내보낼 데이터 형식입니다. 옵션: logs, metrics, usage.
#### `--path -p`
내보낼 파일의 파일 이름을 포함하는 전체 경로 또는 상대 경로입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--force -f`
출력 파일을 강제로 만듭니다. 같은 경로에 있는 기존 파일을 덮어씁니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-arc-dc-upload"></a>azdata arc dc upload
데이터 컨트롤러에서 내보낸 데이터 파일을 Azure로 업로드합니다.
```bash
azdata arc dc upload --path -p 
                     
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
업로드할 파일의 파일 이름을 포함하는 전체 경로 또는 상대 경로입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.

## <a name="next-steps"></a>다음 단계

다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요. 

**azdata** 도구를 설치하는 방법에 대한 자세한 내용은 [azdata 설치](..\install\deploy-install-azdata.md)를 참조하세요.

