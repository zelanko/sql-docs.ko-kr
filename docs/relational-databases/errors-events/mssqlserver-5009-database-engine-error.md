---
description: MSSQLSERVER_5009
title: MSSQLSERVER_5009
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5009 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 1ca7fb52969d9ec08d8c80c48ec1325277a13fa7
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418833"
---
# <a name="mssqlserver_5009"></a>MSSQLSERVER_5009
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>세부 정보

|attribute|값|
|---|---|
|제품 이름|SQL Server|
|이벤트 ID|5009|
|이벤트 원본|MSSQLSERVER|
|구성 요소|SQLEngine|
|심볼 이름|ALT_BADDISKS|
|메시지 텍스트|문에 나열된 하나 이상의 파일을 찾을 수 없거나 초기화할 수 없습니다.|
||

## <a name="explanation"></a>설명

이 오류는 확인할 수 없는 파일 이름 또는 fileID를 ALTER DATABASE 또는 DBCC SHRINK* 명령에 지정했음을 나타냅니다.

다음 스키마를 살펴보세요.

- 전체 또는 대량 로그된 복구 모델을 사용하는 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스가 있습니다.
- 데이터베이스에 *db_file1* 이라는 새 데이터 파일을 추가합니다.
- `db_file1` 파일의 파일 형식을 데이터로 설정합니다.
- 파일 형식을 잘못 지정했음을 알게 됩니다.
- `db_file1` 파일을 제거하고 이 데이터베이스의 트랜잭션 로그를 백업합니다.
- 동일한 데이터베이스에 *db_file1* 이라는 새 로그 파일을 추가합니다.
- ALTER DATABASE 문을 사용하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio를 사용하여 *db_file1* 로그 파일을 제거하도록 지정합니다.

이 시나리오에서는 다음과 같은 오류 메시지가 표시됩니다.

> 메시지 5009, 수준 16, 상태 9, 줄 1. 문에 나열된 하나 이상의 파일을 찾을 수 없거나 초기화할 수 없습니다.

## <a name="possible-causes"></a>가능한 원인

이 문제는 제거할 파일의 논리적 이름이 시스템 카탈로그 테이블에서 고유하지 않은 경우에 발생합니다. 예를 들어 이전에 데이터베이스에 있었던 파일이 제거된 경우 이 문제가 발생합니다.

같은 논리적 이름을 가진 파일을 제거하도록 지정할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 삭제된 논리적 파일을 제거하려고 하며 오류 메시지가 표시됩니다.

## <a name="user-action"></a>사용자 조치

이 문제를 해결하려면 아래 단계를 수행합니다.

> [!NOTE]
> 이 단계를 수행하면 파일 ID 값이 재사용됩니다.

1. 같은 데이터 형식의 새 논리적 파일을 다른 이름으로 만들려면 ALTER DATABASE 문을 사용합니다. 예를 들어 다음 예제와 같이 논리적 파일 이름을 `db_file1`이 아니라 `different_remove_file_name`으로 지정합니다.

    ```sql
    ALTER DATABASE [DBNAME] ADD FILE ( NAME = N'different_remove_file_name',
    FILENAME = N'D:\MSSQL.1\MSSQL\DATA\db_file1.ndf', SIZE = 1MB, MAXSIZE = 1MB)
    ```

    > [!NOTE]
    > 모든 파일 이름이나 파일 경로를 사용할 수 있습니다.

1. 다음 예제와 같이 ALTER DATABASE 문을 사용하여 1단계에서 만든 논리적 파일을 제거합니다.

    ```sql
    ALTER DATABASE [DBNAME] REMOVE FILE [different_remove_file_name]
    ```

1. 데이터베이스의 트랜잭션 로그 백업을 만듭니다.
1. *db_file1* 이라는 논리적 파일을 다시 제거해 봅니다.
