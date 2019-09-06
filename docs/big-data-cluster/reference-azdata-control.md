---
title: azdata 컨트롤 참조
titleSuffix: SQL Server big data clusters
description: Azdata 제어 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2ce02ef0b212070b4a52944e055404137c78c98b
ms.sourcegitcommit: 0c6c1555543daff23da9c395865dafd5bb996948
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70304729"
---
# <a name="azdata-control"></a>azdata 컨트롤

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

이 문서는 **azdata**에 대 한 참조 문서입니다. 

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata 컨트롤 만들기](#azdata-control-create) | 컨트롤 평면을 만듭니다.
[azdata 컨트롤 삭제](#azdata-control-delete) | 컨트롤 평면을 삭제 합니다.
## <a name="azdata-control-create"></a>azdata 컨트롤 만들기
다음 환경 변수 [' CONTROLLER_USERNAME ', ' CONTROLLER_PASSWORD ', ' MSSQL_SA_PASSWORD ', ' KNOX_PASSWORD ']와 함께 시스템에 kube config를 만듭니다.
```bash
azdata control create [--name -n] 
                      [--config-profile -c]  
                      [--accept-eula -a]  
                      [--node-label -l]  
                      [--force -f]
```
### <a name="examples"></a>예
제어 배포.
```bash
azdata control create
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--name -n`
Kubernetes 네임 스페이스에 사용 되는 제어 평면 이름입니다.
#### `--config-profile -c`
클러스터를 배포 하는 데 사용 되는 클러스터 구성 프로필: [' aks ', ' kubeadm ', ' minikube ', ' kubeadm ']
#### `--accept-eula -a`
사용 조건에 동의하시겠습니까? [예/아니요]. 이 인수를 사용하지 않으려면 ACCEPT_EULA 환경 변수를 ‘yes’로 설정하면 됩니다. 
#### `--node-label -l`
노드 레이블-배포할 노드를 지정 하는 데 사용 됩니다.
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
## <a name="azdata-control-delete"></a>azdata 컨트롤 삭제
시스템에 kube config를 삭제 해야 합니다.
```bash
azdata control delete --name -n 
                      [--force -f]
```
### <a name="examples"></a>예
제어 배포.
```bash
azdata control delete
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
Kubernetes 네임 스페이스에 사용 되는 제어 평면 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--force -f`
제어 평면을 강제로 삭제 합니다.
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

- 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요. 

- **azdata** 도구를 설치하는 방법에 대한 자세한 내용은 [azdata를 설치하여 SQL Server 2019 빅 데이터 클러스터 관리](deploy-install-azdata.md)를 참조하세요.
