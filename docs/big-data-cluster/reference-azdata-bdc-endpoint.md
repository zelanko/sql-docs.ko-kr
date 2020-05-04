---
title: azdata bdc endpoint 참조
titleSuffix: SQL Server big data clusters
description: azdata bdc endpoint 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 71f52b8312518cf669751d50dcc857c3d892bd98
ms.sourcegitcommit: db1b6153f0bc2d221ba1ce15543ecc83e1045453
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82588079"
---
# <a name="azdata-bdc-endpoint"></a>azdata bdc endpoint

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

다음 문서에서는 `azdata` 도구의 `bdc endpoint` 명령에 대한 참조를 제공합니다. 다른 `azdata` 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc endpoint list](#azdata-bdc-endpoint-list) | 빅 데이터 클러스터의 엔드포인트를 나열합니다.
## <a name="azdata-bdc-endpoint-list"></a>azdata bdc endpoint list
빅 데이터 클러스터의 엔드포인트를 나열합니다.

```bash
azdata bdc endpoint list [--endpoint-name -e] 
```

### <a name="optional-parameters"></a>선택적 매개 변수

#### `--endpoint-name -e`

빅 데이터 클러스터 엔드포인트 이름입니다.

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
