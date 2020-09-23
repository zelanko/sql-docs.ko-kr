---
title: azdata app template 참조
titleSuffix: SQL Server big data clusters
description: 이 참조 문서를 사용하여 azdata 도구의 SQL 명령, 특히 app template 명령을 이해할 수 있습니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 37371ec8d909115aedf1eb745a78fec7af427cc4
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2020
ms.locfileid: "89734060"
---
# <a name="azdata-app-template"></a>azdata app template

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

다음 문서에서는 `azdata` 도구의 `sql` 명령에 대한 참조를 제공합니다. 다른 `azdata` 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령
| 명령 | 설명 |
| --- | --- |
[azdata app template list](#azdata-app-template-list) | 지원되는 템플릿을 가져옵니다.
[azdata app template pull](#azdata-app-template-pull) | 지원되는 템플릿을 다운로드합니다.
## <a name="azdata-app-template-list"></a>azdata app template list
지정된 [URL] github 리포지토리에서 지원되는 템플릿을 가져옵니다.
```bash
azdata app template list [--url -u] 
                         
```
### <a name="examples"></a>예제
기본 템플릿 리포지토리 위치에 있는 템플릿을 모두 가져옵니다.
```bash
azdata app template list
```
다른 리포지토리 위치에 있는 템플릿을 모두 가져옵니다.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>선택적 매개 변수
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
## <a name="azdata-app-template-pull"></a>azdata app template pull
지정된 [URL] github 리포지토리에서 지원되는 템플릿을 다운로드합니다.
```bash
azdata app template pull [--name -n] 
                         [--url -u]  
                         
[--destination -d]
```
### <a name="examples"></a>예제
기본 템플릿 리포지토리 위치에 있는 템플릿을 모두 다운로드합니다.
```bash
azdata app template pull
```
다른 리포지토리 위치에 있는 템플릿을 모두 다운로드합니다.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
이름을 기준으로 개별 템플릿을 다운로드합니다.
```bash
azdata app template pull --name ssis            
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--name -n`
템플릿 이름입니다. 지원되는 템플릿 이름의 전체 목록을 보려면 `azdata app template list`를 실행합니다.
#### `--url -u`
다른 템플릿 리포지토리 위치를 지정합니다. 기본값: https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
애플리케이션 구조 템플릿을 저장할 위치입니다.
`./templates`
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
