---
title: mssqlctl 앱 참조
titleSuffix: SQL Server 2019 big data clusters
description: Mssqlctl 앱 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fa2b43c352fbab39cd00112b9646a87a2b752f5b
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527256"
---
# <a name="mssqlctl-app"></a>mssqlctl 앱

다음 문서에 대 한 참조를 제공 합니다 **앱** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a id="commands"></a> 명령

|||
|---|---|
| [create](#create) | 응용 프로그램을 만듭니다. |
| [delete](#delete) | 응용 프로그램을 삭제 합니다. |
| [describe](#describe) | 응용 프로그램에 설명 합니다. |
| [init](#init) | Kickstart 새 응용 프로그램 구조입니다. |
| [list](#list) | 응용 프로그램을 나열 합니다. |
| [run](#run) | 응용 프로그램을 실행 합니다. |
| [update](#update) | 응용 프로그램을 업데이트 합니다. |
| [template](reference-mssqlctl-app-template.md) | 템플릿 명령입니다. |

## <a id="create"></a> mssqlctl 앱 만들기

응용 프로그램을 만듭니다.

```
mssqlctl app create
   --assets
   --code
   --description
   --entrypoint
   --inputs
   --name
   --outputs
   --runtime
   --spec
   --version
   --yes
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--assets -a** | 목록에 포함 되도록 추가 응용 프로그램 파일 자산입니다. |
| **--code -c** | R 또는 Python 코드 파일 경로입니다. |
| **--description -d** | 응용 프로그램에 대한 설명입니다. |
| **--entrypoint** |  |
| **--inputs** | 입력된 매개 변수 스키마입니다. |
| **--name -n** | 애플리케이션 이름. |
| **--outputs** | 출력 매개 변수 스키마입니다. |
| **--runtime -r** | 응용 프로그램 런타임입니다.  허용 되는 값: Mleap, Python, R, SSIS |
| **--spec -s** | 응용 프로그램을 설명 하는 YAML 사양 파일을 사용 하 여 디렉터리 경로입니다. |
| **--version -v** | 응용 프로그램 버전입니다. |
| **-예-y** | CWD의 spec.yaml 파일에서 응용 프로그램을 만들 때 확인 표시 되지 않습니다. |

### <a name="examples"></a>예

Spec.yaml (권장)를 통해 새 응용 프로그램을 만듭니다.

```
mssqlctl app create --spec /path/to/dir/with/spec/yaml
```

인수를 사용 하 여 새 Python 앱 인라인을 만듭니다.

```
mssqlctl app create --name add --version v1 --inputs x=float, y=float --outputs result=float --runtime Python --code add.py  --init init.py
```

인수를 사용 하 여 새 R 응용 프로그램 인라인을 만듭니다.

```
mssqlctl app create --name add --version v1 --inputs x=numeric, y=numeric --outputs result=numeric --runtime R --code add.R  --init init.R
```

포함 되도록 추가 파일 자산을 사용 하 여 새 R 응용 프로그램 인라인을 만듭니다.

```
mssqlctl app create --name add --version v1 --runtime R --code  add.R --assets file.RData,/path/to/more/files
```

## <a id="delete"></a> mssqlctl 앱 삭제

응용 프로그램을 삭제 합니다.

```
mssqlctl app delete
   --name
   --version
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--name -n** | 애플리케이션 이름. |
| **--version -v** | 응용 프로그램 버전입니다. |

### <a name="examples"></a>예

이름 및 버전에 따라 응용 프로그램을 삭제 합니다.

```
mssqlctl app delete --name reduce --version v1
```

## <a id="describe"></a> mssqlctl 앱 설명

응용 프로그램에 설명 합니다.

```
mssqlctl app describe
   --name
   --spec
   --version
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--name -n** | 애플리케이션 이름. |
| **--spec -s** | 응용 프로그램을 설명 하는 YAML 사양 파일을 사용 하 여 디렉터리 경로입니다. |
| **--version -v** | 응용 프로그램 버전입니다. |

### <a name="examples"></a>예

응용 프로그램에 설명 합니다.

```
mssqlctl app describe --name reduce --version v1
```

## <a id="init"></a> mssqlctl 앱 초기화

Kickstart 새 응용 프로그램 구조입니다.

```
mssqlctl app init
   --destination
   --name
   --spec
   --template
   --url
   --version
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--destination -d** | 응용 프로그램 구조를 배치할 위치입니다. 기본값: 현재 작업 디렉터리입니다. |
| **--name -n** | 애플리케이션 이름. |
| **--spec -s** | 응용 프로그램 spec.yaml만 생성 합니다. |
| **--template -t** | 템플릿 이름입니다. 전체 목록은 지원 되는 템플릿 이름 해제 실행 `mssqlctl app template list`합니다. |
| **--url -u** | 다른 템플릿 저장소 위치를 지정 합니다. 기본값: https://github.com/Microsoft/sql-server-samples.git합니다. |
| **--version -v** | 응용 프로그램 버전입니다. |

### <a name="examples"></a>예

새 응용 프로그램을 스 캐 폴드 `spec.yaml` 만 합니다.

```
mssqlctl app init --spec
```

에 따라 새 R 응용 프로그램 응용 프로그램 구조를 스 캐 폴드는 `r` 템플릿.

```
mssqlctl app init --name reduce --template r
```

기반으로 하는 새 Python 응용 프로그램 응용 프로그램 구조를 스 캐 폴드는 `python` 템플릿.

```
mssqlctl app init --name reduce --template python
```

에 따라 새 SSIS 응용 프로그램 응용 프로그램 구조를 스 캐 폴드는 `ssis` 템플릿.

```
mssqlctl app init --name reduce --template ssis
```

## <a id="list"></a> mssqlctl 앱 목록

응용 프로그램을 나열 합니다.

```
mssqlctl app list
   --name
   --version
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--name -n** | 애플리케이션 이름. |
| **--version -v** | 응용 프로그램 버전입니다. |

### <a name="examples"></a>예

응용 프로그램 이름과 버전을 나열 합니다.

```
mssqlctl app list --name reduce  --version v1
```

이름으로 모든 응용 프로그램 버전을 나열 합니다.

```
mssqlctl app list --name reduce
```

모든 응용 프로그램을 나열 합니다.

```
mssqlctl app list
```

## <a id="run"></a> mssqlctl 앱 실행

응용 프로그램을 실행 합니다.

```
mssqlctl app run
   --name
   --version
   --inputs
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--name -n** | 애플리케이션 이름. |
| **--version -v** | 응용 프로그램 버전입니다. |
| **--inputs** | 응용 프로그램 입력 매개 변수를 CSV에 `name=value` 형식입니다. |

### <a name="examples"></a>예

입력 매개 변수 없이 응용 프로그램을 실행 합니다.

```
mssqlctl app run --name reduce --version v1
```

1 입력된 매개 변수를 사용 하 여 응용 프로그램을 실행 합니다.

```
mssqlctl app run --name reduce --version v1 --inputs x=10
```

여러 입력된 매개 변수를 사용 하 여 응용 프로그램을 실행 합니다.

```
mssqlctl app run --name reduce --version v1 --inputs x=10,y5.6
```

## <a id="update"></a> mssqlctl 앱 업데이트

응용 프로그램을 업데이트 합니다.

```
mssqlctl app update
   --spec
   --yes
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--spec -s** | 응용 프로그램을 설명 하는 YAML 사양 파일을 사용 하 여 디렉터리 경로입니다. |
| **-예-y** | CWD의 spec.yaml 파일에서 응용 프로그램을 업데이트 하는 경우 확인 표시 되지 않습니다. |

## <a name="next-steps"></a>다음 단계

다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다. 설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.