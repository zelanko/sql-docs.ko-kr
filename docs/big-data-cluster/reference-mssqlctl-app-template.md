---
title: mssqlctl 앱 템플릿 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 앱 템플릿 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0b4cbae0ba35c0cef777b3535b2012ab78f8e6da
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473449"
---
# <a name="mssqlctl-app-template"></a>mssqlctl 앱 템플릿

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **앱 템플릿** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl 앱 템플릿 목록](#mssqlctl-app-template-list) | 지원 되는 템플릿을 가져옵니다.
[mssqlctl 앱 템플릿 끌어오기](#mssqlctl-app-template-pull) | 지원 되는 템플릿을 다운로드 합니다.
## <a name="mssqlctl-app-template-list"></a>mssqlctl 앱 템플릿 목록
지정 된 [URL] github 리포지토리에서 지원 되는 템플릿을 가져옵니다.
```bash
mssqlctl app template list [--url -u] 
                           
```
### <a name="examples"></a>예
기본 템플릿 저장소 위치에서 모든 템플릿을 가져옵니다.
```bash
mssqlctl app template list
```
다른 저장소 위치에서 모든 템플릿을 가져옵니다.
```bash
mssqlctl app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>선택적 매개 변수
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
## <a name="mssqlctl-app-template-pull"></a>mssqlctl 앱 템플릿 끌어오기
지정 된 [URL] github 리포지토리에서 지원 되는 템플릿을 다운로드 합니다.
```bash
mssqlctl app template pull [--name -n] 
                           [--url -u]  
                           [--destination -d]
```
### <a name="examples"></a>예
기본 템플릿 저장소 위치에서 모든 템플릿을 다운로드 합니다.
```bash
mssqlctl app template pull
```
다른 저장소 위치에서 모든 템플릿을 다운로드 합니다.
```bash
mssqlctl app template list --url https://github.com/diffrent/templates.git
```
이름으로 개별 템플릿을 다운로드 합니다.
```bash
mssqlctl app template pull --name ssis            
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--name -n`
템플릿 이름입니다. 전체 목록은 지원 되는 템플릿 namesrun 해제 `mssqlctl app template list`
#### `--url -u`
다른 템플릿 저장소 위치를 지정 합니다. 기본값: https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
응용 프로그램 기본 서식 파일을 배치할 위치입니다.
`./templates`
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