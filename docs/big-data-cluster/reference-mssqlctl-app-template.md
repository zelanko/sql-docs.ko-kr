---
title: mssqlctl 앱 템플릿 참조
titleSuffix: SQL Server big data clusters
description: Mssqlctl 앱 템플릿 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c67ed74750ac36d1a5c79503417414a9dd8ab6b5
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860104"
---
# <a name="mssqlctl-app-template"></a>mssqlctl 앱 템플릿

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

다음 문서에 대 한 참조를 제공 합니다 **앱 템플릿** 명령에 **mssqlctl** 도구입니다. 다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다.

## <a id="commands"></a> 명령

|||
|---|---|
| [목록](#list) | 지원 되는 템플릿을 가져옵니다. |
| [pull](#pull) | 지원 되는 템플릿을 다운로드 합니다. |

## <a id="list"></a> mssqlctl 앱 템플릿 목록

지원 되는 템플릿을 가져옵니다.

```
mssqlctl app template list
   --url
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--url -u** | 다른 템플릿 저장소 위치를 지정 합니다. 기본값: https://github.com/Microsoft/sql-server-samples.git합니다. |

### <a name="examples"></a>예

기본 템플릿 저장소 위치에서 모든 템플릿을 가져옵니다.

```
mssqlctl app template list
```

다른 저장소 위치에서 모든 템플릿을 가져옵니다.

```
mssqlctl app template list --url https://github.com/diffrent/templates.git
```

## <a id="pull"></a> mssqlctl 앱 템플릿 끌어오기

지원 되는 템플릿을 다운로드 합니다.

```
mssqlctl app template pull
   --destination
   --name
   --url
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--destination -d** | 응용 프로그램 기본 서식 파일을 배치할 위치입니다.  기본값:. / 템플릿. |
| **--name -n** | 템플릿 이름입니다. 전체 목록은 지원 되는 템플릿 이름 해제 실행 `mssqlctl app template list`합니다. |
| **--url -u** | 다른 템플릿 저장소 위치를 지정 합니다. 기본값:
https://github.com/Microsoft/sql-server-samples.git에서 분할된 테이블 또는 인덱스를 만들 수 있습니다. |

### <a name="examples"></a>예

기본 템플릿 저장소 위치에서 모든 템플릿을 다운로드 합니다.

```
mssqlctl app template pull
```

다른 저장소 위치에서 모든 템플릿을 다운로드 합니다.

```
mssqlctl app template list --url https://github.com/diffrent/templates.git
```

이름으로 개별 템플릿을 다운로드 합니다.

```
mssqlctl app template pull --name ssis
```

## <a name="next-steps"></a>다음 단계

다른 방법에 대 한 자세한 내용은 **mssqlctl** 명령 참조 [mssqlctl 참조](reference-mssqlctl.md)합니다. 설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.