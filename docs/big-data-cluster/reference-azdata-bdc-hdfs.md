---
title: azdata bdc hdfs 참조
titleSuffix: SQL Server big data clusters
description: azdata bdc hdfs 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e20e7574109ccce4caa6b4d9fd84a4fef65cf0fa
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531784"
---
# <a name="azdata-bdc-hdfs"></a>azdata bdc hdfs

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

다음 문서에서는 `azdata` 도구의 `sql` 명령에 대한 참조를 제공합니다. 다른 `azdata` 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc hdfs status](reference-azdata-bdc-hdfs-status.md) | Hdfs 서비스 상태 명령입니다.
[azdata bdc hdfs shell](#azdata-bdc-hdfs-shell) | HDFS 셸은 HDFS 파일 시스템을 위한 간단한 대화형 명령 셸입니다.
[azdata bdc hdfs ls](#azdata-bdc-hdfs-ls) | 지정된 파일 또는 디렉터리의 상태를 나열합니다.
[azdata bdc hdfs exists](#azdata-bdc-hdfs-exists) | 파일 또는 디렉터리가 있는지 확인합니다.  있으면 True를 반환하고, 없으면 False를 반환합니다.
[azdata bdc hdfs mkdir](#azdata-bdc-hdfs-mkdir) | 지정된 경로에 디렉터리를 만듭니다.
[azdata bdc hdfs mv](#azdata-bdc-hdfs-mv) | 지정된 파일 또는 경로를 지정된 위치로 이동합니다.
[azdata bdc hdfs create](#azdata-bdc-hdfs-create) | 지정된 위치에 텍스트 파일을 만듭니다.  데이터 매개 변수를 통해 간단한 텍스트 콘텐츠를 추가할 수 있습니다.
[azdata bdc hdfs cat](#azdata-bdc-hdfs-cat) | 파일 내용을 읽습니다.  오프셋 및 길이(바이트)는 선택적 매개 변수입니다.
[azdata bdc hdfs rm](#azdata-bdc-hdfs-rm) | 파일 또는 디렉터리를 제거합니다.
[azdata bdc hdfs rmr](#azdata-bdc-hdfs-rmr) | 파일 또는 디렉터리를 재귀적으로 제거합니다.
[azdata bdc hdfs chmod](#azdata-bdc-hdfs-chmod) | 지정된 파일 또는 디렉터리의 사용 권한을 변경합니다.
[azdata bdc hdfs chown](#azdata-bdc-hdfs-chown) | 지정된 파일의 소유자 또는 그룹을 변경합니다.
[azdata bdc hdfs cp](#azdata-bdc-hdfs-cp) | 로컬 머신과 HDFS 간에 파일 또는 디렉터리를 복사합니다.
[azdata bdc hdfs mount](reference-azdata-bdc-hdfs-mount.md) | HDFS에서 원격 저장소의 탑재를 관리합니다.
## <a name="azdata-bdc-hdfs-shell"></a>azdata bdc hdfs shell
HDFS 셸은 HDFS 파일 시스템을 위한 간단한 대화형 명령 셸입니다.
```bash
azdata bdc hdfs shell 
```
### <a name="examples"></a>예
셸을 시작합니다.
```bash
azdata bdc hdfs shell
```
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-ls"></a>azdata bdc hdfs ls
지정된 파일 또는 디렉터리의 상태를 나열합니다.
```bash
azdata bdc hdfs ls --path -p 
 ```
### <a name="examples"></a>예
상태를 나열합니다.
```bash
azdata bdc hdfs ls --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
상태를 나열할 경로입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-exists"></a>azdata bdc hdfs exists
파일 또는 디렉터리가 있는지 확인합니다.  있으면 True를 반환하고, 없으면 False를 반환합니다.
```bash
azdata bdc hdfs exists --path -p 
     ```
### Examples
Check for file or directory existance.
```bash
azdata bdc hdfs exists --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
파일 또는 디렉터리가 있는지 확인할 경로입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-mkdir"></a>azdata bdc hdfs mkdir
지정된 경로에 디렉터리를 만듭니다.
```bash
azdata bdc hdfs mkdir --path -p 
    ```
### Examples
Make directory.
```bash
azdata bdc hdfs mkdir --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
만들 디렉터리의 이름입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-mv"></a>azdata bdc hdfs mv
지정된 파일 또는 경로를 지정된 위치로 이동합니다.
```bash
azdata bdc hdfs mv --source-path -s 
                   --target-path -t
```
### <a name="examples"></a>예
파일 또는 디렉터리를 이동합니다.
```bash
azdata bdc hdfs mv --source-path '/tmp' --target-path '/dest'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--source-path -s`
이동할 디렉터리입니다.
#### `--target-path -t`
이동할 대상 위치입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-create"></a>azdata bdc hdfs create
지정된 위치에 텍스트 파일을 만듭니다.  데이터 매개 변수를 통해 간단한 텍스트 콘텐츠를 추가할 수 있습니다.
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
파일 내용입니다.  간단한 텍스트 콘텐츠를 의미합니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-cat"></a>azdata bdc hdfs cat
파일 내용을 읽습니다.  오프셋 및 길이(바이트)는 선택적 매개 변수입니다.
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
읽을 파일 내의 오프셋 바이트 수입니다.
#### `--length -l`
읽을 데이터의 길이입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-rm"></a>azdata bdc hdfs rm
파일 또는 디렉터리를 제거합니다.
```bash
azdata bdc hdfs rm --path -p 
 ```
### <a name="examples"></a>예
파일 또는 디렉터리를 제거합니다.
```bash
azdata bdc hdfs rm --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
제거할 파일의 이름입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-rmr"></a>azdata bdc hdfs rmr
파일 또는 디렉터리를 재귀적으로 제거합니다.
```bash
azdata bdc hdfs rmr --path -p 
  ```
### <a name="examples"></a>예
디렉터리를 재귀적으로 제거합니다.
```bash
azdata bdc hdfs rmr --path '/tmp'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
재귀적으로 제거할 파일의 이름입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-chmod"></a>azdata bdc hdfs chmod
지정된 파일 또는 디렉터리의 사용 권한을 변경합니다.
```bash
azdata bdc hdfs chmod --path -p 
                      --permission
```
### <a name="examples"></a>예
파일 또는 디렉터리 사용 권한을 변경합니다.
```bash
azdata bdc hdfs chmod --permission 775 --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
사용 권한을 설정할 파일 또는 디렉터리의 이름입니다.
#### `--permission`
설정할 사용 권한(8진수)입니다.  예: “775”
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-chown"></a>azdata bdc hdfs chown
지정된 파일의 소유자 또는 그룹을 변경합니다.
```bash
azdata bdc hdfs chown --path -p 
                      --owner  
                      --group -g
```
### <a name="examples"></a>예
소유자 및 그룹을 변경합니다.
```bash
azdata bdc hdfs chown --owner hdfs --group superusergroup --path '/tmp/test.txt'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
소유자를 변경할 파일 또는 디렉터리의 이름입니다.
#### `--owner`
설정할 소유자 이름입니다.
#### `--group -g`
설정할 그룹 이름입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-hdfs-cp"></a>azdata bdc hdfs cp
로컬 머신과 HDFS 간에 파일 또는 디렉터리를 복사합니다.  입력이 디렉터리인 경우 전체 디렉터리 트리가 복사됩니다.  대상 파일이나 디렉터리가 있으면 명령이 실패합니다.  원격 HDFS 디렉터리 접두사를 "hdfs:" 경로로 지정하려면 다음을 수행합니다.
```bash
azdata bdc hdfs cp --from-path -f 
                   --to-path -t
```
### <a name="examples"></a>예
로컬 머신과 HDFS 간에 파일 또는 디렉터리를 복사합니다.
```bash
azdata bdc hdfs cp --from_path '/tmp/test.txt --to-path 'hdfs:/user/me/test.txt'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--from-path -f`
복사할 경로의 이름입니다.  "hdfs:" 경로를 접두사로 사용하여 HDFS 경로를 표시합니다.
#### `--to-path -t`
복사할 경로의 이름입니다.  "hdfs:" 경로를 접두사로 사용하여 HDFS 경로를 표시합니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.

## <a name="next-steps"></a>다음 단계

다른 `azdata` 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요. `azdata` 도구를 설치하는 방법에 대한 자세한 내용은 [azdata를 설치하여 SQL Server 2019 빅 데이터 클러스터 관리](deploy-install-azdata.md)를 참조하세요.
