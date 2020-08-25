---
title: SQL Server 에이전트 확장
description: SQL 에이전트 작업 및 구성을 관리하기 위한 확장인 Azure Data Studio용 SQL Server 에이전트 확장(미리 보기)을 설치하고 사용하는 방법을 알아봅니다.
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 207388fed1ea2465fb965457640b5e1fb0d162cf
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766162"
---
# <a name="sql-server-agent-extension-preview"></a>SQL Server 에이전트 확장(미리 보기)

SQL Server 에이전트 확장(미리 보기)은 SQL 에이전트 작업 및 구성을 관리하고 문제를 해결하기 위한 확장입니다. 이 확장은 현재 미리 보기로 제공됩니다.

주요 작업은 다음과 같습니다.
- SQL Server에 구성된 SQL Server 에이전트 작업 나열
- 작업 실행 결과가 있는 작업 기록 보기
- 작업을 시작 및 중지하는 기본 작업 컨트롤

## <a name="install-the-sql-server-agent-extension"></a>SQL Server 에이전트 확장 설치

1. 확장 관리자를 열고 사용 가능한 확장에 액세스하려면 확장 아이콘을 선택하거나 **보기** 메뉴에서 **확장**을 선택합니다.
2. 세부 정보를 보려면 사용 가능한 확장을 선택합니다.

   ![에이전트 설치](media/extensions/sql-server-agent-extension/install-sql-agent.png)

1. 원하는 확장을 선택하고 **설치**합니다.
2. **다시 로드**를 선택하여 확장을 사용하도록 설정합니다(확장을 처음 설치할 때만 필요).
1. 서버 또는 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **관리**를 선택하여 관리 대시보드로 이동합니다.
2. 설치된 확장은 관리 대시보드에 탭으로 표시됩니다.

   ![에이전트 보기](media/extensions/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>작업 보기

SQL Server 에이전트 확장에 연결하면 모든 에이전트 작업 목록이 가장 먼저 표시됩니다.

   ![작업 보기](media/extensions/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>다음 단계

SQL Server 에이전트에 대해 자세히 알아보려면 [설명서를 참조하세요.](../ssms/agent/sql-server-agent.md?view=sql-server-2017)