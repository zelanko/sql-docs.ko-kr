---
title: mssqlctl 클러스터 구성 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 클러스터 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3a4693c5ffb68ad555d97d02f983fadf4e6bbd9a
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473300"
---
# <a name="mssqlctl-cluster-config"></a>mssqlctl 클러스터 구성

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **클러스터 구성** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl cluster config get](#mssqlctl-cluster-config-get) | 클러스터 구성-kube 가져오기 구성 시스템에 필요 합니다.
[클러스터 구성 init mssqlctl](#mssqlctl-cluster-config-init) | 클러스터 구성을 초기화합니다.
[mssqlctl cluster config list](#mssqlctl-cluster-config-list) | 사용 가능한 구성 파일 선택 항목을 나열합니다.
[mssqlctl 클러스터 구성 섹션](reference-mssqlctl-cluster-config-section.md) | 구성 파일의 개별 섹션을 사용 하 여 작업에 대 한 명령입니다.
## <a name="mssqlctl-cluster-config-get"></a>mssqlctl 클러스터 구성 가져오기
SQL Server 빅 데이터 클러스터의 현재 구성 파일을 가져옵니다.
```bash
mssqlctl cluster config get --name -n 
                            [--output-file -f]
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
Kubernetes 네임 스페이스에 대해 사용 되는 클러스터 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--output-file -f`
출력 파일에 결과 저장할입니다. 기본값: stdout으로 전송 합니다.
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
지정 된 기본 형식에 따라 사용자에 대 한 클러스터 구성 파일을 초기화 합니다.
```bash
mssqlctl cluster config init [--target -t] 
                             [--src -s]
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--target -t`
저장할 사용자 지정 config.json을 사용 하 여 cwd 기본값으로 배치 구성 파일의 파일 경로입니다.
#### `--src -s`
구성 원본: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-개발-test.json']
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
mssqlctl cluster config list [--config-file -f] 
                             
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--config-file -f`
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