---
title: azdata bdc hdfs 참조
titleSuffix: SQL Server big data clusters
description: Azdata bdc hdfs 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8e892c2d501902ef915a297440ae5a6ffda83bce
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426183"
---
# <a name="azdata-bdc-hdfs"></a>azdata bdc hdfs

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **azdata** 도구의 **bdc hdfs** 명령에 대 한 참조를 제공 합니다. 다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md)를 참조 하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc hdfs shell](#azdata-bdc-hdfs-shell) | HDFS shell은 HDFS 파일 시스템에 대 한 간단한 대화형 명령 셸입니다.
[azdata bdc hdfs ls](#azdata-bdc-hdfs-ls) | 지정 된 파일 또는 디렉터리의 상태를 나열 합니다.
[azdata bdc hdfs 존재](#azdata-bdc-hdfs-exists) | 파일이 나 디렉터리가 있는지 확인 합니다.  있는 경우 True를 반환 하 고 그렇지 않으면 False를 반환 합니다.
[azdata bdc hdfs mkdir](#azdata-bdc-hdfs-mkdir) | 지정 된 경로에 디렉터리를 만듭니다.
[azdata bdc hdfs mv](#azdata-bdc-hdfs-mv) | 지정 된 파일 또는 경로를 지정 된 위치로 이동 합니다.
[azdata bdc hdfs 만들기](#azdata-bdc-hdfs-create) | 지정 된 위치에 텍스트 파일을 만듭니다.  단순 텍스트 콘텐츠는 데이터 매개 변수를 통해 추가할 수 있습니다.
[azdata bdc hdfs cat](#azdata-bdc-hdfs-cat) | 파일의 내용을 읽습니다.  오프셋 및 길이 (바이트)는 선택적 매개 변수입니다.
[azdata bdc hdfs rm](#azdata-bdc-hdfs-rm) | 파일이 나 디렉터리를 제거 합니다.
[azdata bdc hdfs rmr](#azdata-bdc-hdfs-rmr) | 파일이 나 디렉터리를 재귀적으로 제거 합니다.
[azdata bdc hdfs chmod](#azdata-bdc-hdfs-chmod) | 지정 된 파일 또는 디렉터리에 대 한 사용 권한을 변경 합니다.
[azdata bdc hdfs chown](#azdata-bdc-hdfs-chown) | 지정 된 파일의 소유자 또는 그룹을 변경 합니다.
[azdata bdc hdfs 탑재](reference-azdata-bdc-hdfs-mount.md) | HDFS에서 원격 저장소의 탑재를 관리 합니다.
## <a name="azdata-bdc-hdfs-shell"></a>azdata bdc hdfs shell
HDFS shell은 HDFS 파일 시스템에 대 한 간단한 대화형 명령 셸입니다.
```bash
azdata bdc hdfs shell 
```
### <a name="examples"></a>예
셸을 시작 합니다.
```bash
azdata bdc hdfs shell
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
## <a name="azdata-bdc-hdfs-ls"></a>azdata bdc hdfs ls
지정 된 파일 또는 디렉터리의 상태를 나열 합니다.
```bash
azdata bdc hdfs ls --path -p 
                   
```
### <a name="examples"></a>예
상태 나열
```bash
azdata bdc hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
상태를 나열할 경로입니다.
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
## <a name="azdata-bdc-hdfs-exists"></a>azdata bdc hdfs 존재
파일이 나 디렉터리가 있는지 확인 합니다.  있는 경우 True를 반환 하 고 그렇지 않으면 False를 반환 합니다.
```bash
azdata bdc hdfs exists --path -p 
                       
```
### <a name="examples"></a>예
공존 파일 또는 디렉터리를 확인 합니다.
```bash
azdata bdc hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
존재 여부를 확인할 경로입니다.
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
## <a name="azdata-bdc-hdfs-mkdir"></a>azdata bdc hdfs mkdir
지정 된 경로에 디렉터리를 만듭니다.
```bash
azdata bdc hdfs mkdir --path -p 
                      
```
### <a name="examples"></a>예
디렉터리를 만듭니다.
```bash
azdata bdc hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
만들 디렉터리의 이름입니다.
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
## <a name="azdata-bdc-hdfs-mv"></a>azdata bdc hdfs mv
지정 된 파일 또는 경로를 지정 된 위치로 이동 합니다.
```bash
azdata bdc hdfs mv --source-path -s 
                   --target-path -t
```
### <a name="examples"></a>예
파일 또는 디렉터리를 이동 합니다.
```bash
azdata bdc hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--source-path -s`
이동할 디렉터리입니다.
#### `--target-path -t`
이동할 위치입니다.
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
## <a name="azdata-bdc-hdfs-create"></a>azdata bdc hdfs 만들기
지정 된 위치에 텍스트 파일을 만듭니다.  단순 텍스트 콘텐츠는 데이터 매개 변수를 통해 추가할 수 있습니다.
```bash
azdata bdc hdfs create --path -p 
                       --data -d
```
### <a name="examples"></a>예
파일을 만듭니다.
```bash
azdata bdc hdfs create --path '/tmp/test.txt' --data "This is a test."
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
만들 파일의 이름입니다.
#### `--data -d`
파일의 콘텐츠입니다.  간단한 텍스트 콘텐츠를 의미 합니다.
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
## <a name="azdata-bdc-hdfs-cat"></a>azdata bdc hdfs cat
파일의 내용을 읽습니다.  오프셋 및 길이 (바이트)는 선택적 매개 변수입니다.
```bash
azdata bdc hdfs cat --path -p 
                    --offset  
                    --length -l
```
### <a name="examples"></a>예
파일을 읽습니다.
```bash
azdata bdc hdfs cat --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
읽을 파일의 이름입니다.
#### `--offset`
읽을 파일 내에 있는 바이트의 오프셋입니다.
#### `--length -l`
읽을 데이터의 길이입니다.
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
## <a name="azdata-bdc-hdfs-rm"></a>azdata bdc hdfs rm
파일이 나 디렉터리를 제거 합니다.
```bash
azdata bdc hdfs rm --path -p 
                   
```
### <a name="examples"></a>예
파일이 나 디렉터리를 제거 합니다.
```bash
azdata bdc hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
제거할 파일의 이름입니다.
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
## <a name="azdata-bdc-hdfs-rmr"></a>azdata bdc hdfs rmr
파일이 나 디렉터리를 재귀적으로 제거 합니다.
```bash
azdata bdc hdfs rmr --path -p 
                    
```
### <a name="examples"></a>예
디렉터리를 재귀적으로 제거 합니다.
```bash
azdata bdc hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
재귀적으로 제거할 파일의 이름입니다.
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
## <a name="azdata-bdc-hdfs-chmod"></a>azdata bdc hdfs chmod
지정 된 파일 또는 디렉터리에 대 한 사용 권한을 변경 합니다.
```bash
azdata bdc hdfs chmod --path -p 
                      --permission
```
### <a name="examples"></a>예
파일 또는 디렉터리 권한을 변경 하십시오.
```bash
azdata bdc hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
사용 권한을 설정할 파일 또는 디렉터리의 이름입니다.
#### `--permission`
설정할 사용 권한 8 진수입니다.  예: "775".
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
## <a name="azdata-bdc-hdfs-chown"></a>azdata bdc hdfs chown
지정 된 파일의 소유자 또는 그룹을 변경 합니다.
```bash
azdata bdc hdfs chown --path -p 
                      --owner  
                      --group -g
```
### <a name="examples"></a>예
소유자 및 그룹을 변경 합니다.
```bash
azdata bdc hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
소유자를 변경할 파일 또는 디렉터리의 이름입니다.
#### `--owner`
설정할 소유자 이름입니다.
#### `--group -g`
로 설정할 그룹 이름입니다.
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
