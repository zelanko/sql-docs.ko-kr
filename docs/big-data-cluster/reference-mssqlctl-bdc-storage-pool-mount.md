---
title: mssqlctl bdc 저장소 풀 마운트 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl bdc 저장소 풀 마운트 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b6a412c6d7cab9fb869a9aa8ee1b62ae0ed3f717
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958008"
---
# <a name="mssqlctl-bdc-storage-pool-mount"></a>mssqlctl bdc 저장소 풀 마운트

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **bdc 저장소 풀 마운트** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl bdc 저장소 풀 마운트 만들기](#mssqlctl-bdc-storage-pool-mount-create) | HDFS에서 원격 저장소의 탑재를 만듭니다.
[mssqlctl bdc 저장소 풀 마운트 삭제](#mssqlctl-bdc-storage-pool-mount-delete) | HDFS의 원격 저장소의 탑재를 삭제 합니다.
[mssqlctl bdc 저장소 풀 마운트 상태](#mssqlctl-bdc-storage-pool-mount-status) | Mount(s)의 상태입니다.
## <a name="mssqlctl-bdc-storage-pool-mount-create"></a>mssqlctl bdc 저장소 풀 마운트 만들기
HDFS에서 원격 저장소의 탑재를 만듭니다. 있는 경우, 원격 저장소에 액세스 하기 위한 자격 증명을 지정 해야 하는 환경 변수의 MOUNT_CREDENTIALS 키의 쉼표로 구분 된 목록으로 = 값 쌍입니다. 키와 값의 모든 쉼표를 이스케이프 되어야 합니다.
```bash
mssqlctl bdc storage-pool mount create --remote-uri 
                                       --mount-path
```
### <a name="examples"></a>예
공유 키를 사용 하 여 HDFS 경로 /mounts/adlsv2/data에서 Gen 2 ADLS 계정의 "adlsv2example" 컨테이너 "데이터"를 탑재 하려면
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
mssqlctl bdc storage-pool mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
탑재할 원격 HDFS BDC (hdfs://namenode1:8080 /)에서 로컬 HDFS 경로 /mounts hdfs /
```bash
mssqlctl bdc storage-pool mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--remote-uri`
탑재 된 (탑재의 원본)에 있는 원격 저장소의 URI입니다.
#### `--mount-path`
탑재 (탑재 대상)을 만들 수 있는 한 HDFS 경로입니다.
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
## <a name="mssqlctl-bdc-storage-pool-mount-delete"></a>mssqlctl bdc 저장소 풀 마운트 삭제
HDFS의 원격 저장소의 탑재를 삭제 합니다.
```bash
mssqlctl bdc storage-pool mount delete --mount-path 
                                       
```
### <a name="examples"></a>예
Gen 2 ADLS 저장소 계정에 대 한 /mounts/adlsv2/data에서 생성 하는 탑재를 삭제 합니다.
```bash
mssqlctl bdc storage-pool mount delete --mount-path /mounts/adlsv2/data
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
## <a name="mssqlctl-bdc-storage-pool-mount-status"></a>mssqlctl bdc 저장소 풀 마운트 상태
Mount(s)의 상태입니다.
```bash
mssqlctl bdc storage-pool mount status [--mount-path] 
                                       
```
### <a name="examples"></a>예
경로로 탑재 상태 가져오기
```bash
mssqlctl bdc storage-pool mount status --mount-path /mounts/hdfs
```
모든 탑재의 상태를 가져옵니다.
```bash
mssqlctl bdc storage-pool mount status
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