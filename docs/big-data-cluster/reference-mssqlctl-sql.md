---
title: mssqlctl sql 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl sql 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 844ea94e9df18132fd0729745ff154783b578fc1
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728502"
---
# <a name="mssqlctl-sql"></a>mssqlctl sql

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **sql** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl sql 셸](#mssqlctl-sql-shell) | SQL DB CLI T-SQL을 통해 SQL Server와 상호 작용할 수가 있습니다.
[mssqlctl sql 쿼리](#mssqlctl-sql-query) | 쿼리 명령에는 T-SQL 쿼리 실행 수 있습니다.
## <a name="mssqlctl-sql-shell"></a>mssqlctl sql 셸
SQL DB CLI T-SQL을 통해 SQL Server와 상호 작용할 수가 있습니다.
```bash
mssqlctl sql shell 
```
### <a name="examples"></a>예
예제 명령줄 대화형 환경을 시작 합니다.
```bash
mssqlctl sql shell
```
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
## <a name="mssqlctl-sql-query"></a>mssqlctl sql 쿼리
쿼리 명령에는 T-SQL 쿼리 실행 수 있습니다.
```bash
mssqlctl sql query --database -d 
                   -q
```
### <a name="examples"></a>예
테이블 이름 목록을 선택 합니다.  데이터베이스 기본값은 master입니다.
```bash
mssqlctl sql query 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--database -d`
데이터베이스에서 쿼리를 실행 하는입니다.  기본값은 master입니다.
#### `-q`
실행할 T-SQL 쿼리입니다.
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

설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.