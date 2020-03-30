---
title: azdata notebook 참조
titleSuffix: SQL Server big data clusters
description: azdata notebook 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0a866dcca1debba47abf2e2e241d00151b8641ff
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74820966"
---
# <a name="azdata-notebook"></a>azdata notebook

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

다음 문서에서는 `notebook` 도구의 `azdata` 명령에 대한 참조를 제공합니다. 다른 `azdata` 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata notebook view](#azdata-notebook-view) | Notebook을 봅니다.  첫 번째 셀 실행 오류 발생 시 중지하는 옵션입니다.
[azdata notebook run](#azdata-notebook-run) | Notebook을 실행합니다.  첫 번째 오류 발생 시 실행이 중지됩니다.
## <a name="azdata-notebook-view"></a>azdata notebook view
이 명령은 Notebook 파일을 사용하고 Markdown, 코드 및 출력을 색 터미널 형식으로 변환할 수 있습니다.
```bash
azdata notebook view --path -p 
                     [--continue-on-error -c]
```
### <a name="examples"></a>예
Notebook을 봅니다.  모든 셀이 표시됩니다.
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb'
```
Notebook을 봅니다.  출력에 오류가 있는 셀이 없으면 모든 셀이 표시됩니다.  이 경우 출력이 중지됩니다.
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb' --stop-on-error
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
보려는 Notebook의 경로입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--continue-on-error -c`
Notebook 출력에 있는 셀 오류를 무시하고 추가 셀을 계속 표시합니다.  기본 동작은 오류 발생 시 중지하는 것입니다.  중지하면 오류가 발생한 첫 번째 셀을 더 쉽게 확인할 수 있습니다.
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
## <a name="azdata-notebook-run"></a>azdata notebook run
이 명령은 임시 디렉터리를 만들고 이 디렉터리를 작업 디렉터리로 사용하여 지정된 Notebook을 실행합니다.
```bash
azdata notebook run --path -p 
                    [--output-path]  
                    [--output-html]  
                    [--arguments -a]  
                    [--interactive -i]  
                    [--clear -c]  
                    [--timeout -t]
```
### <a name="examples"></a>예
Notebook을 실행합니다.
```bash
azdata notebook run --path '/home/me/notebooks/demo_notebook.ipynb'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
실행할 Notebook의 파일 경로입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--output-path`
Notebook 출력에 사용할 디렉터리 경로입니다.  출력 데이터가 포함된 Notebook 및 Notebook에서 생성된 모든 파일은 이 디렉터리를 기준으로 생성됩니다.
#### `--output-html`
출력 Notebook을 HTML 형식으로 추가 변환할지 여부를 나타내는 선택적 플래그입니다.  두 번째 출력 파일을 만듭니다.
#### `--arguments -a`
Notebook 실행에 삽입할 수 있는 Notebook 인수의 선택적 목록입니다.  JSON 사전으로 인코딩됩니다.  예: '{"name":"value", "name2":"value2"}'
#### `--interactive -i`
대화형 모드에서 Notebook을 실행합니다.
#### `--clear -c`
대화형 모드에서는 셀을 렌더링하기 전에 콘솔을 선택 취소합니다.
#### `--timeout -t`
실행이 완료될 때까지 대기하는 시간(초)입니다. 값 -1은 무기한 대기를 나타냅니다.
`600`
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
