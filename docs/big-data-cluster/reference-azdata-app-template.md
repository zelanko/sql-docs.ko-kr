---
title: azdata app template 참조
titleSuffix: SQL Server big data clusters
description: azdata app template 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 07911616659a29df7f7fa6ce4d356a9c82789ae2
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153222"
---
# <a name="azdata-app-template"></a>azdata app template

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

이 문서는 **azdata**에 대 한 참조 문서입니다. 

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata app template list](#azdata-app-template-list) | 지원되는 템플릿을 가져옵니다.
[azdata app template pull](#azdata-app-template-pull) | 지원되는 템플릿을 다운로드합니다.
## <a name="azdata-app-template-list"></a>azdata app template list
지정된 [URL] github 리포지토리에서 지원되는 템플릿을 가져옵니다.
```bash
azdata app template list 
```
### <a name="examples"></a>예
기본 템플릿 리포지토리 위치에 있는 템플릿을 모두 가져옵니다.
```bash
azdata app template list
```
다른 리포지토리 위치에 있는 템플릿을 모두 가져옵니다.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
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
## <a name="azdata-app-template-pull"></a>azdata app template pull
지정된 [URL] github 리포지토리에서 지원되는 템플릿을 다운로드합니다.
```bash
azdata app template pull 
```
### <a name="examples"></a>예
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
