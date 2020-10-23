---
title: azdata sql 참조
titleSuffix: SQL Server big data clusters
description: azdata sql 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 794c7be56eaa0591d120b4fea40a725fdeecaac1
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358111"
---
# <a name="azdata-sql"></a>azdata sql

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]에 적용됩니다.

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|명령|설명|
| --- | --- |
[azdata sql shell](#azdata-sql-shell) | 사용자는 SQL CLI를 사용하여 T-SQL을 통해 SQL Server 및 Azure SQL을 조작할 수 있습니다.
[azdata sql query](#azdata-sql-query) | 사용자는 SQL CLI를 사용하여 T-SQL을 통해 SQL Server 및 Azure SQL을 조작할 수 있습니다.
## <a name="azdata-sql-shell"></a>azdata sql shell
사용자는 SQL CLI를 사용하여 T-SQL을 통해 SQL Server 및 Azure SQL을 조작할 수 있습니다.
```bash
azdata sql shell [--username -u] 
                 [--database -d]  
                 
[--server -s]  
                 
[--integrated -e]  
                 
[--mssqlclirc]  
                 
[--row-limit]  
                 
[--less-chatty]  
                 
[--auto-vertical-output]  
                 
[--encrypt -n]  
                 
[--trust-server-certificate -c]  
                 
[--connect-timeout -l]  
                 
[--application-intent -k]  
                 
[--multi-subnet-failover -m]  
                 
[--packet-size]  
                 
[--dac-connection -a]  
                 
[--input-file -i]  
                 
[--output-file]  
                 
[--enable-sqltoolsservice-logging]  
                 
[--prompt]
```
### <a name="examples"></a>예제
대화형 환경을 시작하는 예제 명령줄입니다.
```bash
azdata sql shell
```
제공된 서버, 사용자 및 데이터베이스를 사용하는 예제 명령줄
```bash
azdata sql shell --server localhost --username sa --database master         
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--username -u`
데이터베이스에 연결할 사용자 이름입니다.
#### `--database -d`
연결할 데이터베이스 이름입니다.
#### `--server -s`
SQL Server 인스턴스 이름 또는 주소입니다.
#### `--integrated -e`
Windows의 통합 인증을 사용합니다.
#### `--mssqlclirc`
mssqlclirc 구성 파일의 위치입니다.
#### `--row-limit`
행 제한 프롬프트의 임계값을 설정합니다. 프롬프트를 사용하지 않으려면 0을 사용합니다.
#### `--less-chatty`
시작 시 소개와 종료 시 인사말을 건너뜁니다.
#### `--auto-vertical-output`
결과가 터미널 너비보다 넓으면 자동으로 세로 출력 모드로 전환됩니다.
#### `--encrypt -n`
서버에 인증서가 설치되어 있는 경우 SQL Server는 모든 데이터에 대하여 SSL 암호화를 사용합니다.
#### `--trust-server-certificate -c`
신뢰의 유효성을 검사하기 위해 인증서 체인의 탐색을 무시하는 동안 채널은 암호화됩니다.
#### `--connect-timeout -l`
요청을 종료하기 전에 서버 연결을 대기하는 시간(초)입니다.
#### `--application-intent -k`
SQL Server 가용성 그룹의 데이터베이스에 연결할 때 애플리케이션 작업 유형을 선언합니다.
#### `--multi-subnet-failover -m`
애플리케이션이 다른 서브넷의 Always On 가용성 그룹에 연결하는 경우 이를 설정하면 현재 활성 서버에 대한 빠른 검색 및 연결이 가능합니다.
#### `--packet-size`
SQL Server와 통신하는 데 사용되는 네트워크 패킷의 바이트 단위 크기입니다.
#### `--dac-connection -a`
관리자 전용 연결을 사용하여 SQL Server에 연결합니다.
#### `--input-file -i`
SQL 문 일괄 처리가 포함된 파일을 지정합니다.
#### `--output-file`
쿼리의 출력을 받는 파일을 지정합니다.
#### `--enable-sqltoolsservice-logging`
SqlToolsService에 대하여 진단 로깅을 사용하도록 설정합니다.
#### `--prompt`
프롬프트 형식(기본값: \d>
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
## <a name="azdata-sql-query"></a>azdata sql query
사용자는 SQL CLI를 사용하여 T-SQL을 통해 SQL Server 및 Azure SQL을 조작할 수 있습니다.
```bash
azdata sql query -q 
                 [--database -d]  
                 
[--username -u]  
                 
[--server -s]  
                 
[--integrated -e]
```
### <a name="examples"></a>예
테이블 이름 목록을 선택하는 명령줄 예입니다.
```bash
azdata sql query --server localhost --username sa --database master -q "SELECT name FROM SYS.TABLES"
```
### <a name="required-parameters"></a>필수 매개 변수
#### `-q`
실행할 T-SQL 쿼리입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--database -d`
연결할 데이터베이스 이름입니다.
`master`
#### `--username -u`
데이터베이스에 연결할 사용자 이름입니다.
#### `--server -s`
SQL Server 인스턴스 이름 또는 주소입니다.
#### `--integrated -e`
Windows의 통합 인증을 사용합니다.
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

