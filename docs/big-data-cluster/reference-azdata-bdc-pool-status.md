---
title: azdata bdc 풀 상태 참조
titleSuffix: SQL Server big data clusters
description: Azdata bdc 풀 상태 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d0a5925af4f16f2147988b2318880d9acec664c3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426133"
---
# <a name="azdata-bdc-pool-status"></a>azdata bdc 풀 상태

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **azdata** 도구의 **bdc 풀 상태** 명령에 대 한 참조를 제공 합니다. 다른 **azdata** 명령에 대 한 자세한 내용은 [azdata reference](reference-azdata.md)를 참조 하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc 풀 상태 표시](#azdata-bdc-pool-status-show) | 풀 상태.
## <a name="azdata-bdc-pool-status-show"></a>azdata bdc 풀 상태 표시
풀 상태.
```bash
azdata bdc pool status show --kind -k 
                            [--name -n]
```
### <a name="examples"></a>예
저장소 풀의 상태를 가져옵니다.
```bash
azdata bdc pool status show --kind storage --name default
```
데이터 풀의 상태를 가져옵니다.
```bash
azdata bdc pool status show --kind data --name default
```
계산 풀의 상태를 가져옵니다.
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
