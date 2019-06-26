---
title: mssqlctl bdc 컨트롤 상태 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl bdc 컨트롤 상태 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 714ed2152dfff071193a7c33ed29e5fcb9ec8f17
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394395"
---
# <a name="mssqlctl-bdc-control-status"></a>mssqlctl bdc 제어 상태

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **bdc 제어 상태** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[mssqlctl bdc 컨트롤 상태 표시](#mssqlctl-bdc-control-status-show) | 컨트롤 상태입니다.
## <a name="mssqlctl-bdc-control-status-show"></a>mssqlctl bdc 컨트롤 상태 표시
컨트롤 상태입니다.
```bash
mssqlctl bdc control status show 
```
### <a name="examples"></a>예
컨트롤의 상태를 가져옵니다.
```bash
mssqlctl bdc control status show
```
### <a name="global-arguments"></a>전역 인수
#### `--debug`
모든 디버그 로그 표시 로깅의 자세한 정도를 늘립니다.
#### `--help -h`
이 도움말 메시지 및 종료를 표시 합니다.
#### `--output -o`
출력 형식입니다.  허용 되는 값: json, jsonc, 테이블, tsv.  기본값: json.
#### `--query -q`
JMESPath 쿼리 문자열입니다. 참조 [ http://jmespath.org/ ](http://jmespath.org/]) 자세한 내용 및 예제에 대 한 합니다.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 사용-전체 디버그 로그에 대 한 디버그 합니다.

## <a name="next-steps"></a>다음 단계

설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.