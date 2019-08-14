---
title: SQL Server Profiler 확장
titleSuffix: Azure Data Studio
description: Azure Data Studio용 SQL Server Profiler 확장(미리 보기) 설치 및 사용
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 26a448dc27ae2512256ffb1a2929dd8cacc3e31c
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959113"
---
# <a name="sql-server-profiler-extension-preview"></a>SQL Server Profiler 확장(미리 보기)

SQL Server Profiler 확장(미리 보기)은 XEvent를 사용하여 빌드된다는 점을 제외하고 SSMS(SQL Server Management Studio) Profiler와 유사하게, 간단한 SQL Server 추적 솔루션을 제공합니다. SQL Server Profiler는 사용하기 쉬우며, 가장 일반적인 추적 구성에 적합한 기본값을 제공합니다. UX는 이벤트를 탐색하고 연결된 T-SQL(Transact-SQL) 텍스트를 보는 데 최적화되어 있습니다. 또한 Azure Data Studio용 SQL Server Profiler는 사용하기 쉬운 UX를 통해 T-SQL 실행 작업을 수집하는 데 적합한 기본값을 가정합니다. 이 확장은 현재 미리 보기로 제공됩니다.

**일반적인 SQL Profiler 사용 사례:**

- 문제가 발생한 원인을 찾기 위해 문제 쿼리 실행
- 실행이 느린 쿼리를 찾고 진단
- 문제가 발생하는 일련의 Transact-SQL 문 포착
- SQL Server의 성능을 모니터링하여 워크로드 튜닝
- 문제 진단을 위해 성능 카운터의 상관 관계 지정


## <a name="install-the-sql-server-profiler-extension"></a>SQL Server Profiler 확장 설치

1. 확장 관리자를 열고 사용 가능한 확장에 액세스하려면 확장 아이콘을 선택하거나 **보기** 메뉴에서 **확장**을 선택합니다.
2. 세부 정보를 보려면 사용 가능한 확장을 선택합니다.

   ![Profiler 확장 관리자](media/extensions/sql-server-profiler-extension/profiler-extension.png)

1. 원하는 확장을 선택하고 **설치**합니다.
2. **다시 로드**를 선택하여 확장을 사용하도록 설정합니다(확장을 처음 설치할 때만 필요).

## <a name="start-profiler"></a>Profiler 시작

1. Profiler를 시작하려면 먼저 서버 탭에서 서버에 연결합니다.
2. 연결한 다음, **Alt+P**를 입력하여 Profiler를 시작합니다.
3. Profiler를 시작하려면 **Alt+S**를 입력합니다. 이제 확장 이벤트를 볼 수 있습니다.
    ![Profiler 확장 관리자](media/extensions/sql-server-profiler-extension/view-profiler.png)    
1. Profiler를 중지하려면 **Alt+S**를 입력합니다. 이 바로 가기 키는 토글입니다.

## <a name="next-steps"></a>다음 단계

Profiler 및 확장 이벤트에 대한 자세한 내용은 [확장 이벤트](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)를 참조하세요.





