---
description: MSSQLSERVER_832
title: MSSQLSERVER_832
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 832 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 846ce27ff8e7d9560a6d4cc691d1523fddd913fa
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418828"
---
# <a name="mssqlserver_832"></a>MSSQLSERVER_832
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>세부 정보

|attribute|값|
|---|---|
|제품 이름|SQL Server|
|이벤트 ID|832|
|이벤트 원본|MSSQLSERVER|
|구성 요소|SQLEngine|
|심볼 이름|B_CONSTPAGECHANGED|
|메시지 텍스트|고정 페이지가 변경되었습니다(필요한 체크섬: \<expected value>, 실제 체크섬: \<actual value>, 데이터베이스 \<dbid>, 파일 \'<filename>’, 페이지 \<pageno>). 이는 일반적으로 메모리 오류 또는 기타 하드웨어나 OS 손상을 나타냅니다.|
||

## <a name="explanation"></a>설명

외부 요소 때문에 데이터베이스 페이지를 변경하는 데 사용되는 일반 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 엔진 코드 외부에서 데이터베이스 페이지가 수정되었습니다.  조건은 다음과 같을 수 있습니다.  

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에서 실행되는 스레드가 데이터베이스 페이지에 잘못된 쓰기를 실행합니다. 이 동작을 흔히 “스크리블러”라고 합니다.
- 하드웨어, 운영 체제 또는 메모리 관련 문제로 인해 데이터베이스 페이지가 잘못 수정되었거나 손상되었습니다.  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 동작을 감지하면 오류 832가 발생합니다.

## <a name="user-action"></a>사용자 조치

오류의 원인을 찾으려면 다음 옵션을 고려합니다.

- 메모리, CPU 또는 기타 하드웨어 관련 문제가 있는지 확인하려면 일반적인 하드웨어 또는 시스템 검사를 실행해야 합니다. 모든 시스템 드라이버, 운영 체제 업데이트, 하드웨어 업데이트가 시스템에 적용되었는지 확인합니다. 메모리 관련 테스트를 포함하여 하드웨어 제조업체 진단을 실행하는 것이 좋습니다.
- 확장 저장 프로시저, COM 개체 또는 데이터베이스 페이지에 예약된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리를 잘못 수정할 수 있는 기타 DLL을 포함하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드되어 이 문제를 일으킬 수 있는 “외부” DLL을 평가합니다.  

이 오류가 표시될 때마다 오류 메시지에서 \<dbid>가 참조하는 데이터베이스에 대해 `DBCC CHECKDB`를 즉시 실행하는 것이 좋습니다.

## <a name="more-information"></a>자세한 정보

이 오류는 흔히 LazyWriter라고 하는 백그라운드 작업에서 탐지됩니다. 이 작업의 “명령”은 LAZY WRITER로 표시됩니다. 따라서 이 오류는 클라이언트 애플리케이션에 반환되지 않습니다. 이 오류는 Windows 애플리케이션 이벤트 로그에 EventID=832로 기록됩니다.  

현재 캐시에서 수정되지 않은(또는 “더티”가 아닌) 페이지만 검사됩니다. 메시지에서 “고정”이라는 용어를 사용하는 이유는 디스크에서 읽어온 이후 페이지가 변경된 적이 없기 때문입니다. 또한 페이지에 체크섬 값이 있고 체크섬 오류(메시지 824)가 발생하지 않았기 때문에 디스크에서 “클린” 페이지를 읽어왔습니다. 그러나 이 오류가 발생한 후에 페이지가 수정되어 잘못된 수정 내용으로 디스크에 기록되었을 수 있습니다. 이 오류가 발생하면 디스크에 기록되기 전에 모든 수정 내용을 기준으로 새 체크섬이 계산됩니다. 따라서 디스크의 페이지가 손상되었더라도 이후에 디스크에서 읽어올 때는 체크섬 오류가 트리거되지 않을 수 있습니다. 이 오류가 참조하는 모든 데이터베이스에서 `DBCC CHECKDB`를 실행하는 것이 중요합니다.  

디스크에 기록된 후에는 `DBCC CHECKDB`도 이 상태의 페이지에 대해 오류를 보고하지 않을 수 있습니다. 잘못된 수정이 데이터를 저장하지 않거나 중요한 페이지 또는 행 구조 정보를 포함하지 않는 페이지 위치에 있거나 CHECKDB에서 감지할 수 없는 데이터 수정일 수 있기 때문입니다.  

[2장, SQL Server I/O 기본 사항](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)) 백서에서도 메시지 832에 대한 자세한 내용을 확인할 수 있습니다.
