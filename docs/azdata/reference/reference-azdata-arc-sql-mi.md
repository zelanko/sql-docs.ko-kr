---
title: azdata arc sql mi 참조
titleSuffix: SQL Server big data clusters
description: azdata arc sql mi 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 234a990cde52a6fd051410d30000413b9acfa3a0
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358681"
---
# <a name="azdata-arc-sql-mi"></a>azdata arc sql mi

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]에 적용됩니다.

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|명령|설명|
| --- | --- |
[azdata arc sql mi create](#azdata-arc-sql-mi-create) | SQL 관리형 인스턴스를 만듭니다.
[azdata arc sql mi edit](#azdata-arc-sql-mi-edit) | SQL 관리형 인스턴스의 구성을 편집합니다.
[azdata arc sql mi delete](#azdata-arc-sql-mi-delete) | SQL 관리형 인스턴스를 삭제합니다.
[azdata arc sql mi show](#azdata-arc-sql-mi-show) | SQL 관리형 인스턴스의 세부 정보를 표시합니다.
[azdata arc sql mi list](#azdata-arc-sql-mi-list) | SQL 관리형 인스턴스를 나열합니다.
[azdata arc sql mi config](reference-azdata-arc-sql-mi-config.md) | 구성 명령입니다.
## <a name="azdata-arc-sql-mi-create"></a>azdata arc sql mi create
SQL 관리형 인스턴스의 암호를 설정하려면 AZDATA_PASSWORD 환경 변수를 설정합니다.
```bash
azdata arc sql mi create --name -n 
                         [--path]  
                         
[--cores-limit -cl]  
                         
[--cores-request -cr]  
                         
[--memory-limit -ml]  
                         
[--memory-request -mr]  
                         
[--storage-class-data -scd]  
                         
[--storage-class-logs -scl]  
                         
[--storage-class-data-logs -scdl]  
                         
[--storage-class-backups -scb]  
                         
[--volume-size-data -vsd]  
                         
[--volume-size-logs -vsl]  
                         
[--volume-size-data-logs -vsdl]  
                         
[--volume-size-backups -vsb]  
                         
[--no-external-endpoint]  
                         
[--dev]  
                         
[--no-wait]
```
### <a name="examples"></a>예
SQL 관리형 인스턴스를 만듭니다.
```bash
azdata arc sql mi create -n sqlmi1
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
SQL 관리형 인스턴스의 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--path`
SQL 관리형 인스턴스 json 파일의 src 파일 경로입니다.
#### `--cores-limit -cl`
관리형 인스턴스의 코어 한도(정수)입니다.
#### `--cores-request -cr`
관리형 인스턴스의 코어(정수)에 대한 요청입니다.
#### `--memory-limit -ml`
관리형 인스턴스의 용량 한도(정수)입니다.
#### `--memory-request -mr`
관리형 인스턴스의 용량(GB 단위의 정수 메모리 크기)에 대한 요청입니다.
#### `--storage-class-data -scd`
데이터(.mdf)에 사용할 스토리지 클래스입니다. 값을 지정하지 않으면 스토리지 클래스가 지정되지 않으므로 Kubernetes에서 기본 스토리지 클래스를 사용합니다.
#### `--storage-class-logs -scl`
로그(/var/log)에 사용할 스토리지 클래스입니다. 값을 지정하지 않으면 스토리지 클래스가 지정되지 않으므로 Kubernetes에서 기본 스토리지 클래스를 사용합니다.
#### `--storage-class-data-logs -scdl`
데이터베이스 로그(.ldf)에 사용할 스토리지 클래스입니다. 값을 지정하지 않으면 스토리지 클래스가 지정되지 않으므로 Kubernetes에서 기본 스토리지 클래스를 사용합니다.
#### `--storage-class-backups -scb`
백업(/var/opt/mssql/backups)에 사용할 스토리지 클래스입니다. 값을 지정하지 않으면 스토리지 클래스가 지정되지 않으므로 Kubernetes에서 기본 스토리지 클래스를 사용합니다.
#### `--volume-size-data -vsd`
데이터에 사용할 스토리지 볼륨 크기로, 양수 뒤에 Ki(킬로바이트), Mi(메가바이트) 또는 Gi(기가바이트)가 옵니다.
#### `--volume-size-logs -vsl`
로그에 사용할 스토리지 볼륨 크기로, 양수 뒤에 Ki(킬로바이트), Mi(메가바이트) 또는 Gi(기가바이트)가 옵니다.
#### `--volume-size-data-logs -vsdl`
데이터 로그에 사용할 스토리지 볼륨 크기로, 양수 뒤에 Ki(킬로바이트), Mi(메가바이트) 또는 Gi(기가바이트)가 옵니다.
#### `--volume-size-backups -vsb`
백업에 사용할 스토리지 볼륨 크기로, 양수 뒤에 Ki(킬로바이트), Mi(메가바이트) 또는 Gi(기가바이트)가 옵니다.
#### `--no-external-endpoint`
지정하면 외부 서비스가 생성되지 않습니다. 지정하지 않으면 데이터 컨트롤러와 동일한 서비스 유형을 사용하여 외부 서비스가 생성됩니다.
#### `--dev`
이 매개 변수를 지정하면 개발 인스턴스로 간주되어 요금이 청구되지 않습니다.
#### `--no-wait`
지정된 경우에는 인스턴스가 준비 상태로 전환될 때까지 기다리지 않고 명령이 반환됩니다.
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
## <a name="azdata-arc-sql-mi-edit"></a>azdata arc sql mi edit
SQL 관리형 인스턴스의 구성을 편집합니다.
```bash
azdata arc sql mi edit --name -n 
                       [--path]  
                       
[--cores-limit -cl]  
                       
[--cores-request -cr]  
                       
[--memory-limit -ml]  
                       
[--memory-request -mr]  
                       
[--dev]  
                       
[--no-wait]
```
### <a name="examples"></a>예
SQL 관리형 인스턴스의 구성을 편집합니다.
```bash
azdata arc sql mi edit --path ./spec.json -n sqlmi1
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
편집 중인 SQL 관리형 인스턴스의 이름입니다. 인스턴스를 배포하는 데 사용되는 이름은 변경할 수 없습니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--path`
SQL 관리형 인스턴스 json 파일의 src 파일 경로입니다.
#### `--cores-limit -cl`
관리형 인스턴스의 코어 한도(정수)입니다.
#### `--cores-request -cr`
관리형 인스턴스의 코어(정수)에 대한 요청입니다.
#### `--memory-limit -ml`
관리형 인스턴스의 용량 한도(정수)입니다.
#### `--memory-request -mr`
관리형 인스턴스의 용량(GB 단위의 정수 메모리 크기)에 대한 요청입니다.
#### `--dev`
이 매개 변수를 지정하면 개발 인스턴스로 간주되어 요금이 청구되지 않습니다.
#### `--no-wait`
지정된 경우에는 인스턴스가 준비 상태로 전환될 때까지 기다리지 않고 명령이 반환됩니다.
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
## <a name="azdata-arc-sql-mi-delete"></a>azdata arc sql mi delete
SQL 관리형 인스턴스를 삭제합니다.
```bash
azdata arc sql mi delete --name -n 
                         
```
### <a name="examples"></a>예
SQL 관리형 인스턴스를 삭제합니다.
```bash
azdata arc sql mi delete -n sqlmi1
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
삭제할 SQL 관리형 인스턴스의 이름입니다.
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
## <a name="azdata-arc-sql-mi-show"></a>azdata arc sql mi show
SQL 관리형 인스턴스의 세부 정보를 표시합니다.
```bash
azdata arc sql mi show --name -n 
                       [--path -p]
```
### <a name="examples"></a>예
SQL 관리형 인스턴스의 세부 정보를 표시합니다.
```bash
azdata arc sql mi show -n sqlmi1
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
표시할 SQL 관리형 인스턴스의 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--path -p`
SQL 관리형 인스턴스의 전체 사양을 기록할 경로입니다. 생략하면 사양이 표준 출력에 기록됩니다.
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
## <a name="azdata-arc-sql-mi-list"></a>azdata arc sql mi list
SQL 관리형 인스턴스를 나열합니다.
```bash
azdata arc sql mi list 
```
### <a name="examples"></a>예
SQL 관리형 인스턴스를 나열합니다.
```bash
azdata arc sql mi list
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

