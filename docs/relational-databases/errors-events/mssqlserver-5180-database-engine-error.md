---
description: MSSQLSERVER_5180
title: MSSQLSERVER_5180
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5180 (Database Engine error)
ms.assetid: ''
author: rgward
ms.author: ramakoni
ms.openlocfilehash: cbdc30c1e05d50bb20df3f9e3ebf54097c770743
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418825"
---
# <a name="mssqlserver_5180"></a>MSSQLSERVER_5180
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>세부 정보

|attribute|값|
|---|---|
|제품 이름|SQL Server|
|이벤트 ID|5180|
|이벤트 원본|MSSQLSERVER|
|구성 요소|SQLEngine|
|심볼 이름|DSK_BAD_FCB_FILEID|
|메시지 텍스트|데이터베이스 '%.*ls'의 파일 ID %d이(가) 잘못되어 FCB(File Control Bank)를 열 수 없습니다. 파일 위치를 확인하고 DBCC CHECKDB를 실행합니다.|
||

## <a name="explanation"></a>설명

[!INCLUDE[ssDENoVersion](../../includes/ssdenoversion_md.md)]에서 잘못된 파일 ID를 참조할 경우 오류 5180이 발생하여 쿼리 또는 작업이 실패할 수 있습니다. 예를 들면 다음과 같습니다.

> 메시지 5180, 수준 22, 상태 1, 줄 1  
데이터베이스 '%.*ls'의 파일 ID %d이(가) 잘못되어 FCB(File Control Bank)를 열 수 없습니다. 파일 위치를 확인하고 DBCC CHECKDB를 실행합니다.

오류가 심각도 22로 발생했으므로 사용자 세션 연결이 끊어집니다. 이 오류 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그 및 Windows 애플리케이션 이벤트 로그에 EventID = 5180으로 기록됩니다.

## <a name="possible-causes"></a>가능한 원인

[!INCLUDE[ssDENoVersion](../../includes/ssdenoversion-md.md)]은 다양한 상황에서 대체로 페이지 ID를 참조할 때 파일 ID를 참조하게 됩니다. 파일 ID가 페이지 ID의 첫 번째 부분이기 때문입니다. 어떤 이유로든 참조되는 파일 ID가 0 미만이거나 데이터베이스의 유효한 파일 ID가 아닌 경우(sys.database_files와 같은 시스템 카탈로그 뷰에 나열된 유효한 파일 ID 기준) 5180 오류가 발생할 수 있습니다.

한 가지 가능한 원인은 저장된 파일 ID가 잘못되었기 때문입니다. 행에 전달된 레코드가 다른 페이지를 참조하기 때문에 해당 페이지에 액세스하고 파일 ID가 잘못된 경우 5180 오류가 발생할 수 있습니다. 이 조건은 전달된 레코드가 있는 페이지의 데이터베이스 손상 오류입니다. 예제에서는 `DBCC CHECKDB`에서 메시지 8993을 보고합니다.

또 다른 예는 다음 또는 이전 페이지 ID로 페이지 머리글에 저장된 페이지 ID에 잘못된 파일 ID가 포함된 경우입니다. 이 필드는 클러스터형 인덱스 등에서 일련의 페이지를 연결하는 데 사용됩니다. 이전 또는 다음 페이지의 파일 ID가 잘못된 경우 엔진에서 해당 ID를 참조하여 다음 또는 이전 페이지로 이동해야 할 때 5180 오류가 발생할 수 있습니다. 예제에서는 `DBCC CHECKDB`에서 메시지 8981을 보고합니다.

저장된 페이지 ID가 손상되어 잘못된 파일 ID가 포함된 것이 문제의 원인이 아닌 경우에는 [!INCLUDE[ssDENoVersion](../../includes/ssdenoversion-md.md)] 내의 문제일 수 있습니다.

## <a name="user-action"></a>사용자 조치

이 오류가 발생할 경우 오류 메시지에 나열된 데이터베이스에 대해 `DBCC CHECKDB`를 실행해야 합니다. 오류를 발견하면 알려진 정상 백업에서 복원해야 합니다. 백업에서 복원할 수 없는 경우 출력의 권장 사항에 따라 `DBCC CHECKDB`의 복구 옵션을 사용할 수 있습니다. 대부분의 경우 이 유형의 오류를 복구하면 데이터 손실이 발생합니다. CHECKDB 사용 방법 및 데이터베이스 손상 문제의 원인에 대한 자세한 내용은 다음 문서를 참조하세요. [DBCC CHECKDB에서 보고된 데이터베이스 일관성 오류 문제를 해결하는 방법](https://support.microsoft.com/kb/2015748)

`DBCC CHECKDB`에서 오류를 보고하지 않고 문제가 계속 발생하면 Microsoft 기술 지원 팀에 도움을 요청해야 합니다. 5180 오류가 발생하는 쿼리를 제공할 수 있도록 준비합니다. 오류가 발생한 쿼리를 확인하는 방법에 대한 자세한 내용은 [추가 정보](#more-information) 섹션을 참조하세요.

## <a name="more-information"></a>자세한 정보

FCB(파일 제어 블록)는 데이터베이스와 관련된 파일에 대한 중요한 정보를 추적하는 내부 메모리 구조입니다. 파일 ID는 데이터베이스의 FCB를 고유하게 식별하는 데 사용됩니다. 서버 엔진이 잘못된 파일 ID를 참조하는 경우 FCB 구조를 찾을 수 없어 5180 오류 조건이 트리거됩니다.

이 오류가 발생한 쿼리를 확인하려면 다음 방법을 사용합니다.

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 이상 버전에서 system_health 세션에 쿼리 텍스트를 포함하는 오류 레코드가 있는지 확인합니다. system_health 세션에 대한 자세한 내용은 다음 리소스를 참조하세요. [SQL Server 2008 지원: system_health 세션](https://techcommunity.microsoft.com/t5/sql-server-support/supporting-sql-server-2008-the-system-health-session/ba-p/315509)
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler를 사용하여 `SQL:BatchStarting`, `RPC:Starting`, 예외 이벤트를 캡처합니다. 예외 이벤트와 관련된 세션에서 5180 예외 이벤트 앞에 오는 쿼리를 찾습니다.
