---
title: mssqlctl 클러스터 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 클러스터 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c69aeced2378e018376172e1fb6370d56706ecb7
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473329"
---
# <a name="mssqlctl-cluster"></a>mssqlctl 클러스터

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **클러스터** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl 클러스터 만들기](#mssqlctl-cluster-create) | 클러스터를 만듭니다.
[mssqlctl 클러스터 삭제](#mssqlctl-cluster-delete) | 클러스터를 삭제 합니다.
[mssqlctl cluster config](reference-mssqlctl-cluster-config.md) | 클러스터 구성 명령입니다.
[mssqlctl 클러스터 디버그](reference-mssqlctl-cluster-debug.md) | 명령을 디버그 합니다.
## <a name="mssqlctl-cluster-create"></a>mssqlctl 클러스터 만들기
SQL Server 빅 데이터 클러스터를 만듭니다.
```bash
mssqlctl cluster create [--config-file -f] 
                        [--accept-eula -e]  
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--config-file -f`
구성 프로필, 클러스터를 배포 하는 데 클러스터: ['aks-dev-test.json', ' kubeadm-dev-test.json', ' minikube-개발-test.json']
#### `--accept-eula -e`
사용 약관 수락 하 시겠습니까? [yes/no].
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
## <a name="mssqlctl-cluster-delete"></a>mssqlctl 클러스터 삭제
SQL Server 빅 데이터 클러스터를 삭제 합니다.
```bash
mssqlctl cluster delete --name -n 
                        [--force -f]
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
Kubernetes 네임 스페이스에 대해 사용 되는 클러스터 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--force -f`
강제 삭제 클러스터입니다.
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
