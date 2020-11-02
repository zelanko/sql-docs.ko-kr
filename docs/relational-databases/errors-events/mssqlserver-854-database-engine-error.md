---
description: MSSQLSERVER_854
title: MSSQLSERVER_854
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 854 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: f0bf9061b452329280f0625bcc1339469372f4df
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418873"
---
# <a name="mssqlserver_854"></a>MSSQLSERVER_854
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>세부 정보

|attribute|값|
|---|---|
|제품 이름|SQL Server|
|이벤트 ID|854|
|이벤트 원본|MSSQLSERVER|
|구성 요소|SQLEngine|
|심볼 이름|HARDWARE_MEMORY_SCRUBBER|
|메시지 텍스트|머신에서 메모리 오류 복구를 지원합니다. SQL 메모리 보호를 사용하여 메모리 손상을 복구할 수 있습니다.|
||

## <a name="explanation"></a>설명

이 메시지는 운영 체제의 하드웨어에서 메모리 오류 복구 기능을 지원함을 나타냅니다. 최신 하드웨어를 포함하고 Windows Server 2012 이상 버전을 실행하는 컴퓨터에서는 하드웨어가 운영 체제 및 애플리케이션에 메모리 페이지(운영 체제 페이지)가 잘못되었거나 손상된 것으로 표시되었음을 알릴 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 같은 애플리케이션은 다음 API 집합을 사용하여 잘못된 메모리 페이지 알림을 등록할 수 있습니다.

- `GetMemoryErrorHandlingCapabilities`
- `RegisterBadMemoryNotification`
- `BadMemoryCallbackRoutine`

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 이상 버전에서 이 알림 지원을 추가합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 시작하는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 하드웨어에서 이 새로운 기능을 지원하는지 확인합니다. 또한 오류 로그에 다음 메시지가 표시됩니다.

> \<Datetime> 서버 머신에서 메모리 오류 복구를 지원합니다. SQL 메모리 보호를 사용하여 메모리 손상을 복구할 수 있습니다.

## <a name="user-action"></a>사용자 조치

855, 856 등의 다른 오류가 발생하는지 확인하고 적절한 정정 작업을 수행합니다.

## <a name="more-information"></a>자세한 정보

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 추적 플래그 849를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 메모리 오류 알림을 위해 운영 체제에 등록하지 않도록 할 수 있습니다. 그러나 추적 플래그 849를 사용하도록 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 운영 체제에서 잘못된 메모리 알림을 받지 못합니다. 따라서 일반적인 경우에는 이 추적 플래그를 사용하지 않는 것이 좋습니다.
