---
title: Azure 데이터 Studio SQL Server 에이전트 확장 | Microsoft Docs
description: Azure Data Studio 용 SQL Server 에이전트 확장 (미리 보기)
ms.custom: tools|sos
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 1ad136bb5bda8534d722b3b89d6731db5b704cb6
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356214"
---
# <a name="sql-server-agent-extension-preview"></a>SQL Server 에이전트 확장 (미리 보기)

SQL Server 에이전트 확장 (미리 보기)는 관리 및 SQL 에이전트 작업 및 구성 문제 해결에 대 한 확장이입니다. 이 확장은 현재 미리 보기로 제공에서 됩니다.

키 작업은 다음과 같습니다.
- SQL Server에 구성 하는 목록 SQL Server 에이전트 작업
- 작업 실행 결과 사용 하 여 작업 기록 보기
- 작업을 시작 및 중지 하는 기본적인 작업 제어

## <a name="install-the-sql-server-agent-extension"></a>SQL Server 에이전트 확장 설치

1. 확장 관리자를 열고 사용 가능한 확장에 액세스를 하려면 확장 아이콘을 선택 하거나 선택 **Extensions** 에 **보기** 메뉴.
2. 세부 정보를 보려면 사용 가능한 확장을 선택 합니다.

   ![에이전트 설치](media/extensions/sql-server-agent-extension/install-sql-agent.png)

1. 원하는 확장을 선택 하 고 **설치** 것입니다.
2. 선택 **다시 로드** (처음 확장을 설치 하면 필수)에 확장을 사용 하도록 설정 합니다.
1. 서버 또는 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 관리 대시보드로 이동 **관리**합니다.
2. 설치 된 확장 관리 대시보드에서 탭으로 나타납니다.

   ![에이전트 보기](media/extensions/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>작업 보기

SQL Server 에이전트 확장은에 연결할 때 가장 먼저 표시은 목록에 모든 에이전트 작업입니다.

   ![작업 보기](media/extensions/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>다음 단계

SQL Server 에이전트에 자세히 알아보려면 [설명서를 확인 합니다.](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent?view=sql-server-2017)


