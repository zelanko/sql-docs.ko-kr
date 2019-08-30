---
title: azdata bdc spark 상태 참조
titleSuffix: SQL Server big data clusters
description: Azdata bdc spark status 명령에 대 한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 96d2bf17e051f45a3041a911cce71c42827768d8
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158068"
---
# <a name="azdata-bdc-spark-status"></a>azdata bdc spark 상태

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

이 문서는 **azdata**에 대 한 참조 문서입니다. 

## <a name="commands"></a>명령
|     |     |
| --- | --- |
[azdata bdc spark 상태 표시](#azdata-bdc-spark-status-show) | Spark 서비스 상태입니다.
## <a name="azdata-bdc-spark-status-show"></a>azdata bdc spark 상태 표시
Spark 서비스 상태입니다.
```bash
azdata bdc spark status show [--resource -r] 
                             [--all -a]
```
### <a name="examples"></a>예
Spark 서비스의 상태를 가져옵니다.
```bash
azdata bdc spark status show
```
모든 인스턴스를 사용 하 여 spark 서비스의 상태를 가져옵니다.
```bash
azdata bdc spark status show --all
```
Spark 서비스 내에서 저장소 리소스의 상태를 가져옵니다.
```bash
azdata bdc spark status show --resource storage-0
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--resource -r`
이 서비스에서이 리소스를 가져옵니다.
#### `--all -a`
서비스 내에서 각 리소스의 모든 인스턴스를 표시 합니다.
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
