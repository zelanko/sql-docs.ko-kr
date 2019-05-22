---
title: mssqlctl 클러스터 구성 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 클러스터 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 984a3c50ac691df3759edc161baabc533bd9456f
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993339"
---
# <a name="mssqlctl-cluster-config"></a>mssqlctl 클러스터 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **클러스터 구성** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl cluster config show](#mssqlctl-cluster-config-show) | SQL Server 빅 데이터 클러스터의 현재 구성을 가져옵니다.
[클러스터 구성 init mssqlctl](#mssqlctl-cluster-config-init) | 초기화 클러스터와 함께 사용할 수 있는 클러스터 구성 프로필을 만듭니다.
[mssqlctl cluster config list](#mssqlctl-cluster-config-list) | 사용 가능한 구성 파일 선택 항목을 나열합니다.
[mssqlctl 클러스터 구성 섹션](reference-mssqlctl-cluster-config-section.md) | 클러스터 구성 파일의 개별 섹션을 사용 하 여 작업에 대 한 명령입니다.
## <a name="mssqlctl-cluster-config-show"></a>mssqlctl 클러스터 config show
SQL Server 빅 데이터 클러스터의 현재 구성 파일 및 대상 파일에 출력 또는 매우 콘솔에 출력 합니다.
```bash
mssqlctl cluster config show [--target -t] 
                             [--force -f]
```
### <a name="examples"></a>예
콘솔에서 클러스터 구성 표시
```bash
mssqlctl cluster config show
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--target -t`
출력 파일에 결과 저장할입니다. 기본값: stdout으로 전송 합니다.
#### `--force -f`
대상 파일의 덮어쓰기를 강제 합니다.
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
## <a name="mssqlctl-cluster-config-init"></a>클러스터 구성 init mssqlctl
초기화 클러스터와 함께 사용할 수 있는 클러스터 구성 프로필을 만듭니다. 구성 프로필의 특정 원본 3 선택 항목 중에서 인수에 지정할 수 있습니다.
```bash
mssqlctl cluster config init [--target -t] 
                             [--src -s]  
                             [--force -f]
```
### <a name="examples"></a>예
클러스터 구성 init 환경-단계별 필요한 값에 대 한 프롬프트가 나타납니다.
```bash
mssqlctl cluster config init
```
인수를 사용 하 여 구성 init 클러스터, aks-개발-테스트의 구성 프로필을 만듭니다. / custom.json 합니다.
```bash
mssqlctl cluster config init --src aks-dev-test.json --target custom.json
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--target -t`
사용자 지정 config.json을 사용 하 여 cwd 기본값으로 배치 구성 프로필 하려는의 파일 경로입니다.
#### `--src -s`
구성 프로필 소스: ['aks-dev-test.json', ' kubeadm-개발자-test.json', ' minikube-dev-test.json']
#### `--force -f`
대상 파일의 덮어쓰기를 강제 합니다.
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
## <a name="mssqlctl-cluster-config-list"></a>mssqlctl 클러스터 구성 목록
클러스터 구성 초기화에 사용할 사용 가능한 구성 파일 선택 항목을 나열합니다.
```bash
mssqlctl cluster config list [--config-file -c] 
                             
```
### <a name="examples"></a>예
모든 사용 가능한 구성 프로필 이름을 표시합니다.
```bash
mssqlctl cluster config list
```
특정 구성 프로필의 json을 보여 줍니다.
```bash
mssqlctl cluster config list --config-file aks-dev-test.json
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--config-file -c`
기본 구성 파일: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-dev-test.json']
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