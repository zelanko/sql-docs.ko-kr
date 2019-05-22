---
title: mssqlctl 클러스터 저장소 풀 마운트 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 클러스터 저장소 풀 마운트 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c527a203b9a8a902f02368c291a37da4c38ccd31
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65995031"
---
# <a name="mssqlctl-cluster-storage-pool-mount"></a>mssqlctl 클러스터 저장소 풀 마운트

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **클러스터 저장소 풀 마운트** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[클러스터 저장소 풀 마운트 mssqlctl 만들기](#mssqlctl-cluster-storage-pool-mount-create) | HDFS에서 원격 저장소의 탑재를 만듭니다.
[mssqlctl 클러스터 저장소 풀 마운트 삭제](#mssqlctl-cluster-storage-pool-mount-delete) | HDFS의 원격 저장소의 탑재를 삭제 합니다.
[mssqlctl 클러스터 저장소 풀 마운트 상태](#mssqlctl-cluster-storage-pool-mount-status) | Mount(s)의 상태입니다.
## <a name="mssqlctl-cluster-storage-pool-mount-create"></a>클러스터 저장소 풀 마운트 mssqlctl 만들기
HDFS에서 원격 저장소의 탑재를 만듭니다.
```bash
mssqlctl cluster storage-pool mount create --remote-uri 
                                           --mount-path  
                                           [--credential-file]
```
### <a name="examples"></a>예
공유 키를 사용 하 여 HDFS 경로 /mounts/adlsv2/data에서 Gen 2 ADLS 계정의 "adlsv2example" 컨테이너 "데이터"를 탑재 하려면
```bash
mssqlctl cluster storage-pool mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data --credentials credential_file
```
원격 HDFS 클러스터 탑재 (hdfs://namenode1:8080 /)에서 로컬 HDFS 경로 /mounts hdfs /
```bash
mssqlctl cluster storage-pool mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--remote-uri`
탑재 된 (탑재의 원본)에 있는 원격 저장소의 URI입니다.
#### `--mount-path`
탑재 (탑재 대상)을 만들 수 있는 한 HDFS 경로입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--credential-file`
원격 저장소에 액세스 하는 자격 증명을 포함 하는 파일입니다. 자격 증명 키로 지정할 필요가 = 값 쌍 하나의 키를 사용 하 여 = 줄 값입니다. 키 또는 값에서 모든 equals를 이스케이프 해야 합니다. 기본적으로 자격 증명이 필요 합니다. 필요한 키를 탑재 하는 원격 저장소의 유형 및 사용 권한 부여의 형식에 따라 달라 집니다.
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
## <a name="mssqlctl-cluster-storage-pool-mount-delete"></a>mssqlctl 클러스터 저장소 풀 마운트 삭제
HDFS의 원격 저장소의 탑재를 삭제 합니다.
```bash
mssqlctl cluster storage-pool mount delete --mount-path 
                                           
```
### <a name="examples"></a>예
Gen 2 ADLS 저장소 계정에 대 한 /mounts/adlsv2/data에서 생성 하는 탑재를 삭제 합니다.
```bash
mssqlctl cluster storage-pool mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--mount-path`
삭제 된 해당 탑재 하는 HDFS 경로입니다.
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
## <a name="mssqlctl-cluster-storage-pool-mount-status"></a>mssqlctl 클러스터 저장소 풀 마운트 상태
Mount(s)의 상태입니다.
```bash
mssqlctl cluster storage-pool mount status [--mount-path] 
                                           
```
### <a name="examples"></a>예
경로로 탑재 상태 가져오기
```bash
mssqlctl cluster storage-pool mount status --mount-path /mounts/hdfs
```
모든 탑재의 상태를 가져옵니다.
```bash
mssqlctl cluster storage-pool mount status
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--mount-path`
탑재 경로입니다.
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