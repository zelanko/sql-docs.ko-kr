---
title: azdata bdc sql status 참조
titleSuffix: SQL Server big data clusters
description: azdata bdc sql status 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 81c1a84ea196e7f986f9427605de575f59a3152c
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531706"
---
# <a name="azdata-bdc-sql-status"></a>azdata bdc sql status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

다음 문서에서는 `azdata` 도구의 `sql` 명령에 대한 참조를 제공합니다. 다른 `azdata` 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc sql status 표시](#azdata-bdc-sql-status-show) | Sql-server 서비스 상태.
## <a name="azdata-bdc-sql-status-show"></a>azdata bdc sql status 표시
Sql-server 서비스 상태.
```bash
azdata bdc sql status show [--resource -r] 
                           [--all -a]
```
### <a name="examples"></a>예
sql 서비스의 상태를 가져옵니다.
```bash
azdata bdc sql status show
```
모든 인스턴스에서 sql 서비스 상태를 가져옵니다.
```bash
azdata bdc sql status show --all
```
sql 서비스 내에서 마스터 리소스의 상태를 가져옵니다.
```bash
azdata bdc sql status show --resource master
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--resource -r`
이 서비스에서 이 리소스를 가져옵니다.
#### `--all -a`
서비스 내에서 각 리소스의 모든 인스턴스를 표시합니다.
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
