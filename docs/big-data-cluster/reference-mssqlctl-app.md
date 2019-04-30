---
title: mssqlctl 앱 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 앱 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 850964adc9cd790a27cf69e3e0f5229cdaf589c8
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473268"
---
# <a name="mssqlctl-app"></a>mssqlctl 앱

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **앱** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl 앱 템플릿](reference-mssqlctl-app-template.md) | 템플릿을 구성 합니다.
[mssqlctl 앱 초기화](#mssqlctl-app-init) | Kickstart 새 응용 프로그램 구조입니다.
[mssqlctl 앱 만들기](#mssqlctl-app-create) | 응용 프로그램을 만듭니다.
[mssqlctl 앱 업데이트](#mssqlctl-app-update) | 응용 프로그램을 업데이트 합니다.
[mssqlctl 앱 목록](#mssqlctl-app-list) | 응용 프로그램을 나열 합니다.
[mssqlctl 앱 삭제](#mssqlctl-app-delete) | 응용 프로그램을 삭제 합니다.
[mssqlctl 앱 실행](#mssqlctl-app-run) | 응용 프로그램을 실행 합니다.
[mssqlctl 앱 설명](#mssqlctl-app-describe) | 응용 프로그램에 설명 합니다.
## <a name="mssqlctl-app-init"></a>mssqlctl 앱 초기화
Kickstart 새 응용 프로그램 구조 및/또는 런타임 환경에 따라 사양 파일에 도움이 됩니다.
```bash
mssqlctl app init [--spec -s] 
                  [--name -n]  
                  [--version -v]  
                  [--template -t]  
                  [--destination -d]  
                  [--url -u]
```
### <a name="examples"></a>예
새 응용 프로그램을 스 캐 폴드 `spec.yaml` 만 합니다.
```bash
mssqlctl app init --spec
```
에 따라 새 R 응용 프로그램 응용 프로그램 구조를 스 캐 폴드는 `r` 템플릿.
```bash
mssqlctl app init --name reduce --template r
```
기반으로 하는 새 Python 응용 프로그램 응용 프로그램 구조를 스 캐 폴드는 `python` 템플릿.
```bash
mssqlctl app init --name reduce --template python
```
에 따라 새 SSIS 응용 프로그램 응용 프로그램 구조를 스 캐 폴드는 `ssis` 템플릿.
```bash
mssqlctl app init --name reduce --template ssis            
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--spec -s`
응용 프로그램 spec.yaml만 생성 합니다.
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
응용 프로그램 버전입니다.
#### `--template -t`
템플릿 이름입니다. 전체 목록을 실행 하는 지원 되는 템플릿 이름 해제 `mssqlctl app template list`
#### `--destination -d`
응용 프로그램 구조를 배치할 위치입니다. 기본값: 현재 작업 디렉터리입니다.
#### `--url -u`
다른 템플릿 저장소 위치를 지정 합니다. 기본값: https://github.com/Microsoft/SQLBDC-AppDeploy.git
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
## <a name="mssqlctl-app-create"></a>mssqlctl 앱 만들기
응용 프로그램을 만듭니다.
```bash
mssqlctl app create --spec -s 
                    
```
### <a name="examples"></a>예
유효한 spec.yaml 배포 사양이 포함 되어 있는 디렉터리에서 새 응용 프로그램을 만듭니다.
```bash
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--spec -s`
응용 프로그램을 설명 하는 YAML 사양 파일을 사용 하 여 디렉터리 경로입니다.
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
## <a name="mssqlctl-app-update"></a>mssqlctl 앱 업데이트
응용 프로그램을 업데이트 합니다.
```bash
mssqlctl app update [--spec -s] 
                    [--yes -y]
```
### <a name="examples"></a>예
유효한 spec.yaml 배포 사양이 포함 되어 있는 디렉터리에서 기존 응용 프로그램을 업데이트 합니다.
```bash
mssqlctl app update --spec /path/to/dir/with/spec/yaml    
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--spec -s`
응용 프로그램을 설명 하는 YAML 사양 파일을 사용 하 여 디렉터리 경로입니다.
#### `--yes -y`
CWD의 spec.yaml 파일에서 응용 프로그램을 업데이트 하는 경우 확인 표시 되지 않습니다.
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
## <a name="mssqlctl-app-list"></a>mssqlctl 앱 목록
응용 프로그램을 나열 합니다.,
```bash
mssqlctl app list [--name -n] 
                  [--version -v]
```
### <a name="examples"></a>예
응용 프로그램 이름과 버전을 나열 합니다.
```bash
mssqlctl app list --name reduce  --version v1
```
이름으로 모든 응용 프로그램 버전을 나열 합니다.
```bash
mssqlctl app list --name reduce
```
이름으로 모든 응용 프로그램 버전을 나열 합니다.
```bash
mssqlctl app list
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
응용 프로그램 버전입니다.
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
## <a name="mssqlctl-app-delete"></a>mssqlctl 앱 삭제
응용 프로그램을 삭제 합니다.
```bash
mssqlctl app delete --name -n 
                    --version -v
```
### <a name="examples"></a>예
이름 및 버전에 따라 응용 프로그램을 삭제 합니다.
```bash
mssqlctl app delete --name reduce --version v1    
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
응용 프로그램 버전입니다.
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
1 입력된 매개 변수를 사용 하 여 응용 프로그램을 실행 합니다.
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10
```
여러 입력된 매개 변수를 사용 하 여 응용 프로그램을 실행 합니다.
```bash
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6    
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
응용 프로그램 버전입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--inputs`
응용 프로그램 입력 매개 변수를 CSV에 `name=value` 형식입니다.
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
## <a name="mssqlctl-app-describe"></a>mssqlctl 앱 설명
응용 프로그램에 설명 합니다.
```bash
mssqlctl app describe [--spec -s] 
                      [--name -n]  
                      [--version -v]
```
### <a name="examples"></a>예
응용 프로그램에 설명 합니다.
```bash
mssqlctl app describe --name reduce --version v1    
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--spec -s`
응용 프로그램을 설명 하는 YAML 사양 파일을 사용 하 여 디렉터리 경로입니다.
#### `--name -n`
애플리케이션 이름.
#### `--version -v`
응용 프로그램 버전입니다.
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

다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다. 설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.