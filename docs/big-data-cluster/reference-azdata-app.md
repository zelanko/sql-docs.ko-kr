---
title: azdata app 참조
titleSuffix: SQL Server big data clusters
description: azdata app 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ec7e461705138905713b803e2f0f96934044d971
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155302"
---
# <a name="azdata-app"></a>azdata app

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

이 문서는 **azdata**에 대 한 참조 문서입니다. 

## <a name="commands"></a>명령
|     |     |
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
azdata app init 
```
### <a name="examples"></a>예
새 애플리케이션 `spec.yaml`만 스캐폴드합니다.
```bash
azdata app init --spec
```
`r` 템플릿을 기반으로 새 R 응용 프로그램 응용 프로그램 구조를 스 캐 폴드 합니다.
```bash
azdata app init --name reduce --template r
```
`python` 템플릿을 기반으로 하는 새 Python 응용 프로그램 응용 프로그램 구조를 스 캐 폴드 합니다.
```bash
azdata app init --name reduce --template python
```
`ssis` 템플릿을 기반으로 새 SSIS 응용 프로그램 응용 프로그램 구조를 스 캐 폴드 합니다.
```bash
azdata app init --name reduce --template ssis            
```
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-app-create"></a>azdata app create
애플리케이션을 만듭니다.
```bash
azdata app create 
```
### <a name="examples"></a>예
유효한 spec.yaml 배포 사양이 있는 디렉터리에서 새 애플리케이션을 만듭니다.
```bash
azdata app create --spec /path/to/dir/with/spec/yaml
```
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-app-update"></a>azdata app update
애플리케이션을 업데이트합니다.
```bash
azdata app update 
```
### <a name="examples"></a>예
유효한 spec.yaml 배포 사양이 있는 디렉터리에서 기존 애플리케이션을 업데이트합니다.
```bash
azdata app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-app-list"></a>azdata app list
애플리케이션을 나열합니다.
```bash
azdata app list 
```
### <a name="examples"></a>예
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
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-app-delete"></a>azdata app delete
애플리케이션을 삭제합니다.
```bash
azdata app delete 
```
### <a name="examples"></a>예
이름 및 버전을 기준으로 애플리케이션을 삭제합니다.
```bash
azdata app delete --name reduce --version v1    
```
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-app-run"></a>azdata app run
애플리케이션을 실행합니다.
```bash
azdata app run 
```
### <a name="examples"></a>예
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
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-app-describe"></a>azdata app describe
애플리케이션을 설명합니다.
```bash
azdata app describe 
```
### <a name="examples"></a>예
애플리케이션을 설명합니다.
```bash
azdata app describe --name reduce --version v1    
```
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org/])를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.

## <a name="next-steps"></a>다음 단계

- 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요. 

- **azdata** 도구를 설치하는 방법에 대한 자세한 내용은 [azdata를 설치하여 SQL Server 2019 빅 데이터 클러스터 관리](deploy-install-azdata.md)를 참조하세요.
