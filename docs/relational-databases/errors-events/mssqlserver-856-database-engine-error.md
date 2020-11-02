---
description: MSSQLSERVER_856
title: MSSQLSERVER_856
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 856 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: f94f6f4e8f8eebee48bbb0c2a6d0faefa4218c25
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418863"
---
# <a name="mssqlserver_856"></a>MSSQLSERVER_856
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>세부 정보

|attribute|값|
|---|---|
|제품 이름|SQL Server|
|이벤트 ID|856|
|이벤트 원본|MSSQLSERVER|
|구성 요소|SQLEngine|
|심볼 이름|BAD_MEMORY_CLEAN_DATABASE_PAGE|
|메시지 텍스트|SQL Server가 ‘%ls’ 데이터베이스, 파일 ID %u, 페이지 ID %u, 메모리 주소 0x% I64x에서 하드웨어 메모리 손상을 탐지하고 페이지를 복구했습니다.|
||

## <a name="explanation"></a>설명

이 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 버퍼 풀 외부에 캐시된 개체에서 잘못된 메모리 페이지를 탐지했음을 나타냅니다. 메모리 오류 복구 기능을 지원하는 시스템에서 메시지가 발생합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 수정되지 않은 손상된 메모리 페이지를 삭제하여 관련 메모리 오류를 수정하고 이 오류 메시지를 로그합니다. 손상된 메모리 페이지가 수정(더티)된 경우에는 오류 824가 발생합니다([MSSQLSERVER_824](mssqlserver-824-database-engine-error.md)).

## <a name="user-action"></a>사용자 조치

하드웨어 또는 시스템 검사를 실행하여 메모리 또는 CPU 관련 문제가 있는지 확인해야 합니다. 모든 시스템 드라이버, 운영 체제 업데이트, 하드웨어 업데이트가 시스템에 적용되었는지 확인합니다. 메모리 관련 테스트를 포함하여 하드웨어 제조업체 진단을 실행하는 것이 좋습니다. 이 오류가 표시될 때마다 이 인스턴스의 모든 데이터베이스에 대해 `DBCC CHECKDB`를 실행하는 것이 좋습니다.

## <a name="more-information"></a>자세한 정보

최신 하드웨어를 포함하고 Windows Server 2012 이상 버전을 실행하는 컴퓨터에서는 하드웨어가 운영 체제 및 애플리케이션에 메모리 페이지(운영 체제 페이지)가 잘못되었거나 손상된 것으로 표시되었음을 알릴 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 같은 애플리케이션은 다음 API 집합을 사용하여 잘못된 메모리 페이지 알림을 등록할 수 있습니다.

- `GetMemoryErrorHandlingCapabilities`
- `RegisterBadMemoryNotification`
- `BadMemoryCallbackRoutine`

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 버전에서 이 알림 지원을 추가합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 시작하는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 하드웨어에서 이 새로운 기능을 지원하는지 확인합니다. 또한 오류 로그에 다음 메시지가 표시됩니다.

> \<Datetime> 서버 머신에서 메모리 오류 복구를 지원합니다. SQL 메모리 보호를 사용하여 메모리 손상을 복구할 수 있습니다.

현재, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 알림을 받은 경우에만 버퍼 풀에서 작업을 수행합니다. 알림을 받은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 전체 버퍼 풀을 반복하여 할당된 각 버퍼의 주소를 검색해야 합니다. 그런 다음, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 `QueryWorkingSetEX` API를 사용하여 데이터 페이지를 지원하는 메모리 페이지가 잘못된 것으로 표시되었는지 확인합니다. 손상된 것으로 보고된 멤버가 있을 경우 이 메모리 페이지에 해당하는 `PSAPI_WORKING_SET_EX_BLOCK` 출력 구조에서 잘못된 멤버는 1로 설정됩니다.

해당 버퍼 풀 또는 데이터 페이지가 현재 변경되지 않았거나 I/O를 처리하고 있지 않은 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터 페이지를 삭제하고 커밋을 취소할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 다음 메시지를 로그합니다.

> SQL Server가 ‘%ls’ 데이터베이스, 파일 ID %u, 페이지 ID %u, 메모리 주소 0x% I64x에서 하드웨어 메모리 손상을 탐지하고 페이지를 복구했습니다.

해당 데이터 페이지가 쿼리에 다시 필요한 경우 버퍼 풀은 디스크에서 데이터 페이지를 다시 읽고 콘텐츠를 버퍼 풀로 가져올 수 있습니다. 디스크에 있는 페이지 버전이 손상된 상태일 수도 있습니다. 이 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류 824와 같은 추가 오류를 로그할 수 있습니다.

버퍼 풀은 잘못된 페이지를 사용하지 않지만 캐시된 다른 개체 또는 구조에서 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 다음 메시지를 로그합니다.

> 수정할 수 없는 하드웨어 메모리 손상이 탐지되었습니다. 시스템이 불안정해질 수 있습니다. 자세한 내용은 Windows 이벤트 로그를 확인하세요.

서버에서 메모리 오류를 보고하는 경우 컴퓨터 하드웨어 공급업체에 문의하여 메모리 진단 수행, BIOS 및 펌웨어 업데이트, 잘못된 메모리 모듈 교체 등의 적절한 작업을 수행해야 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 추적 플래그 849를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 메모리 오류 알림을 위해 운영 체제에 등록하지 않도록 할 수 있습니다. 그러나 추적 플래그 849를 사용하도록 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 운영 체제에서 잘못된 메모리 알림을 받지 못합니다. 따라서 일반적인 경우에는 이 추적 플래그를 사용하지 않는 것이 좋습니다.

기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 지원되는 하드웨어에서 관련 알림을 받습니다.

또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 메모리 오류 알림을 위해 등록하는 경우에는 지연 기록기 시스템 프로세스에서 고정 페이지 검사를 수행하지 않습니다. 고정 페이지 검사에 대한 자세한 내용은 [SQL Server에서 메시지 832(고정 페이지 변경) 문제를 해결하는 방법](https://support.microsoft.com/help/2015759)을 참조하세요.
