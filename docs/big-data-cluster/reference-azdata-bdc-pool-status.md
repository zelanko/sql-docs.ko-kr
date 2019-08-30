---
title: azdata bdc pool status 참조
titleSuffix: SQL Server big data clusters
description: azdata bdc pool status 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ee49ee09107c98047bd5aea849b9ae486eb6736a
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153109"
---
# <a name="azdata-bdc-pool-status"></a>azdata bdc pool status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

이 문서는 **azdata**에 대 한 참조 문서입니다. 

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc pool status show](#azdata-bdc-pool-status-show) | 풀 상태입니다.
## <a name="azdata-bdc-pool-status-show"></a>azdata bdc pool status show
풀 상태입니다.
```bash
azdata bdc pool status show --kind -k 
                            [--name -n]
```
### <a name="examples"></a>예
스토리지 풀의 상태를 가져옵니다.
```bash
azdata bdc pool status show --kind storage --name default
```
데이터 풀의 상태를 가져옵니다.
```bash
azdata bdc pool status show --kind data --name default
```
컴퓨팅 풀의 상태를 가져옵니다.
```bash
azdata bdc pool status show --kind compute --name default
```
마스터 풀의 상태를 가져옵니다.
```bash
azdata bdc pool status show --kind master --name default
```
Spark 풀의 상태를 가져옵니다.
```bash
azdata bdc pool status show --kind spark --name default
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--kind -k`
빅 데이터 클러스터 풀 종류입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--name -n`
빅 데이터 클러스터 풀 이름입니다.
`default`
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
