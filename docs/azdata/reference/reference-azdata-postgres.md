---
title: azdata postgres 참조
titleSuffix: SQL Server big data clusters
description: azdata postgres 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 80b83f53c486a90c635924accf36e5acff98fe2c
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942789"
---
# <a name="azdata-postgres"></a>azdata postgres

`azdata`에 적용됩니다.

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|명령|설명|
| --- | --- |
[azdata postgres shell](#azdata-postgres-shell) | Postgres용 명령줄 셸 인터페이스입니다. https://www.pgcli.com/을 참조하십시오.
[azdata postgres query](#azdata-postgres-query) | query 명령을 사용하면 데이터베이스 세션에서 PostgreSQL 명령을 실행할 수 있습니다.
## <a name="azdata-postgres-shell"></a>azdata postgres shell
Postgres용 명령줄 셸 인터페이스입니다. https://www.pgcli.com/을 참조하십시오.
```bash
azdata postgres shell [--dbname -d] 
                      [--host]  
                      
[--port -p]  
                      
[--password -w]  
                      
[--no-password]  
                      
[--single-connection]  
                      
[--username -u]  
                      
[--pgclirc]  
                      
[--dsn]  
                      
[--list-dsn]  
                      
[--row-limit]  
                      
[--less-chatty]  
                      
[--prompt]  
                      
[--prompt-dsn]  
                      
[--list -l]  
                      
[--auto-vertical-output]  
                      
[--warn]  
                      
[--no-warn]
```
### <a name="examples"></a>예제
대화형 환경을 시작하는 예제 명령줄입니다.
```bash
azdata postgres shell
```
제공된 데이터베이스와 사용자를 사용하는 예제 명령줄
```bash
azdata postgres shell --dbname <database> --username <username> --host <host>
```
전체 연결 문자열을 사용하여 시작할 예제 명령줄입니다.
```bash
azdata postgres shell --dbname postgres://user:passw0rd@example.com:5432/master 
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--dbname -d`
연결할 데이터베이스 이름입니다.
#### `--host`
postgres 데이터베이스의 호스트 주소입니다.
#### `--port -p`
postgres 인스턴스가 수신 대기하는 포트 번호입니다.
#### `--password -w`
암호 프롬프트를 강제 적용합니다.
#### `--no-password`
암호 프롬프트를 표시하지 않습니다.
#### `--single-connection`
완료 시 별도의 연결을 사용하지 않습니다.
#### `--username -u`
postgres 데이터베이스에 연결할 사용자 이름입니다.
#### `--pgclirc`
pgclirc 파일의 위치입니다.
#### `--dsn`
pgclirc 파일의 [alias_dsn] 섹션에 구성된 DSN을 사용합니다.
#### `--list-dsn`
pgclirc 파일의 [alias_dsn] 섹션에 구성된 DSN 목록입니다.
#### `--row-limit`
행 제한 프롬프트의 임계값을 설정합니다. 프롬프트를 사용하지 않으려면 0을 사용합니다.
#### `--less-chatty`
시작 시 소개와 종료 시 인사말을 건너뜁니다.
#### `--prompt`
프롬프트 형식입니다(기본값: “\u@\h:\d> ”).
#### `--prompt-dsn`
DSN 별칭을 사용하는 연결의 프롬프트 형식입니다(기본값: “\u@\h:\d> ”).
#### `--list -l`
사용 가능한 데이터베이스를 나열한 후 종료됩니다.
#### `--auto-vertical-output`
결과가 터미널 너비보다 넓으면 자동으로 세로 출력 모드로 전환됩니다.
#### `--warn`
파괴적 쿼리를 실행하기 전에 경고합니다.
#### `--no-warn`
파괴적 쿼리를 실행하기 전에 경고합니다.
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
## <a name="azdata-postgres-query"></a>azdata postgres query
query 명령을 사용하면 데이터베이스 세션에서 PostgreSQL 명령을 실행할 수 있습니다.
```bash
azdata postgres query --q -q 
                      [--host]  
                      
[--dbname -d]  
                      
[--port -p]  
                      
[--username -u]
```
### <a name="examples"></a>예
Information_schema의 모든 테이블을 나열합니다.
```bash
azdata postgres query --host <host> --username <username> -q "SELECT * FROM information_schema.tables"
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--q -q`
실행할 PostgreSQL 쿼리입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--host`
postgres 데이터베이스의 호스트 주소입니다.
`localhost`
#### `--dbname -d`
쿼리를 실행할 데이터베이스입니다.
#### `--port -p`
postgres 인스턴스가 수신 대기하는 포트 번호입니다.
`5432`
#### `--username -u`
postgres 데이터베이스에 연결할 사용자 이름입니다.
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

