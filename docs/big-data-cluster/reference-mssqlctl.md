---
title: mssqlctl 참조
titleSuffix: SQL Server 2019 big data clusters
description: Mssqlctl 명령에 대 한 참조 문서입니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: be1ece46bd171370a91273c832bf89a0bf426cd3
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018369"
---
# <a name="mssqlctl"></a>mssqlctl

다음 문서에 대 한 참조를 제공 합니다 **mssqlctl** SQL Server 2019 빅 데이터 클러스터 (미리 보기)에 대 한 도구입니다.

## <a id="commands"></a> 명령

|||
|---|---|
| [app](reference-mssqlctl-app.md) | 만들기, 삭제, 실행 및 응용 프로그램을 관리 합니다. |
| [cluster](reference-mssqlctl-cluster.md) | 선택 하 고, 관리 및 클러스터 작동 합니다. |
| [login](#login) | 클러스터에 로그인 합니다. |
| [logout](#logout) | 로그 아웃 클러스터 합니다. |
| [storage](reference-mssqlctl-storage.md) | 클러스터 저장소를 관리 합니다. |

## <a id="login"></a> mssqlctl 로그인

클러스터에 로그인 합니다.

```
mssqlctl login
   --endpoint
   --password
   --username
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
|**--endpoint -e**| 호스트 및 포트 (예:)을 클러스터 `http://host:port"`합니다. |
|**--password -p**| 암호 자격 증명입니다. |
|**--username -u**| 사용자 계정입니다. |

### <a name="examples"></a>예

대화형으로 로그인 합니다.

```
mssqlctl login
```

사용자 이름 및 암호로 로그인 합니다.

```
mssqlctl login -u johndoe@contoso.com -p VerySecret
```

사용자 이름, 암호 및 클러스터 끝점으로 로그인 합니다.

```
mssqlctl login -u johndoe@contoso.com -p VerySecret --endpoint https://host.com:12800
```

## <a id="logout"></a> mssqlctl logout

로그 아웃 클러스터 합니다.

```
mssqlctl logout
   --username
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
|---|---|
| **--username -u** | 계정 사용자의 경우 누락 된 경우 현재 활성 계정을 로그 아웃 합니다. |

### <a name="examples"></a>예

이 사용자를 로그 아웃이 있습니다.

```
mssqlctl logout --username admin
```

## <a name="next-steps"></a>다음 단계

설치 하는 방법에 대 한 자세한 합니다 **mssqlctl** 도구를 참조 하십시오 [SQL Server 2019 빅 데이터 클러스터를 관리 하는 mssqlctl 설치](deploy-install-mssqlctl.md)합니다.