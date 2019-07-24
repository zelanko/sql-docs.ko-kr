---
title: azdata bdc hdfs 탑재 참조
titleSuffix: SQL Server big data clusters
description: Azdata bdc hdfs 탑재 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7f0b259a3ac4ac0850fa05de3867e928b035307b
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426273"
---
# <a name="azdata-bdc-hdfs-mount"></a>azdata bdc hdfs 탑재

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **azdata** 도구의 **bdc hdfs 탑재** 명령에 대 한 참조를 제공 합니다. 다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md)를 참조 하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc hdfs 탑재 만들기](#azdata-bdc-hdfs-mount-create) | HDFS에 원격 저장소의 탑재를 만듭니다.
[azdata bdc hdfs 탑재 삭제](#azdata-bdc-hdfs-mount-delete) | HDFS에서 원격 저장소의 탑재를 삭제 합니다.
[azdata bdc hdfs 탑재 상태](#azdata-bdc-hdfs-mount-status) | 탑재의 상태입니다.
[azdata bdc hdfs 탑재 새로 고침](#azdata-bdc-hdfs-mount-refresh) | HDFS에서 탑재의 콘텐츠를 새로 고칩니다.
## <a name="azdata-bdc-hdfs-mount-create"></a>azdata bdc hdfs 탑재 만들기
HDFS에 원격 저장소의 탑재를 만듭니다. 원격 저장소에 액세스 하기 위한 자격 증명 (있는 경우)은 MOUNT_CREDENTIALS 환경 변수를 키 = 값 쌍의 쉼표로 구분 된 목록으로 사용 하 여 지정 해야 합니다. 키 또는 값의 모든 쉼표는 이스케이프 되어야 합니다.
```bash
azdata bdc hdfs mount create --remote-uri -r 
                             --mount-path -m
```
### <a name="examples"></a>예
공유 키를 사용 하 여 HDFS 경로/mounts/adlsv2/data의 ADLS Gen 2 계정 "adlsv2example"에 컨테이너 "data"를 탑재 하려면
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
azdata bdc hdfs mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
로컬 HDFS 경로/mounts/hdfs/에 원격 HDFS BDC (hdfs://namenode1:8080/)를 탑재 하려면
```bash
azdata bdc hdfs mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--remote-uri -r`
탑재 된 원격 저장소의 URI (탑재 원본)입니다.
#### `--mount-path -m`
탑재를 만들어야 하는 HDFS 경로 (탑재 대상).
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
## <a name="azdata-bdc-hdfs-mount-delete"></a>azdata bdc hdfs 탑재 삭제
HDFS에서 원격 저장소의 탑재를 삭제 합니다.
```bash
azdata bdc hdfs mount delete --mount-path -m 
                             
```
### <a name="examples"></a>예
ADLS Gen 2 저장소 계정에 대 한/mounts/adlsv2/data에서 만든 탑재를 삭제 합니다.
```bash
azdata bdc hdfs mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--mount-path -m`
삭제 해야 하는 탑재에 해당 하는 HDFS 경로입니다.
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
## <a name="azdata-bdc-hdfs-mount-status"></a>azdata bdc hdfs 탑재 상태
탑재의 상태입니다.
```bash
azdata bdc hdfs mount status [--mount-path -m] 
                             
```
### <a name="examples"></a>예
경로를 기준으로 탑재 상태 가져오기
```bash
azdata bdc hdfs mount status --mount-path /mounts/hdfs
```
모든 탑재의 상태를 가져옵니다.
```bash
azdata bdc hdfs mount status
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--mount-path -m`
탑재 경로입니다.
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
## <a name="azdata-bdc-hdfs-mount-refresh"></a>azdata bdc hdfs 탑재 새로 고침
HDFS에서 탑재의 콘텐츠를 새로 고칩니다.
```bash
azdata bdc hdfs mount refresh --mount-path -m 
                              
```
### <a name="examples"></a>예
/Mounts/adlsv2/data.에서 새로 고침 탑재 생성
```bash
azdata bdc hdfs mount refresh --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--mount-path -m`
새로 고쳐야 하는 탑재에 해당 하는 HDFS 경로입니다.
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
