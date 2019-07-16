---
title: SQL Server Profiler 확장
titleSuffix: Azure Data Studio
description: 설치 하 고 Azure Data Studio 용 SQL Server Profiler 확장 (미리 보기) 사용
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 26a448dc27ae2512256ffb1a2929dd8cacc3e31c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959113"
---
# <a name="sql-server-profiler-extension-preview"></a>SQL Server Profiler 확장 (미리 보기)

SQL Server Profiler 확장 (미리 보기) Xevent를 사용 하 여 빌드된 제외 하 고 SQL Server Management Studio (SSMS) Profiler 유사한 간단한 SQL Server 추적 솔루션을 제공 합니다. SQL Server Profiler는 매우 쉽게 사용할 수 있으며 가장 일반적인 추적 구성에 대 한 좋은 기본값. UX는 이벤트를 통해 검색 및 연관 된 TRANSACT-SQL (T-SQL) 텍스트를 보기 위해 최적화 됩니다. Azure Data Studio에 대 한 SQL Server Profiler를 사용 하기 쉬운 사용자 환경을 사용 하 여 T-SQL 실행 작업을 수집 하기 위한 좋은 기본값 가정 이 확장은 현재 미리 보기로 제공에서 됩니다.

**일반적인 SQL Profiler 사용 사례:**

- 문제가 발생한 원인을 찾기 위해 문제 쿼리 실행
- 실행이 느린 쿼리를 찾고 진단
- 문제가 발생 하는 TRANSACT-SQL 문 포착 합니다.
- 워크 로드를 튜닝 하려면 SQL Server의 성능을 모니터링 합니다.
- 문제 진단을 위해 성능 카운터의 상관 관계 지정


## <a name="install-the-sql-server-profiler-extension"></a>SQL Server Profiler 확장 설치

1. 확장 관리자를 열고 사용 가능한 확장에 액세스를 하려면 확장 아이콘을 선택 하거나 선택 **Extensions** 에 **보기** 메뉴.
2. 해당 정보를 보려면 사용 가능한 확장을 선택 합니다.

   ![프로파일러 확장 관리자](media/extensions/sql-server-profiler-extension/profiler-extension.png)

1. 원하는 확장을 선택 하 고 **설치** 것입니다.
2. 선택 **다시 로드** (처음 확장을 설치 하면 필수)에 확장을 사용 하도록 설정 합니다.

## <a name="start-profiler"></a>Profiler를 시작 합니다.

1. Profiler를 시작 하려면 먼저 서버 탭에서 서버에 연결을 확인 합니다.
2. 연결 후, 입력 **Alt + P** Profiler를 시작 합니다.
3. Profiler를 시작 하려면 입력 **Alt + S.** 확장 이벤트를 표시 합니다. 이제 시작할 수 있습니다.
    ![프로파일러 확장 관리자](media/extensions/sql-server-profiler-extension/view-profiler.png)    
1. Profiler를 중지 하려면 입력 **Alt + S.** 이 바로 가기이 키 토글입니다.

## <a name="next-steps"></a>다음 단계

Profiler 및 확장된 이벤트에 대 한 자세한 내용은 참조 하세요 [확장 이벤트](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)합니다.





