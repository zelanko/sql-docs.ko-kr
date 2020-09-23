---
title: azdata app 참조
titleSuffix: SQL Server big data clusters
description: 이 참조 문서를 사용하여 azdata 도구의 SQL 명령, 특히 다양한 app 명령을 이해할 수 있습니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2d78769ddd8992f24da5f4f53da4d41362492155
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89734049"
---
# <a name="azdata-app"></a>azdata app

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

다음 문서에서는 `azdata` 도구의 `sql` 명령에 대한 참조를 제공합니다. 다른 `azdata` 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령
| 명령 | 설명 |
| --- | --- |
[azdata app template](reference-azdata-app-template.md) | 템플릿입니다.
[azdata app init](#azdata-app-init) | 새 애플리케이션 구조를 시작합니다.
[azdata app create](#azdata-app-create) | 애플리케이션을 만듭니다.
[azdata app update](#azdata-app-update) | 애플리케이션을 업데이트합니다.
[azdata app list](#azdata-app-list) | 애플리케이션을 나열합니다.
[azdata app delete](#azdata-app-delete) | 애플리케이션을 삭제합니다.
[azdata app run](#azdata-app-run) | 애플리케이션을 실행합니다.
[azdata app describe](#azdata-app-describe) | 애플리케이션을 설명합니다.
## <a name="azdata-app-init"></a>azdata app init
런타임 환경에 따라 새 애플리케이션 구조 및/또는 사양 파일을 시작할 수 있습니다.
```bash
azdata app init [--spec -s] 
                [--name -n]  
                
[--version -v]  
                
[--template -t]  
                
[--destination -d]  
                
[--url -u]
```
### <a name="examples"></a>예제
새 애플리케이션 `spec.yaml`만 스캐폴드합니다.
```bash
azdata app init --spec
```
`r` 템플릿을 기준으로 새로운 R 애플리케이션 구조를 스캐폴드합니다.
```bash
azdata app init --name reduce --template r
```
`python` 템플릿을 기준으로 새로운 Python 애플리케이션 구조를 스캐폴드합니다.
```bash
azdata app init --name reduce --template python
```
`ssis` 템플릿을 기준으로 새로운 SSIS 애플리케이션 구조를 스캐폴드합니다.
```bash
azdata app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--spec -s`
애플리케이션 spec.yaml만 생성합니다.
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
애플리케이션 버전입니다.
#### `--template -t`
템플릿 이름입니다. 지원되는 템플릿 이름의 전체 목록을 보려면 `azdata app template list`를 실행합니다.
#### `--destination -d`
애플리케이션 구조를 저장할 위치입니다. 기본값: 현재 작업 디렉터리
#### `--url -u`
다른 템플릿 리포지토리 위치를 지정합니다. 기본값: https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="azdata-app-create"></a>azdata app create
애플리케이션을 만듭니다.
```bash
azdata app create --spec -s 
                  
```
### <a name="examples"></a>예제
유효한 spec.yaml 배포 사양이 있는 디렉터리에서 새 애플리케이션을 만듭니다.
```bash
azdata app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--spec -s`
애플리케이션을 설명하는 YAML 사양 파일이 있는 디렉터리의 경로입니다.
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
## <a name="azdata-app-update"></a>azdata app update
애플리케이션을 업데이트합니다.
```bash
azdata app update [--spec -s] 
                  [--yes -y]
```
### <a name="examples"></a>예제
유효한 spec.yaml 배포 사양이 있는 디렉터리에서 기존 애플리케이션을 업데이트합니다.
```bash
azdata app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--spec -s`
애플리케이션을 설명하는 YAML 사양 파일이 있는 디렉터리의 경로입니다.
#### `--yes -y`
CWD의 spec.yaml 파일에서 애플리케이션을 업데이트할 때 확인 메시지를 표시하지 않습니다.
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
## <a name="azdata-app-list"></a>azdata app list
애플리케이션을 나열합니다.
```bash
azdata app list [--name -n] 
                [--version -v]
```
### <a name="examples"></a>예제
이름 및 버전을 기준으로 애플리케이션을 나열합니다.
```bash
azdata app list --name reduce  --version v1
```
이름을 기준으로 모든 애플리케이션 버전을 나열합니다.
```bash
azdata app list --name reduce
```
이름을 기준으로 모든 애플리케이션 버전을 나열합니다.
```bash
azdata app list
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
애플리케이션 버전입니다.
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
## <a name="azdata-app-delete"></a>azdata app delete
애플리케이션을 삭제합니다.
```bash
azdata app delete --name -n 
                  --version -v
```
### <a name="examples"></a>예제
이름 및 버전을 기준으로 애플리케이션을 삭제합니다.
```bash
azdata app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
애플리케이션 버전입니다.
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
## <a name="azdata-app-run"></a>azdata app run
애플리케이션을 실행합니다.
```bash
azdata app run --name -n 
               --version -v  
               
[--inputs]
```
### <a name="examples"></a>예제
입력 매개 변수 없이 애플리케이션을 실행합니다.
```bash
azdata app run --name reduce --version v1
```
입력 매개 변수 1개를 사용하여 애플리케이션을 실행합니다.
```bash
azdata app run --name reduce --version v1 --inputs x=10
```
여러 개의 입력 매개 변수를 사용하여 애플리케이션을 실행합니다.
```bash
azdata app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
애플리케이션 버전입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--inputs`
CSV `name=value` 형식의 애플리케이션 입력 매개 변수입니다.
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
## <a name="azdata-app-describe"></a>azdata app describe
애플리케이션을 설명합니다.
```bash
azdata app describe [--spec -s] 
                    [--name -n]  
                    
[--version -v]
```
### <a name="examples"></a>예제
애플리케이션을 설명합니다.
```bash
azdata app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--spec -s`
애플리케이션을 설명하는 YAML 사양 파일이 있는 디렉터리의 경로입니다.
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
애플리케이션 버전입니다.
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

다른 `azdata` 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요. `azdata` 도구를 설치하는 방법에 대한 자세한 내용은 [azdata를 설치하여 SQL Server 2019 빅 데이터 클러스터 관리](../install/deploy-install-azdata.md)를 참조하세요.
