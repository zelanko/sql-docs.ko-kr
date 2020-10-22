---
title: azdata arc postgres server backup 참조
titleSuffix: SQL Server big data clusters
description: azdata arc postgres server backup 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 44a3811ab3412a7631a0a0bf95aecc85150206b0
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358751"
---
# <a name="azdata-arc-postgres-server-backup"></a>azdata arc postgres server backup

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]에 적용됩니다.

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|명령|설명|
| --- | --- |
[azdata arc postgres server backup create](#azdata-arc-postgres-server-backup-create) | PostgreSQL 서버 그룹의 백업을 만듭니다.
[azdata arc postgres server backup delete](#azdata-arc-postgres-server-backup-delete) | PostgreSQL 서버 그룹의 백업을 삭제합니다.
[azdata arc postgres server backup restore](#azdata-arc-postgres-server-backup-restore) | PostgreSQL 서버 그룹의 백업을 복원합니다.
[azdata arc postgres server backup restorestatus](#azdata-arc-postgres-server-backup-restorestatus) | 가장 최근의 복원 작업 상태를 가져옵니다(있는 경우).
[azdata arc postgres server backup show](#azdata-arc-postgres-server-backup-show) | PostgreSQL 서버 그룹의 백업에 대한 세부 정보를 표시합니다.
## <a name="azdata-arc-postgres-server-backup-create"></a>azdata arc postgres server backup create
PostgreSQL 서버 그룹의 백업을 만듭니다.
```bash
azdata arc postgres server backup create 
```
### <a name="examples"></a>예
‘pg’ 서비스의 백업을 만듭니다.
```bash
azdata arc postgres server backup create -sn pg
```
‘pg’ 서비스의 명명된 백업을 만듭니다.
```bash
azdata arc postgres server backup create -sn pg -n backup1
```
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
## <a name="azdata-arc-postgres-server-backup-delete"></a>azdata arc postgres server backup delete
PostgreSQL 서버 그룹의 백업을 삭제합니다.
```bash
azdata arc postgres server backup delete 
```
### <a name="examples"></a>예
PostgreSQL 서버 그룹의 백업을 삭제합니다.
```bash
azdata arc postgres backup delete -sn pg -id e07dd3940e374bd9acbc86869cbc123d
```
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
## <a name="azdata-arc-postgres-server-backup-restore"></a>azdata arc postgres server backup restore
PostgreSQL 서버 그룹의 백업을 복원합니다.
```bash
azdata arc postgres server backup restore 
```
### <a name="examples"></a>예
가장 최근의 백업을 복원합니다.
```bash
azdata arc postgres server restore -sn pg```
Restore a backup by ID
```bash
azdata arc postgres server restore -sn pg -id 123e4567e89b12d3a456426655440000
```
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
## <a name="azdata-arc-postgres-server-backup-restorestatus"></a>azdata arc postgres server backup restorestatus
가장 최근의 복원 작업 상태를 가져옵니다(있는 경우).
```bash
azdata arc postgres server backup restorestatus 
```
### <a name="examples"></a>예
‘pg’ 서비스의 최근 복원 상태를 ID로 가져옵니다.
```bash
azdata arc postgres server backup restorestatus -sn pg -id 123e4567e89b12d3a456426655440000
```
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
## <a name="azdata-arc-postgres-server-backup-show"></a>azdata arc postgres server backup show
PostgreSQL 서버 그룹의 백업에 대한 세부 정보를 표시합니다.
```bash
azdata arc postgres server backup show 
```
### <a name="examples"></a>예
‘pg’ 서비스의 백업을 ID로 가져옵니다.
```bash
azdata arc postgres server backup show -sn pg -id 123e4567e89b12d3a456426655440000
```
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

