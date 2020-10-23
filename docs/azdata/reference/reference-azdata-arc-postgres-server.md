---
title: azdata arc postgres server 참조
titleSuffix: SQL Server big data clusters
description: azdata arc postgres server 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0a28ba44dfbeb2b0ef1b5191e6e3bfba5352d540
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358731"
---
# <a name="azdata-arc-postgres-server"></a>azdata arc postgres server

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]에 적용됩니다.

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|명령|설명|
| --- | --- |
[azdata arc postgres server create](#azdata-arc-postgres-server-create) | PostgreSQL 서버 그룹을 만듭니다.
[azdata arc postgres server edit](#azdata-arc-postgres-server-edit) | PostgreSQL 서버 그룹의 구성을 편집합니다.
[azdata arc postgres server delete](#azdata-arc-postgres-server-delete) | PostgreSQL 서버 그룹을 삭제합니다.
[azdata arc postgres server show](#azdata-arc-postgres-server-show) | PostgreSQL 서버 그룹의 세부 정보를 표시합니다.
[azdata arc postgres server list](#azdata-arc-postgres-server-list) | PostgreSQL 서버 그룹을 나열합니다.
[azdata arc postgres server config](reference-azdata-arc-postgres-server-config.md) | 구성 명령입니다.
[azdata arc postgres server backup](reference-azdata-arc-postgres-server-backup.md) | PostgreSQL 서버 그룹 백업을 관리합니다.
## <a name="azdata-arc-postgres-server-create"></a>azdata arc postgres server create
서버 그룹의 암호를 설정하려면 AZDATA_PASSWORD 환경 변수를 설정합니다.
```bash
azdata arc postgres server create --name -n 
                                  [--path]  
                                  
[--cores-limit -cl]  
                                  
[--cores-request -cr]  
                                  
[--memory-limit -ml]  
                                  
[--memory-request -mr]  
                                  
[--storage-class-data -scd]  
                                  
[--storage-class-logs -scl]  
                                  
[--storage-class-backups -scb]  
                                  
[--extensions]  
                                  
[--volume-size-data -vsd]  
                                  
[--volume-size-logs -vsl]  
                                  
[--volume-size-backups -vsb]  
                                  
[--workers -w]  
                                  
[--engine-version -ev]  
                                  
[--no-external-endpoint]  
                                  
[--dev]  
                                  
[--port]  
                                  
[--no-wait]  
                                  
[--engine-settings -e]
```
### <a name="examples"></a>예
PostgreSQL 서버 그룹을 만듭니다.
```bash
azdata arc postgres server create -n pg1
```
엔진 설정을 사용하여 PostgreSQL 서버 그룹을 만듭니다. 아래 두 예제는 모두 유효합니다.
```bash
azdata arc postgres server create -n pg1 --engine-settings "key1=val1"
azdata arc postgres server create -n pg1 --engine-settings "key2=val2"
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
인스턴스 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--path`
PostgreSQL 서버 그룹의 원본 json 파일 경로입니다. 선택 사항입니다.
#### `--cores-limit -cl`
노드당 사용할 수 있는 postgres 인스턴스의 최대 CPU 코어 수입니다. 부분 코어가 지원됩니다.
#### `--cores-request -cr`
서비스를 예약하기 위해 노드당 사용할 수 있어야 하는 최소 CPU 코어 수입니다. 부분 코어가 지원됩니다.
#### `--memory-limit -ml`
postgres 인스턴스의 메모리 한도로, 숫자 뒤에 Ki(킬로바이트), Mi(메가바이트) 또는 Gi(기가바이트)가 옵니다.
#### `--memory-request -mr`
postgres 인스턴스의 메모리 요청으로, 숫자 뒤에 Ki(킬로바이트), Mi(메가바이트) 또는 Gi(기가바이트)가 옵니다.
#### `--storage-class-data -scd`
영구적 데이터 볼륨에 사용할 스토리지 클래스입니다.
#### `--storage-class-logs -scl`
영구적 로그 볼륨에 사용할 스토리지 클래스입니다.
#### `--storage-class-backups -scb`
영구적 백업 볼륨에 사용할 스토리지 클래스입니다.
#### `--extensions`
시작 시 로드해야 하는 Postgres 확장의 쉼표로 구분된 목록입니다. 지원되는 값은 postgres 설명서를 참조하세요.
#### `--volume-size-data -vsd`
데이터에 사용할 스토리지 볼륨 크기로, 양수 뒤에 Ki(킬로바이트), Mi(메가바이트) 또는 Gi(기가바이트)가 옵니다.
#### `--volume-size-logs -vsl`
로그에 사용할 스토리지 볼륨 크기로, 양수 뒤에 Ki(킬로바이트), Mi(메가바이트) 또는 Gi(기가바이트)가 옵니다.
#### `--volume-size-backups -vsb`
백업에 사용할 스토리지 볼륨 크기로, 양수 뒤에 Ki(킬로바이트), Mi(메가바이트) 또는 Gi(기가바이트)가 옵니다.
#### `--workers -w`
분할된 클러스터에 프로비저닝할 작업자 노드 수 또는 단일 노드 Postgres의 경우 0(기본값)입니다.
#### `--engine-version -ev`
11 또는 12여야 합니다. 기본 값은 12입니다.
#### `--no-external-endpoint`
지정하면 외부 서비스가 생성되지 않습니다. 지정하지 않으면 데이터 컨트롤러와 동일한 서비스 유형을 사용하여 외부 서비스가 생성됩니다.
#### `--dev`
이 매개 변수를 지정하면 개발 인스턴스로 간주되어 요금이 청구되지 않습니다.
#### `--port`
선택 사항입니다.
#### `--no-wait`
지정된 경우에는 인스턴스가 준비 상태로 전환될 때까지 기다리지 않고 명령이 반환됩니다.
#### `--engine-settings -e`
‘key1=val1, key2=val2’ 형식으로 구성된 Postgres 엔진 설정의 쉼표로 구분된 목록입니다.
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
## <a name="azdata-arc-postgres-server-edit"></a>azdata arc postgres server edit
PostgreSQL 서버 그룹의 구성을 편집합니다.
```bash
azdata arc postgres server edit --name -n 
                                [--path]  
                                
[--workers -w]  
                                
[--engine-version -ev]  
                                
[--cores-limit -cl]  
                                
[--cores-request -cr]  
                                
[--memory-limit -ml]  
                                
[--memory-request -mr]  
                                
[--extensions]  
                                
[--dev]  
                                
[--port]  
                                
[--no-wait]  
                                
[--engine-settings -e]  
                                
[--replace-engine-settings -re]  
                                
[--admin-password]
```
### <a name="examples"></a>예
PostgreSQL 서버 그룹의 구성을 편집합니다.
```bash
azdata arc postgres server edit --src ./spec.json -n pg1
```
엔진 설정을 사용하여 PostgreSQL 서버 그룹을 편집합니다.
```bash
azdata arc postgres server edit -n pg1 --engine-settings "key2=val2"
```
PostgreSQL 서버 그룹을 편집하고 기존 엔진 설정을 새 설정 key1=val1로 바꿉니다.
```bash
azdata arc postgres server edit -n pg1 --engine-settings "key1=val1" --replace-engine-settings
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
편집 중인 PostgreSQL 서버 그룹의 이름입니다. 인스턴스를 배포하는 데 사용되는 이름은 변경할 수 없습니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--path`
PostgreSQL 서버 그룹의 원본 json 파일 경로입니다. 선택 사항입니다.
#### `--workers -w`
분할된 클러스터에 프로비저닝할 작업자 노드 수 또는 단일 노드 Postgres의 경우 0(기본값)입니다.
#### `--engine-version -ev`
엔진 버전은 변경할 수 없습니다. 엔진 버전이 다른 두 서버 그룹의 이름이 같은 경우 --name과 함께 --engine-version을 사용하여 PostgreSQL 하이퍼스케일 서버 그룹을 식별할 수 있습니다. --engine-version은 선택 사항으로, 서버 그룹을 식별하는 데 사용할 경우 11 또는 12여야 합니다.
#### `--cores-limit -cl`
노드당 사용할 수 있는 postgres 인스턴스의 최대 CPU 코어 수입니다. 부분 코어가 지원됩니다. cores_limit를 제거하려면 해당 값을 빈 문자열로 지정합니다.
#### `--cores-request -cr`
서비스를 예약하기 위해 노드당 사용할 수 있어야 하는 최소 CPU 코어 수입니다. 부분 코어가 지원됩니다. cores_request를 제거하려면 해당 값을 빈 문자열로 지정합니다.
#### `--memory-limit -ml`
postgres 인스턴스의 메모리 한도로, 숫자 뒤에 Ki(킬로바이트), Mi(메가바이트) 또는 Gi(기가바이트)가 옵니다. memory_limit를 제거하려면 해당 값을 빈 문자열로 지정합니다.
#### `--memory-request -mr`
postgres 인스턴스의 메모리 요청으로, 숫자 뒤에 Ki(킬로바이트), Mi(메가바이트) 또는 Gi(기가바이트)가 옵니다. memory_request를 제거하려면 해당 값을 빈 문자열로 지정합니다.
#### `--extensions`
시작 시 로드해야 하는 Postgres 확장의 쉼표로 구분된 목록입니다. 지원되는 값은 postgres 설명서를 참조하세요.
#### `--dev`
이 매개 변수를 지정하면 개발 인스턴스로 간주되어 요금이 청구되지 않습니다.
#### `--port`
선택 사항입니다.
#### `--no-wait`
지정된 경우에는 인스턴스가 준비 상태로 전환될 때까지 기다리지 않고 명령이 반환됩니다.
#### `--engine-settings -e`
‘key1=val1, key2=val2’ 형식으로 구성된 Postgres 엔진 설정의 쉼표로 구분된 목록입니다. 지정한 설정이 기존 설정과 병합됩니다. 설정을 제거하려면 ‘removedKey=’와 같이 빈 값을 지정합니다. 다시 시작해야 하는 엔진 설정을 변경하면 서비스가 다시 시작되어 설정을 즉시 적용합니다.
#### `--replace-engine-settings -re`
--engine-settings로 지정하면 기존의 모든 사용자 지정 엔진 설정이 새로운 설정 및 값 세트로 바뀝니다.
#### `--admin-password`
지정된 경우 Postgres 서버의 관리자 암호는 AZDATA_PASSWORD 환경 변수(있는 경우)의 값으로 설정되거나, 해당 환경 변수가 없으면 프롬프트 값으로 설정됩니다.
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
## <a name="azdata-arc-postgres-server-delete"></a>azdata arc postgres server delete
PostgreSQL 서버 그룹을 삭제합니다.
```bash
azdata arc postgres server delete --name -n 
                                  [--engine-version -ev]
```
### <a name="examples"></a>예
PostgreSQL 서버 그룹을 삭제합니다.
```bash
azdata arc postgres server delete -n pg1
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
PostgreSQL 서버 그룹의 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--engine-version -ev`
엔진 버전이 다른 두 서버 그룹의 이름이 같은 경우 --name과 함께 --engine-version을 사용하여 PostgreSQL 하이퍼스케일 서버 그룹을 식별할 수 있습니다. --engine-version은 선택 사항으로, 서버 그룹을 식별하는 데 사용할 경우 11 또는 12여야 합니다.
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
## <a name="azdata-arc-postgres-server-show"></a>azdata arc postgres server show
PostgreSQL 서버 그룹의 세부 정보를 표시합니다.
```bash
azdata arc postgres server show --name -n 
                                [--engine-version -ev]  
                                
[--path -p]
```
### <a name="examples"></a>예
PostgreSQL 서버 그룹의 세부 정보를 표시합니다.
```bash
azdata arc postgres server show -n pg1
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
PostgreSQL 서버 그룹의 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--engine-version -ev`
엔진 버전이 다른 두 서버 그룹의 이름이 같은 경우 --name과 함께 --engine-version을 사용하여 PostgreSQL 하이퍼스케일 서버 그룹을 식별할 수 있습니다. --engine-version은 선택 사항으로, 서버 그룹을 식별하는 데 사용할 경우 11 또는 12여야 합니다.
#### `--path -p`
PostgreSQL 서버 그룹의 전체 사양을 기록할 경로입니다. 생략하면 사양이 표준 출력에 기록됩니다.
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
## <a name="azdata-arc-postgres-server-list"></a>azdata arc postgres server list
PostgreSQL 서버 그룹을 나열합니다.
```bash
azdata arc postgres server list 
```
### <a name="examples"></a>예
PostgreSQL 서버 그룹을 나열합니다.
```bash
azdata arc postgres server list
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

