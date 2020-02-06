---
title: azdata bdc control status 참조
description: azdata bdc control status 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1a617b57e4a73db83d88573b77f7058e0aab3889
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75233925"
---
# <a name="azdata-bdc-control-status"></a>azdata bdc control status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

다음 문서에서는 `bdc control` 도구의 `azdata` 명령에 대한 참조를 제공합니다. 다른 `azdata` 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc control status show](#azdata-bdc-control-status-show) | 서비스 상태를 제어합니다.
## <a name="azdata-bdc-control-status-show"></a>azdata bdc control status show
서비스 상태를 제어합니다.
```bash
azdata bdc control status show [--resource -r] 
                               [--all -a]
```
### <a name="examples"></a>예
서비스 상태를 가져옵니다.
```bash
azdata bdc control status show
```
모든 인스턴스에서 컨트롤 서비스 상태를 가져옵니다.
```bash
azdata bdc control status show --all
```
컨트롤 서비스 내에서 컨트롤 리소스의 상태를 가져옵니다.
```bash
azdata bdc control status show --resource control
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
