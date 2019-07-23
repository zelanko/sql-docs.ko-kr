---
title: mssqlctl 앱 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl app 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d0df3e9ca007fb6546310236f4c23d1775687cc5
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388394"
---
# <a name="mssqlctl-app"></a>mssqlctl 앱

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **mssqlctl** 도구의 **응용 프로그램** 명령에 대 한 참조를 제공 합니다. 다른 **mssqlctl** 명령에 대 한 자세한 내용은 [mssqlctl reference](reference-mssqlctl.md)를 참조 하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl 앱 템플릿](reference-mssqlctl-app-template.md) | 모음.
[mssqlctl 앱 초기화](#mssqlctl-app-init) | 새 응용 프로그램 구조를 Kickstart.
[mssqlctl app 만들기](#mssqlctl-app-create) | 응용 프로그램을 만듭니다.
[mssqlctl 앱 업데이트](#mssqlctl-app-update) | 응용 프로그램을 업데이트 합니다.
[mssqlctl 앱 목록](#mssqlctl-app-list) | 응용 프로그램을 나열 합니다.
[mssqlctl 앱 삭제](#mssqlctl-app-delete) | 응용 프로그램을 삭제 합니다.
[mssqlctl 앱 실행](#mssqlctl-app-run) | 응용 프로그램을 실행 합니다.
[mssqlctl 앱 설명](#mssqlctl-app-describe) | 응용 프로그램을 설명 합니다.
## <a name="mssqlctl-app-init"></a>mssqlctl 앱 초기화
런타임 환경에 따라 새 응용 프로그램 구조 및/또는 사양 파일을 kickstart 수 있습니다.
```bash
mssqlctl app init [--spec -s] 
                  [--name -n]  
                  [--version -v]  
                  [--template -t]  
                  [--destination -d]  
                  [--url -u]
```
### <a name="examples"></a>예
스 캐 폴드는 새 응용 `spec.yaml` 프로그램에만 적용 됩니다.
```bash
mssqlctl app init --spec
```
`r` 템플릿을 기반으로 새 R 응용 프로그램 구조를 스 캐 폴드 합니다.
```bash
mssqlctl app init --name reduce --template r
```
`python` 템플릿을 기반으로 하는 새 Python 응용 프로그램 구조를 스 캐 폴드 합니다.
```bash
mssqlctl app init --name reduce --template python
```
`ssis` 템플릿을 기반으로 새 SSIS 응용 프로그램 구조를 스 캐 폴드 합니다.
```bash
mssqlctl app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--spec -s`
응용 프로그램 사양만 생성 합니다.
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
응용 프로그램 버전.
#### `--template -t`
템플릿 이름입니다. 전체 목록을 해제 하는 경우 지원 되는 템플릿 이름이 실행 됩니다.`mssqlctl app template list`
#### `--destination -d`
응용 프로그램 구조를 저장할 위치입니다. 기본값: 현재 작업 디렉터리입니다.
#### `--url -u`
다른 템플릿 리포지토리 위치를 지정 하십시오. 기본 https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="mssqlctl-app-create"></a>mssqlctl app 만들기
응용 프로그램을 만듭니다.
```bash
mssqlctl app create --spec -s 
                    
```
### <a name="examples"></a>예
유효한 사양과 aml 배포 사양을 포함 하는 디렉터리에서 새 응용 프로그램을 만듭니다.
```bash
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--spec -s`
응용 프로그램을 설명 하는 YAML 사양 파일이 있는 디렉터리의 경로입니다.
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
## <a name="mssqlctl-app-update"></a>mssqlctl 앱 업데이트
응용 프로그램을 업데이트 합니다.
```bash
mssqlctl app update [--spec -s] 
                    [--yes -y]
```
### <a name="examples"></a>예
유효한 사양과 aml 배포 사양이 포함 된 디렉터리에서 기존 응용 프로그램을 업데이트 합니다.
```bash
mssqlctl app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--spec -s`
응용 프로그램을 설명 하는 YAML 사양 파일이 있는 디렉터리의 경로입니다.
#### `--yes -y`
CWD의 사양 .yaml 파일에서 응용 프로그램을 업데이트할 때 확인 메시지를 표시 하지 않습니다.
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
## <a name="mssqlctl-app-list"></a>mssqlctl 앱 목록
응용 프로그램을 나열 합니다.
```bash
mssqlctl app list [--name -n] 
                  [--version -v]
```
### <a name="examples"></a>예
이름 및 버전별 응용 프로그램을 나열 합니다.
```bash
mssqlctl app list --name reduce  --version v1
```
모든 응용 프로그램 버전을 이름별로 나열 합니다.
```bash
mssqlctl app list --name reduce
```
모든 응용 프로그램 버전을 이름별로 나열 합니다.
```bash
mssqlctl app list
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
응용 프로그램 버전.
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
## <a name="mssqlctl-app-delete"></a>mssqlctl 앱 삭제
응용 프로그램을 삭제 합니다.
```bash
mssqlctl app delete --name -n 
                    --version -v
```
### <a name="examples"></a>예
이름 및 버전으로 응용 프로그램을 삭제 합니다.
```bash
mssqlctl app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
응용 프로그램 버전.
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
## <a name="mssqlctl-app-run"></a>mssqlctl 앱 실행
응용 프로그램을 실행 합니다.
```bash
mssqlctl app run --name -n 
                 --version -v  
                 [--inputs]
```
### <a name="examples"></a>예
입력 매개 변수 없이 응용 프로그램을 실행 합니다.
```bash
mssqlctl app run --name reduce --version v1
```
입력 매개 변수 1 개를 사용 하 여 응용 프로그램을 실행 합니다.
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10
```
여러 입력 매개 변수를 사용 하 여 응용 프로그램을 실행 합니다.
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
응용 프로그램 버전.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--inputs`
CSV `name=value` 형식의 응용 프로그램 입력 매개 변수입니다.
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
## <a name="mssqlctl-app-describe"></a>mssqlctl 앱 설명
응용 프로그램을 설명 합니다.
```bash
mssqlctl app describe [--spec -s] 
                      [--name -n]  
                      [--version -v]
```
### <a name="examples"></a>예
응용 프로그램을 설명 합니다.
```bash
mssqlctl app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--spec -s`
응용 프로그램을 설명 하는 YAML 사양 파일이 있는 디렉터리의 경로입니다.
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
응용 프로그램 버전.
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

다른 **mssqlctl** 명령에 대 한 자세한 내용은 [mssqlctl reference](reference-mssqlctl.md)를 참조 하세요. **Mssqlctl** 도구를 설치 하는 방법에 대 한 자세한 내용은 [install mssqlctl to manage SQL Server 2019 빅 data 클러스터](deploy-install-mssqlctl.md)를 참조 하세요.