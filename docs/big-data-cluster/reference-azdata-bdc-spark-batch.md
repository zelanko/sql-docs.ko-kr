---
title: azdata bdc spark 일괄 처리 참조
titleSuffix: SQL Server big data clusters
description: Azdata bdc spark batch 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6e242b26f439b49dbf0b3cf5ab50ea46c273f45f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426163"
---
# <a name="azdata-bdc-spark-batch"></a>azdata bdc spark 일괄 처리

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **azdata** 도구의 **bdc spark batch** 명령에 대 한 참조를 제공 합니다. 다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md) 를 참조 하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc spark batch 만들기](#azdata-bdc-spark-batch-create) | 새 Spark 일괄 처리를 만듭니다.
[azdata bdc spark 일괄 처리 목록](#azdata-bdc-spark-batch-list) | Spark의 모든 일괄 처리를 나열 합니다.
[azdata bdc spark 일괄 처리 정보](#azdata-bdc-spark-batch-info) | 활성 Spark 일괄 처리에 대 한 정보를 가져옵니다.
[azdata bdc spark 일괄 처리 로그](#azdata-bdc-spark-batch-log) | Spark 일괄 처리에 대 한 실행 로그를 가져옵니다.
[azdata bdc spark 일괄 처리 상태](#azdata-bdc-spark-batch-state) | Spark 일괄 처리에 대 한 실행 상태를 가져옵니다.
[azdata bdc spark 일괄 삭제](#azdata-bdc-spark-batch-delete) | Spark 일괄 처리를 삭제 합니다.
## <a name="azdata-bdc-spark-batch-create"></a>azdata bdc spark batch 만들기
그러면 제공 된 코드를 실행 하는 새 batch Spark 작업이 생성 됩니다.
```bash
azdata bdc spark batch create --file -f 
                              [--class-name -c]  
                              [--arguments -a]  
                              [--jar-files -j]  
                              [--py-files -p]  
                              [--files]  
                              [--driver-memory]  
                              [--driver-cores]  
                              [--executor-memory]  
                              [--executor-cores]  
                              [--executor-count]  
                              [--archives]  
                              [--queue -q]  
                              [--name -n]  
                              [--config]
```
### <a name="examples"></a>예
새 Spark 일괄 처리를 만듭니다.
```bash
azdata spark batch create --code "2+2"
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--file -f`
실행할 파일의 경로입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--class-name -c`
하나 이상의 jar 파일을 전달할 때 실행할 클래스의 이름입니다.
#### `--arguments -a`
인수 목록입니다.  목록 JSON을 전달 하려면 값을 인코딩합니다.  예: ' ["entry1", "entry2"] '.
#### `--jar-files -j`
Jar 파일 경로의 목록입니다.  목록 JSON을 전달 하려면 값을 인코딩합니다.  예: ' ["entry1", "entry2"] '.
#### `--py-files -p`
Python 파일 경로 목록입니다.  목록 JSON을 전달 하려면 값을 인코딩합니다.  예: ' ["entry1", "entry2"] '.
#### `--files`
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
#### `--archives`
보관 경로 목록입니다.  목록 JSON을 전달 하려면 값을 인코딩합니다.  예: ' ["entry1", "entry2"] '.
#### `--queue -q`
세션을 실행할 Spark 큐의 이름입니다.
#### `--name -n`
Spark 세션의 이름입니다.
#### `--config`
Spark 구성 값을 포함 하는 이름 값 쌍의 목록입니다.  JSON 사전으로 인코딩됩니다.  예: ' {"name": "value", "name2": "value2"} '.
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
## <a name="azdata-bdc-spark-batch-list"></a>azdata bdc spark 일괄 처리 목록
Spark의 모든 일괄 처리를 나열 합니다.
```bash
azdata bdc spark batch list 
```
### <a name="examples"></a>예
모든 활성 일괄 처리를 나열 합니다.
```bash
azdata spark batch list
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
## <a name="azdata-bdc-spark-batch-info"></a>azdata bdc spark 일괄 처리 정보
지정 된 ID를 가진 Spark 일괄 처리에 대 한 정보를 가져옵니다.  일괄 처리 id는 ' spark batch 만들기 '에서 반환 됩니다.
```bash
azdata bdc spark batch info --batch-id -i 
                            
```
### <a name="examples"></a>예
ID가 0 인 일괄 처리에 대 한 일괄 처리 정보를 가져옵니다.
```bash
azdata spark batch info --batch-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--batch-id -i`
Spark 일괄 처리 ID 번호입니다.
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
## <a name="azdata-bdc-spark-batch-log"></a>azdata bdc spark 일괄 처리 로그
지정 된 ID를 가진 Spark 일괄 처리에 대 한 일괄 처리 로그 항목을 가져옵니다.  일괄 처리 id는 ' spark batch 만들기 '에서 반환 됩니다.
```bash
azdata bdc spark batch log --batch-id -i 
                           
```
### <a name="examples"></a>예
ID가 0 인 일괄 처리 로그를 가져옵니다.
```bash
azdata spark batch log --batch-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--batch-id -i`
Spark 일괄 처리 ID 번호입니다.
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
## <a name="azdata-bdc-spark-batch-state"></a>azdata bdc spark 일괄 처리 상태
지정 된 ID를 사용 하 여 Spark 일괄 처리에 대 한 일괄 처리 상태를 가져옵니다.  일괄 처리 id는 ' spark batch 만들기 '에서 반환 됩니다.
```bash
azdata bdc spark batch state --batch-id -i 
                             
```
### <a name="examples"></a>예
ID가 0 인 일괄 처리에 대 한 일괄 처리 상태를 가져옵니다.
```bash
azdata spark batch state --batch-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--batch-id -i`
Spark 일괄 처리 ID 번호입니다.
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
## <a name="azdata-bdc-spark-batch-delete"></a>azdata bdc spark 일괄 삭제
Spark 일괄 처리를 삭제 합니다. 일괄 처리 id는 ' spark batch 만들기 '에서 반환 됩니다.
```bash
azdata bdc spark batch delete --batch-id -i 
                              
```
### <a name="examples"></a>예
일괄 처리를 삭제 합니다.
```bash
azdata spark batch delete --batch-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--batch-id -i`
Spark 일괄 처리 ID 번호입니다.
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
