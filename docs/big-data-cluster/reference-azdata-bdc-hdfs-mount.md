---
title: azdata bdc hdfs mount 참조
titleSuffix: SQL Server big data clusters
description: azdata bdc hdfs mount 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7f0b259a3ac4ac0850fa05de3867e928b035307b
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68426273"
---
# <a name="azdata-bdc-hdfs-mount"></a>azdata bdc hdfs mount

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **azdata** 도구의 **bdc hdfs mount** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc hdfs mount create](#azdata-bdc-hdfs-mount-create) | HDFS에 원격 저장소의 탑재를 만듭니다.
[azdata bdc hdfs mount delete](#azdata-bdc-hdfs-mount-delete) | HDFS에서 원격 저장소의 탑재를 삭제합니다.
[azdata bdc hdfs mount status](#azdata-bdc-hdfs-mount-status) | 탑재의 상태입니다.
[azdata bdc hdfs mount refresh](#azdata-bdc-hdfs-mount-refresh) | HDFS에서 탑재의 콘텐츠를 새로 고칩니다.
## <a name="azdata-bdc-hdfs-mount-create"></a>azdata bdc hdfs mount create
HDFS에 원격 저장소의 탑재를 만듭니다. 원격 저장소에 액세스하기 위한 자격 증명(있는 경우)은 MOUNT_CREDENTIALS 환경 변수를 쉼표로 구분된 키=값 쌍 목록으로 사용하여 지정해야 합니다. 키 또는 값의 모든 쉼표는 이스케이프해야 합니다.
```bash
azdata bdc hdfs mount create --remote-uri -r 
                             --mount-path -m
```
### <a name="examples"></a>예
공유 키를 사용하여 HDFS 경로 /mounts/adlsv2/data의 ADLS Gen 2 계정 "adlsv2example"에 컨테이너 "data"를 탑재하려면 다음을 실행합니다.
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
azdata bdc hdfs mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
로컬 HDFS 경로 /mounts/hdfs/에 원격 HDFS BDC(hdfs://namenode1:8080/)를 탑재하려면 다음을 실행합니다.
```bash
azdata bdc hdfs mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--remote-uri -r`
탑재할 원격 저장소의 URI입니다(탑재 원본).
#### `--mount-path -m`
탑재를 만들 HDFS 경로입니다(탑재 대상).
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-mount-delete"></a>azdata bdc hdfs mount delete
HDFS에서 원격 저장소의 탑재를 삭제합니다.
```bash
azdata bdc hdfs mount delete --mount-path -m 
                             
```
### <a name="examples"></a>예
ADLS Gen 2 스토리지 계정의 /mounts/adlsv2/data에서 만든 탑재를 삭제합니다.
```bash
azdata bdc hdfs mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--mount-path -m`
삭제해야 하는 탑재에 해당하는 HDFS 경로입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-mount-status"></a>azdata bdc hdfs mount status
탑재의 상태입니다.
```bash
azdata bdc hdfs mount status [--mount-path -m] 
                             
```
### <a name="examples"></a>예
경로별 탑재 상태를 가져옵니다.
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
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-mount-refresh"></a>azdata bdc hdfs mount refresh
HDFS에서 탑재의 콘텐츠를 새로 고칩니다.
```bash
azdata bdc hdfs mount refresh --mount-path -m 
                              
```
### <a name="examples"></a>예
/Mounts/adlsv2/data에서 만든 탑재를 새로 고칩니다.
```bash
azdata bdc hdfs mount refresh --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--mount-path -m`
새로 고쳐야 하는 탑재에 해당하는 HDFS 경로입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.

## <a name="next-steps"></a>다음 단계

다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요. **azdata** 도구를 설치하는 방법에 대한 자세한 내용은 [azdata를 설치하여 SQL Server 2019 빅 데이터 클러스터 관리](deploy-install-azdata.md)를 참조하세요.
