---
title: azdata bdc spark 세션 참조
titleSuffix: SQL Server big data clusters
description: Azdata bdc spark session 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 20b7ac3dcf72482e80278ce0f0df922026232a6d
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426103"
---
# <a name="azdata-bdc-spark-session"></a>azdata bdc spark 세션

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

다음 문서에서는 **azdata** 도구의 **bdc spark 세션** 명령에 대 한 참조를 제공 합니다. 다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md) 를 참조 하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc spark 세션 만들기](#azdata-bdc-spark-session-create) | 새 Spark 세션을 만듭니다.
[azdata bdc spark 세션 목록](#azdata-bdc-spark-session-list) | Spark의 모든 활성 세션을 나열 합니다.
[azdata bdc spark 세션 정보](#azdata-bdc-spark-session-info) | 활성 Spark 세션에 대 한 정보를 가져옵니다.
[azdata bdc spark 세션 로그](#azdata-bdc-spark-session-log) | 활성 Spark 세션에 대 한 실행 로그를 가져옵니다.
[azdata bdc spark 세션 상태](#azdata-bdc-spark-session-state) | 활성 Spark 세션의 실행 상태를 가져옵니다.
[azdata bdc spark 세션 삭제](#azdata-bdc-spark-session-delete) | Spark 세션을 삭제 합니다.
## <a name="azdata-bdc-spark-session-create"></a>azdata bdc spark 세션 만들기
그러면 새 대화형 Spark 세션이 만들어집니다. 호출자는 Spark 세션의 유형을 지정 해야 합니다. 이 세션은 azdata 실행의 수명 보다 오래 지속 되며 ' spark 세션 삭제 '를 사용 하 여 삭제 해야 합니다.
```bash
azdata bdc spark session create [--session-kind -k] 
                                [--jar-files -j]  
                                [--py-files -p]  
                                [--files -f]  
                                [--driver-memory]  
                                [--driver-cores]  
                                [--executor-memory]  
                                [--executor-cores]  
                                [--executor-count]  
                                [--archives -a]  
                                [--queue -q]  
                                [--name -n]  
                                [--config -c]  
                                [--timeout-seconds -t]
```
### <a name="examples"></a>예
세션을 만듭니다.
```bash
azdata spark session create --session-kind pyspark
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--session-kind -k`
만들 세션 형식의 이름입니다.  Spark, pyspark, sparkr 또는 sql 중 하나입니다.
#### `--jar-files -j`
Jar 파일 경로의 목록입니다.  목록 JSON을 전달 하려면 값을 인코딩합니다.  예: ' ["entry1", "entry2"] '.
#### `--py-files -p`
Python 파일 경로 목록입니다.  목록 JSON을 전달 하려면 값을 인코딩합니다.  예: ' ["entry1", "entry2"] '.
#### `--files -f`
파일 경로 목록입니다.  목록 JSON을 전달 하려면 값을 인코딩합니다.  예: ' ["entry1", "entry2"] '.
#### `--driver-memory`
드라이버에 할당할 메모리의 양입니다.  단위를 값의 일부로 지정 합니다.  예 512M 또는 2G.
#### `--driver-cores`
드라이버에 할당할 CPU 코어의 양입니다.
#### `--executor-memory`
실행자에 할당할 메모리의 양입니다.  단위를 값의 일부로 지정 합니다.  예 512M 또는 2G.
#### `--executor-cores`
실행자에 할당할 CPU 코어의 양입니다.
#### `--executor-count`
실행할 실행자 인스턴스 수입니다.
#### `--archives -a`
보관 경로 목록입니다.  목록 JSON을 전달 하려면 값을 인코딩합니다.  예: ' ["entry1", "entry2"] '.
#### `--queue -q`
세션을 실행할 Spark 큐의 이름입니다.
#### `--name -n`
Spark 세션의 이름입니다.
#### `--config -c`
Spark 구성 값을 포함 하는 이름 값 쌍의 목록입니다.  JSON 사전으로 인코딩됩니다.  예: ' {"name": "value", "name2": "value2"} '.
#### `--timeout-seconds -t`
세션 유휴 시간 제한 (초)입니다.
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
## <a name="azdata-bdc-spark-session-list"></a>azdata bdc spark 세션 목록
Spark의 모든 활성 세션을 나열 합니다.
```bash
azdata bdc spark session list 
```
### <a name="examples"></a>예
모든 활성 세션을 나열 합니다.
```bash
azdata spark session list
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
## <a name="azdata-bdc-spark-session-info"></a>azdata bdc spark 세션 정보
지정 된 ID를 사용 하 여 활성 Spark 세션에 대 한 세션 정보를 가져옵니다.  세션 id는 ' spark 세션 만들기 '에서 반환 됩니다.
```bash
azdata bdc spark session info --session-id -i 
                              
```
### <a name="examples"></a>예
ID가 0 인 세션에 대 한 세션 정보를 가져옵니다.
```bash
azdata spark session info --session-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--session-id -i`
Spark 세션 ID 번호입니다.
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
## <a name="azdata-bdc-spark-session-log"></a>azdata bdc spark 세션 로그
지정 된 ID를 가진 활성 Spark 세션의 세션 로그 항목을 가져옵니다.  세션 id는 ' spark 세션 만들기 '에서 반환 됩니다.
```bash
azdata bdc spark session log --session-id -i 
                             
```
### <a name="examples"></a>예
ID가 0 인 세션에 대 한 세션 로그를 가져옵니다.
```bash
azdata spark session log --session-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--session-id -i`
Spark 세션 ID 번호입니다.
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
## <a name="azdata-bdc-spark-session-state"></a>azdata bdc spark 세션 상태
지정 된 ID를 사용 하 여 활성 Spark 세션의 세션 상태를 가져옵니다.  세션 id는 ' spark 세션 만들기 '에서 반환 됩니다.
```bash
azdata bdc spark session state --session-id -i 
                               
```
### <a name="examples"></a>예
ID가 0 인 세션에 대 한 세션 상태를 가져옵니다.
```bash
azdata spark session state --session-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--session-id -i`
Spark 세션 ID 번호입니다.
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
## <a name="azdata-bdc-spark-session-delete"></a>azdata bdc spark 세션 삭제
그러면 대화형 Spark 세션이 삭제 됩니다. 세션 id는 ' spark 세션 만들기 '에서 반환 됩니다.
```bash
azdata bdc spark session delete --session-id -i 
                                
```
### <a name="examples"></a>예
세션을 삭제 합니다.
```bash
azdata spark session delete --session-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--session-id -i`
Spark 세션 ID 번호입니다.
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
