---
title: azdata 노트북 참조
titleSuffix: SQL Server big data clusters
description: Azdata 노트북 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b96c5e06ec51f53964a28cac86f385d6b42c1dc4
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426013"
---
# <a name="azdata-notebook"></a>azdata 노트북

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **azdata** 도구의 **노트북** 명령에 대 한 참조를 제공 합니다. 다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md) 를 참조 하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata 노트북 보기](#azdata-notebook-view) | 노트북 보기  첫 번째 셀 실행 오류에서 중지 하는 옵션입니다.
[azdata 노트북 실행](#azdata-notebook-run) | 노트북을 실행 합니다.  첫 번째 오류 발생 시 실행이 중지 됩니다.
## <a name="azdata-notebook-view"></a>azdata 노트북 보기
이 명령은 노트북 파일을 사용 하 여 markdown, 코드 및 출력을 색 터미널 형식으로 변환할 수 있습니다.
```bash
azdata notebook view --path -p 
                     [--continue-on-error -c]
```
### <a name="examples"></a>예
노트북 보기  모든 셀이 표시 됩니다.
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb'
```
노트북 보기  출력에 오류가 있는 셀이 발견 되지 않는 한 모든 셀이 표시 됩니다.  이 경우 출력이 중지 됩니다.
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb' --stop-on-error
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
보려는 노트북의 경로입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--continue-on-error -c`
노트북 출력에 있는 셀 오류를 무시 하 고 추가 셀을 계속 표시 합니다.  기본 동작은 오류 발생 시 중지 하는 것입니다.  를 중지 하면 오류가 발생 한 첫 번째 셀을 더 쉽게 볼 수 있습니다.
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
## <a name="azdata-notebook-run"></a>azdata 노트북 실행
이 명령은 임시 디렉터리를 만들고이 디렉터리 내에서 작업 디렉터리로 지정 된 노트북을 실행 합니다.
```bash
azdata notebook run --path -p 
                    [--output-path]  
                    [--output-html]
```
### <a name="examples"></a>예
노트북을 실행 합니다.
```bash
azdata notebook run --path '/home/me/notebooks/demo_notebook.ipynb'
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--path -p`
실행할 노트북의 파일 경로입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--output-path`
전자 필기장 출력에 사용할 디렉터리 경로입니다.  출력 데이터 및 모든 노트북 생성 파일이 포함 된 노트북은이 디렉터리를 기준으로 생성 됩니다.
#### `--output-html`
선택적 플래그 indicatingg는 출력 노트북을 HTML 형식으로 추가로 변환할지 여부를 결정 합니다.  두 번째 출력 파일을 만듭니다.
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

**Azdata** 도구를 설치 하는 방법에 대 한 자세한 내용은 [install azdata to manage SQL Server 2019 빅 data 클러스터](deploy-install-azdata.md)를 참조 하세요.
