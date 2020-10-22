---
title: azdata arc resource 참조
titleSuffix: SQL Server big data clusters
description: azdata arc resource 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 20f96bb8ce3d88e438c28b28f49deff3b5b3054c
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358701"
---
# <a name="azdata-arc-resource"></a>azdata arc resource

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]에 적용됩니다.

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|명령|설명|
| --- | --- |
[azdata arc resource-kind list](#azdata-arc-resource-kind-list) | 정의하고 만들 수 있는 Arc의 사용 가능한 사용자 지정 리소스 종류를 나열합니다.
[azdata arc resource-kind get](#azdata-arc-resource-kind-get) | Arc 리소스 종류의 템플릿 파일을 가져옵니다.
## <a name="azdata-arc-resource-kind-list"></a>azdata arc resource-kind list
정의하고 만들 수 있는 Arc의 사용 가능한 사용자 지정 리소스 종류를 나열합니다. 나열한 후 해당 사용자 지정 리소스를 정의하거나 만드는 데 필요한 템플릿 파일을 가져올 수 있습니다.
```bash
azdata arc resource-kind list 
```
### <a name="examples"></a>예
Arc의 사용 가능한 사용자 지정 리소스 종류를 나열하기 위한 예제 명령입니다.
```bash
azdata arc resource-kind list
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
## <a name="azdata-arc-resource-kind-get"></a>azdata arc resource-kind get
Arc 리소스 종류의 템플릿 파일을 가져옵니다.
```bash
azdata arc resource-kind get --kind -k 
                             [--dest -d]
```
### <a name="examples"></a>예
Arc 리소스 종류의 CRD 템플릿 파일을 가져오기 위한 예제 명령입니다.
```bash
azdata arc resource-kind get --kind sqldb
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--kind -k`
템플릿 파일을 가져오려는 arc 리소스 종류입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--dest -d`
템플릿 파일을 저장할 디렉터리입니다.
`template`
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

