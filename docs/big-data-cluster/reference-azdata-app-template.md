---
title: azdata 앱 템플릿 참조
titleSuffix: SQL Server big data clusters
description: Azdata 앱 템플릿 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3b257a2bacc56a7907ab0d25f492ed0ebd605543
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426333"
---
# <a name="azdata-app-template"></a>azdata 앱 템플릿

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **azdata** 도구의 **앱 템플릿** 명령에 대 한 참조를 제공 합니다. 다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md)를 참조 하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata 앱 템플릿 목록](#azdata-app-template-list) | 지원 되는 템플릿을 가져옵니다.
[azdata 앱 템플릿 풀](#azdata-app-template-pull) | 지원 되는 템플릿 다운로드
## <a name="azdata-app-template-list"></a>azdata 앱 템플릿 목록
지정 된 [URL] github 리포지토리에서 지원 되는 템플릿을 가져옵니다.
```bash
azdata app template list [--url -u] 
                         
```
### <a name="examples"></a>예
기본 템플릿 리포지토리 위치 아래의 모든 템플릿을 가져옵니다.
```bash
azdata app template list
```
다른 리포지토리 위치에 있는 모든 템플릿을 가져옵니다.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>선택적 매개 변수
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
## <a name="azdata-app-template-pull"></a>azdata 앱 템플릿 풀
지정 된 [URL] github 리포지토리에서 지원 되는 템플릿을 다운로드 합니다.
```bash
azdata app template pull [--name -n] 
                         [--url -u]  
                         [--destination -d]
```
### <a name="examples"></a>예
기본 템플릿 리포지토리 위치 아래의 모든 템플릿을 다운로드 합니다.
```bash
azdata app template pull
```
다른 리포지토리 위치에 있는 모든 템플릿을 다운로드 합니다.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
이름별로 개별 템플릿을 다운로드 합니다.
```bash
azdata app template pull --name ssis            
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--name -n`
템플릿 이름입니다. 전체 목록은 지원 되는 템플릿 namesrun`azdata app template list`
#### `--url -u`
다른 템플릿 리포지토리 위치를 지정 하십시오. 기본 https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
응용 프로그램 구조 템플릿을 저장할 위치입니다.
`./templates`
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
