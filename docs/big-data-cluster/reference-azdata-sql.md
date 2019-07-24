---
title: azdata sql 참조
titleSuffix: SQL Server big data clusters
description: Azdata sql 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 90512592901fcf83e4697b5eefc80a6df7aeb032
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426023"
---
# <a name="azdata-sql"></a>azdata sql

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대 한 참조를 제공 합니다. 다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md)를 참조 하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata sql shell](#azdata-sql-shell) | 사용자는 SQL DB CLI를 사용 하 여 T-sql을 통해 SQL Server와 상호 작용할 수 있습니다.
[azdata sql 쿼리](#azdata-sql-query) | 쿼리 명령을 사용 하면 T-sql 쿼리를 실행할 수 있습니다.
## <a name="azdata-sql-shell"></a>azdata sql shell
사용자는 SQL DB CLI를 사용 하 여 T-sql을 통해 SQL Server와 상호 작용할 수 있습니다.
```bash
azdata sql shell 
```
### <a name="examples"></a>예
대화형 환경을 시작 하는 예제 명령줄입니다.
```bash
azdata sql shell
```
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
## <a name="azdata-sql-query"></a>azdata sql 쿼리
쿼리 명령을 사용 하면 T-sql 쿼리를 실행할 수 있습니다.
```bash
azdata sql query --database -d 
                 -q
```
### <a name="examples"></a>예
테이블 이름 목록을 선택 합니다.  데이터베이스 기본값은 master입니다.
```bash
azdata sql query 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--database -d`
쿼리를 실행할 데이터베이스입니다.  기본값은 master입니다.
#### `-q`
실행할 t-sql 쿼리입니다.
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

**Azdata** 도구를 설치 하는 방법에 대 한 자세한 내용은 [install azdata to manage SQL Server 2019 빅 data 클러스터](deploy-install-azdata.md)를 참조 하세요.
