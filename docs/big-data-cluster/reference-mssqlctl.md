---
title: mssqlctl 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ebd3b63d641c77dae1afbff21264ec4fe34df4d0
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64775498"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **mssqlctl** 에 대 한 도구 [SQL Server 2019 빅 데이터 클러스터 (미리 보기)](big-data-cluster-overview.md)합니다. 설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
|[mssqlctl 앱](reference-mssqlctl-app.md) | 만들기, 삭제, 실행 및 응용 프로그램을 관리 합니다. |
|[mssqlctl cluster](reference-mssqlctl-cluster.md) | 선택 하 고, 관리 및 클러스터 작동 합니다. |
[mssqlctl login](#mssqlctl-login) | 클러스터에 로그인 합니다.
[mssqlctl logout](#mssqlctl-logout) | 로그 아웃 클러스터 합니다.
|[mssqlctl storage](reference-mssqlctl-storage.md) | 클러스터 저장소를 관리 합니다. |
## <a name="mssqlctl-login"></a>mssqlctl 로그인
클러스터에 로그인 합니다.
```bash
mssqlctl login [--username -u] 
               [--password -p]  
               [--endpoint -e]
```
### <a name="examples"></a>예
대화형으로 로그인 합니다.
```bash
mssqlctl login
```
사용자 이름 및 암호로 로그인 합니다.
```bash
mssqlctl login -u johndoe@contoso.com -p VerySecret
```
사용자 이름, 암호 및 클러스터 끝점으로 로그인 합니다.
```bash
mssqlctl login -u johndoe@contoso.com -p VerySecret --endpoint https://host.com:12800
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--username -u`
사용자 계정입니다.
#### `--password -p`
암호 자격 증명입니다.
#### `--endpoint -e`
클러스터 호스트 및 포트 (예:) "http://host:port"입니다.
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
## <a name="mssqlctl-logout"></a>mssqlctl 로그 아웃
로그 아웃 클러스터 합니다.
```bash
mssqlctl logout 
```
### <a name="examples"></a>예
이 사용자를 로그 아웃이 있습니다.
```bash
mssqlctl logout
```
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

설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.