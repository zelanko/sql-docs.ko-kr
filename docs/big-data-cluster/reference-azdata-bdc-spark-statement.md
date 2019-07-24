---
title: azdata bdc spark 문 참조
titleSuffix: SQL Server big data clusters
description: Azdata bdc spark 문 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 778980ac6b93e7db79d59182fbd18ab4cfdb8b75
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426093"
---
# <a name="azdata-bdc-spark-statement"></a>azdata bdc spark 문

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

다음 문서에서는 **azdata** 도구의 **bdc spark 문** 명령에 대 한 참조를 제공 합니다. 다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md) 를 참조 하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc spark 문 목록](#azdata-bdc-spark-statement-list) | 지정 된 Spark 세션의 모든 문을 나열 합니다.
[azdata bdc spark 문 만들기](#azdata-bdc-spark-statement-create) | 지정 된 세션에서 새 Spark 문을 만듭니다.
[azdata bdc spark 문 정보](#azdata-bdc-spark-statement-info) | 지정 된 Spark 세션에서 요청 된 문에 대 한 정보를 가져옵니다.
[azdata bdc spark 문 취소](#azdata-bdc-spark-statement-cancel) | 지정 된 Spark 세션 내에서 문을 취소 합니다.
## <a name="azdata-bdc-spark-statement-list"></a>azdata bdc spark 문 목록
지정 된 Spark 세션의 모든 문을 나열 합니다.
```bash
azdata bdc spark statement list --session-id -i 
                                
```
### <a name="examples"></a>예
모든 session 문을 나열 합니다.
```bash
azdata spark statement list --session-id 0
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
## <a name="azdata-bdc-spark-statement-create"></a>azdata bdc spark 문 만들기
그러면 지정 된 세션에서 새 문이 생성 되 고 실행 됩니다.  Execute가 quick 이면 결과에 실행의 출력이 포함 됩니다.  그렇지 않으면 문이 완료 된 후 ' spark 세션 정보 '를 사용 하 여 결과를 검색할 수 있습니다.
```bash
azdata bdc spark statement create --session-id -i 
                                  --code -c
```
### <a name="examples"></a>예
문을 실행 합니다.
```bash
azdata spark statement create --session-id 0 --code "2+2"
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--session-id -i`
Spark 세션 ID 번호입니다.
#### `--code -c`
문의 일부로 실행할 코드를 포함 하는 문자열입니다.
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
## <a name="azdata-bdc-spark-statement-info"></a>azdata bdc spark 문 정보
문이 완료 된 경우 실행 상태 및 실행 결과를 가져옵니다. 문 id는 ' spark 문 만들기 '에서 반환 됩니다.
```bash
azdata bdc spark statement info --session-id -i 
                                --statement-id -s
```
### <a name="examples"></a>예
ID가 0이 고 문 ID가 0 인 세션에 대 한 문 정보를 가져옵니다.
```bash
azdata spark statement info --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--session-id -i`
Spark 세션 ID 번호입니다.
#### `--statement-id -s`
지정 된 세션 ID 내의 Spark 문 ID 번호입니다.
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
## <a name="azdata-bdc-spark-statement-cancel"></a>azdata bdc spark 문 취소
지정 된 Spark 세션 내에서 문을 취소 합니다. 문 id는 ' spark 문 만들기 '에서 반환 됩니다.
```bash
azdata bdc spark statement cancel --session-id -i 
                                  --statement-id -s
```
### <a name="examples"></a>예
문을 취소 합니다.
```bash
azdata spark statement cancel --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--session-id -i`
Spark 세션 ID 번호입니다.
#### `--statement-id -s`
지정 된 세션 ID 내의 Spark 문 ID 번호입니다.
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
