---
title: azdata bdc debug 참조
titleSuffix: SQL Server big data clusters
description: azdata bdc debug 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d2cdb04cfc0bf98e2143b8e7b5ae67a7b0db9069
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653360"
---
# <a name="azdata-bdc-debug"></a>azdata bdc debug

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에서는 **azdata** 도구의 **bdc debug** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc debug copy-logs](#azdata-bdc-debug-copy-logs) | 로그를 복사합니다.
[azdata bdc debug dump](#azdata-bdc-debug-dump) | 로깅 덤프를 트리거합니다.
## <a name="azdata-bdc-debug-copy-logs"></a>azdata bdc debug copy-logs
빅 데이터 클러스터에서 디버그 로그를 복사합니다. 시스템에 kube 구성이 있어야 합니다.
```bash
azdata bdc debug copy-logs --namespace -n 
                           [--container -c]  
                           [--target-folder -d]  
                           [--pod -p]  
                           [--timeout -t]
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--namespace -n`
Kubernetes 네임스페이스에 사용되는 빅 데이터 클러스터 이름입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--container -c`
유사한 이름을 가진 컨테이너의 로그를 복사합니다. 선택 사항이며, 기본적으로 모든 컨테이너의 로그를 복사합니다. 여러 번 지정할 수 없습니다. 여러 번 지정하면 마지막 항목이 사용됩니다.
#### `--target-folder -d`
로그를 복사할 대상 폴더 경로입니다. 선택 사항이며, 기본적으로 로컬 폴더에 결과를 만듭니다.  여러 번 지정할 수 없습니다. 여러 번 지정하면 마지막 항목이 사용됩니다.
#### `--pod -p`
유사한 이름을 가진 Pod의 로그를 복사합니다. 선택 사항이며, 기본적으로 모든 Pod의 로그를 복사합니다. 여러 번 지정할 수 없습니다. 여러 번 지정하면 마지막 항목이 사용됩니다.
#### `--timeout -t`
명령이 완료될 때까지 대기할 시간(초)입니다. 기본값은 0으로, 무제한입니다.
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
## <a name="azdata-bdc-debug-dump"></a>azdata bdc debug dump
로깅 덤프를 트리거하고 컨테이너에서 복사합니다. 시스템에 kube 구성이 있어야 합니다.
```bash
azdata bdc debug dump --namespace -n 
                      --container -c  
                      [--target-folder -d]
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--namespace -n`
Kubernetes 네임스페이스에 사용되는 빅 데이터 클러스터 이름입니다.
#### `--container -c`
유사한 이름을 가진 컨테이너의 로그를 복사합니다. 선택 사항이며, 기본적으로 모든 컨테이너의 로그를 복사합니다. 여러 번 지정할 수 없습니다. 여러 번 지정하면 마지막 항목이 사용됩니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--target-folder -d`
로그를 복사할 대상 폴더 경로입니다. 선택 사항이며, 기본적으로 로컬 폴더에 결과를 만듭니다.  여러 번 지정할 수 없습니다. 여러 번 지정하면 마지막 항목이 사용됩니다(`./output/dump`).
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

다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요. **Azdata** 도구를 설치 하는 방법에 대 한 자세한 내용은 [install azdata to manage [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] ](deploy-install-azdata.md)항목을 참조 하세요.
