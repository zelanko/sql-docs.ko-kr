---
title: azdata 확장 참조
titleSuffix: SQL Server big data clusters
description: azdata 확장 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 16facb611565f02d1b07ae8a46f53ba2b83b3bfc
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914395"
---
# <a name="azdata-extension"></a>azdata 확장

`azdata`에 적용됩니다.

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|명령|설명|
| --- | --- |
[azdata extension add](#azdata-extension-add) | 확장을 추가합니다.
[azdata extension remove](#azdata-extension-remove) | 확장을 제거합니다.
[azdata extension list](#azdata-extension-list) | 설치된 모든 확장을 나열합니다.
## <a name="azdata-extension-add"></a>azdata extension add
확장을 추가합니다.
```bash
azdata extension add --source -s 
                     [--index]  
                     
[--pip-proxy]  
                     
[--pip-extra-index-urls]  
                     
[--yes -y]
```
### <a name="examples"></a>예제
URL에서 확장을 추가합니다.
```bash
azdata extension add --source https://contoso.com/some_ext-0.0.1-py2.py3-none-any.whl```
Add extension from local disk.
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl```
Add extension from local disk and use pip proxy for dependencies.
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl --pip-proxy https://user:pass@proxy.server:8080
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--source -s`
디스크의 확장 휠 또는 확장에 대한 URL의 경로입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--index`
Python 패키지 인덱스의 기준 URL입니다(기본값: https://pypi.org/simple) ). PEP 503(간단한 리포지토리 API) 규격 리포지토리 또는 동일한 형식으로 명시된 로컬 디렉터리를 가리켜야 합니다.
#### `--pip-proxy`
pip이 확장 종속성에 대해 [user:passwd@]proxy.server:port의 형식으로 사용할 프록시입니다.
#### `--pip-extra-index-urls`
사용할 패키지 인덱스의 추가 URL을 공백으로 구분한 목록입니다. PEP 503(간단한 리포지토리 API) 규격 리포지토리 또는 동일한 형식으로 명시된 로컬 디렉터리를 가리켜야 합니다.
#### `--yes -y`
확인을 묻는 메시지를 표시하지 마세요.
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
## <a name="azdata-extension-remove"></a>azdata extension remove
확장을 제거합니다.
```bash
azdata extension remove --name -n 
                        [--yes -y]
```
### <a name="examples"></a>예제
확장을 제거합니다.
```bash
azdata extension remove --name some-ext
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--name -n`
확장의 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--yes -y`
확인을 묻는 메시지를 표시하지 마세요.
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
## <a name="azdata-extension-list"></a>azdata extension list
설치된 모든 확장을 나열합니다.
```bash
azdata extension list 
```
### <a name="examples"></a>예제
확장을 나열합니다.
```bash
azdata extension list
```
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

다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요. 

**azdata** 도구를 설치하는 방법에 대한 자세한 내용은 [azdata 설치](..\install\deploy-install-azdata.md)를 참조하세요.

