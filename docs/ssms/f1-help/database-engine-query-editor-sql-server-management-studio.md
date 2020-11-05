---
title: SSMS 쿼리 편집기
description: SSMS(SQL Server Management Studio) 쿼리 편집기
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.query.advanced.f1
- sql13.swb.query.ansi.f1
- sql13.swb.query.general.f1
- sql13.swb.query.grid.f1
- sql13.swb.sqleditors.multiserverresultssettings
- sql13.swb.tsqlquery.f1
- sql13.swb.tsqlresults.f1
dev_langs:
- TSQL
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], editor
- SQL Server Management Studio [SQL Server], Database Engine Query Editor
- SQL Server Management Studio [SQL Server], templates
- SQL Server Management Studio [SQL Server], query editor
- Query Editor [SQL Server Management Studio]
- Query Editor [Database Engine]
- Query Editor [Database Engine], Features
- Query Editor [Database Engine], Toolbar
- Query Editor [SQL Server Management Studio], full screen mode
- Query Editor [Database Engine], templates
- Query Editor [SQL Server Management Studio], about Query Editor
- Transact-SQL Editor See Query Editor [Database Engine]
- Database Engine Query Editor See Query Editor [Database Engine]
- Code Editor [SQL Server Management Studio], about Query Editor
- editors [SQL Server Management Studio], Database Engine Query Editor
- full screen mode [SQL Server Management Studio]
- writing scripts
- modifying scripts
- writing queries
- scripts [SQL Server], SQL Server Management Studio
- queries [SQL Server], SQL Server Management Studio
ms.assetid: 05cfae9b-96d5-4a35-a098-0bc3a548bcfc
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019, contperfq1
ms.date: 08/28/2020
ms.openlocfilehash: 7450a77549d05dab5a024b39be6d2b4aef6c09de
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364854"
---
# <a name="sql-server-management-studio-ssms-query-editor"></a>SSMS(SQL Server Management Studio) 쿼리 편집기

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

이 문서에서는 SSMS(SQL Server Management Studio)의 쿼리 편집기 기능에 대해 설명합니다.

> [!Note]
> T-SQL(Transact-SQL) F1 도움말을 사용하는 방법에 대한 자세한 내용은 [Transact-SQL F1 도움말](#transact-sql-f1-help) 섹션을 참조하세요.
>
> 편집기를 사용하여 수행할 수 있는 작업에 대해 알아보려면 [편집기 작업](#editor-tasks) 섹션을 참조하세요.

SSMS의 편집기는 일반적인 아키텍처를 공유합니다. 텍스트 편집기는 기본 수준의 기능을 구현하며 텍스트 파일의 기본 편집기로 사용될 수 있습니다. 다른 편집기, 즉 쿼리 편집기는 SQL Server에서 지원되는 언어 중 하나의 구문을 정의하는 언어 서비스를 포함하여 이 기능 베이스를 확장합니다. 또한 쿼리 편집기는 IntelliSense 및 디버깅 같은 편집기 기능을 다양한 수준으로 지원합니다. 쿼리 편집기에는 T-SQL 및 XQuery 문을 포함하는 스크립트를 작성하는 데 사용되는 데이터베이스 엔진 쿼리 편집기, MDX 언어용 MDX 편집기, DMX 언어용 DMX 편집기 및 XML for Analysis 언어용 XML/A 편집기가 포함됩니다.
쿼리 편집기를 사용하여 Transact-SQL 문을 포함하는 스크립트를 만들고 실행할 수 있습니다.

![새 쿼리](media/database-engine-query-editor-sql-server-management-studio/new-query.png)

## <a name="sql-editor-toolbar"></a>SQL 편집기 도구 모음

쿼리 편집기가 열려 있으면 다음 단추를 포함하는 SQL 편집기 도구 모음이 표시됩니다.

**보기** 메뉴를 선택하고 **도구 모음** 을 선택한 다음 **SQL 편집기** 를 선택하여 SQL 편집기 도구 모음을 추가할 수도 있습니다. 쿼리 편집기 창이 열려 있지 않을 때 SQL 편집기 도구 모음을 추가하면 모든 단추를 사용할 수 없습니다.

![편집기 도구 모음](media/database-engine-query-editor-sql-server-management-studio/editor-toolbar.png)

### <a name="connect-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 연결

**[서버에 연결](connect-to-server-database-engine.md)** 대화 상자를 엽니다. 이 대화 상자를 사용하여 서버에 연결합니다.

[상황에 맞는 메뉴](#connection-using-the-context-menu)를 사용하여 데이터베이스에 연결할 수도 있습니다.

### <a name="change-connection-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 연결 변경

**서버에 연결** 대화 상자를 엽니다. 이 대화 상자를 사용하여 [다른 서버에 연결](f1-help-for-server-connections-sql-server-management-studio.md)합니다.

[상황에 맞는 메뉴](#connection-using-the-context-menu)를 사용하여 연결을 변경할 수도 있습니다.

### <a name="available-databases-using-the-editor-toolbar"></a>편집기 도구 모음으로 사용 가능한 데이터베이스

같은 서버의 다른 데이터베이스로 연결을 변경합니다.

### <a name="execute-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 실행

선택한 코드를 실행하거나, 코드를 선택하지 않은 경우 모든 쿼리 편집기 코드를 실행합니다.

F5 키를 선택하거나 [상황에 맞는 메뉴](#execute-using-the-context-menu)에서 쿼리를 **실행** 할 수도 있습니다.

### <a name="cancel-executing-query-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 쿼리 실행 취소

취소 요청을 서버로 보냅니다. 일부 쿼리는 바로 취소할 수 없으며 적절한 취소 조건이 될 때까지 기다려야 합니다. 트랜잭션을 취소해도 트랜잭션이 롤백되는 동안 작업이 지연될 수 있습니다.

Alt + Break를 선택하여 쿼리 실행을 취소할 수도 있습니다.

### <a name="parse-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 구문 분석

선택한 코드의 구문을 검사합니다. 코드를 선택하지 않은 경우 쿼리 편집기 창에 있는 모든 코드의 구문을 검사합니다.

Ctrl + F5를 선택하여 쿼리 편집기의 코드를 확인할 수도 있습니다.

### <a name="display-estimated-execution-plan-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 예상 실행 계획 표시

쿼리를 실행하지 않고 쿼리 프로세서에서 쿼리 실행 계획을 요청한 다음 **실행 계획** 창에 계획을 표시합니다. 이 계획은 인덱스 통계를 사용하여 쿼리 실행의 각 부분에서 반환될 것으로 예상되는 행 수를 계산합니다. 실제 사용되는 쿼리 계획은 예상 실행 계획과 다를 수 있습니다. 반환되는 행 수가 예상치와 크게 달라 쿼리 프로세서가 계획을 더 효율적으로 변경할 경우 이러한 차이가 발생할 수 있습니다.

Ctrl + L을 선택하거나 [상황에 맞는 메뉴](#display-estimated-execution-plan-using-the-context-menu)에서 예상 실행 계획을 표시할 수도 있습니다.

### <a name="query-options-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 쿼리 옵션 구성

**쿼리 옵션** 대화 상자를 엽니다. 이 대화 상자를 사용하여 쿼리 실행 및 쿼리 결과에 대한 기본 옵션을 구성합니다.

[상황에 맞는 메뉴](#query-options-using-the-context-menu)에서 **쿼리 옵션** 을 선택할 수도 있습니다.

### <a name="intellisense-enabled-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 IntelliSense 사용 설정

데이터베이스 엔진 쿼리 편집기에서 [IntelliSense](../scripting/configure-intellisense-sql-server-management-studio.md) 기능을 사용할지를 지정합니다. 이 옵션은 기본적으로 설정되어 있습니다.

Ctrl+B, Ctrl+I를 차례로 선택하거나 [상황에 맞는 메뉴](#intellisense-enabled-using-the-context-menu)에서 **IntelliSense 사용** 을 선택할 수도 있습니다.

### <a name="include-actual-execution-plan-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 실제 실행 계획 포함

쿼리를 실행하고, 쿼리 결과를 반환하고, 쿼리 실행 계획을 사용합니다. 쿼리는 **실행 계획** 창에 그래픽 쿼리 계획으로 표시됩니다.

Ctrl + M을 선택하거나 [상황에 맞는 메뉴](#include-actual-execution-plan-using-the-context-menu)에서 **실제 실행 계획 포함** 을 선택할 수도 있습니다.

### <a name="include-live-query-statistics-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 활성 쿼리 통계 포함

제어권이 한 쿼리 계획 연산자에서 다른 연산자로 흘러갈 때 쿼리 실행 프로세스를 실시간으로 파악할 수 있습니다.

[상황에 맞는 메뉴](#include-live-query-statistics-using-the-context-menu)에서 **활성 쿼리 통계 포함** 을 선택할 수도 있습니다.

### <a name="include-client-statistics-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 클라이언트 통계 포함

쿼리 통계와 네트워크 패킷 통계 및 쿼리 경과 시간이 표시된 **클라이언트 통계** 창을 포함합니다.

Shift + Alt + S를 선택하거나 [상황에 맞는 메뉴](#include-client-statistics-using-the-context-menu)에서 **활성 쿼리 통계 포함** 을 선택할 수 있습니다.

### <a name="results-to-text-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 텍스트로 결과 표시

쿼리 결과를 텍스트로 **결과** 창에 반환합니다.

Ctrl + T를 선택하거나 [상황에 맞는 메뉴](#results-using-the-context-menu)에서 결과를 반환할 수도 있습니다.

### <a name="results-to-grid-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 표 형태로 결과 표시

쿼리 결과를 하나 이상의 표로 **결과** 창에 반환합니다. 이 옵션은 기본적으로 사용됩니다.

Ctrl + D를 선택하거나 [상황에 맞는 메뉴](#results-using-the-context-menu)에서 결과를 반환할 수도 있습니다.

### <a name="results-to-file-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 파일로 결과 저장

쿼리를 실행하면 **결과 저장** 대화 상자가 열립니다. **저장 위치** 에서 파일을 저장할 폴더를 선택합니다. **파일 이름** 에 파일 이름을 입력하고 **저장** 을 선택하여 쿼리 결과를 확장명이 .rpt인 **보고서** 파일로 저장합니다. 고급 옵션을 보려면 **저장** 단추의 아래쪽 화살표를 선택한 다음 **인코딩하여 저장** 을 선택합니다.

Ctrl + Shift + F를 선택하거나 [상황에 맞는 메뉴](#results-using-the-context-menu)에서 결과를 텍스트로 반환할 수도 있습니다.

### <a name="comment-out-the-selected-lines-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 선택된 줄을 주석으로 처리

줄의 시작 부분에 주석 기호(--)를 추가하여 현재 줄을 주석으로 처리합니다.

Ctrl+K, Ctrl+C를 차례로 선택하여 줄을 주석으로 처리할 수도 있습니다.

### <a name="uncomment-the-selected-lines-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 선택된 줄의 주석 처리 제거

줄의 시작 부분에서 주석 기호(--)를 제거하여 현재 줄을 활성 소스 코드 문으로 처리합니다.

Ctrl+K, Ctrl+U를 차례로 선택하여 줄의 주석 처리를 제거할 수도 있습니다.

### <a name="decrease-indent-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 내어쓰기

줄의 시작 부분에서 공백을 제거하여 해당 줄의 텍스트를 왼쪽으로 이동합니다.

### <a name="increase-line-indent-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 줄 들여쓰기

줄의 시작 부분에 공백을 추가하여 해당 줄의 텍스트를 오른쪽으로 이동합니다.

### <a name="specify-values-for-template-parameters-using-the-editor-toolbar"></a>편집기 도구 모음을 사용하여 템플릿 매개 변수 값 지정

저장 프로시저 및 함수의 매개 변수 값을 지정하는 데 사용할 수 있는 대화 상자를 엽니다.

## <a name="context-menu"></a>상황에 맞는 메뉴

쿼리 편집기의 아무 곳이나 *마우스 오른쪽 단추로 클릭* 하여 상황에 맞는 메뉴에 액세스할 수 있습니다. 상황에 맞는 메뉴의 옵션은 SQL 편집기 도구 모음과 비슷합니다. 상황에 맞는 메뉴를 사용하여 **연결** 및 **실행** 과 같은 옵션을 볼 수 있지만 **코드 조각 삽입** 및 **코드 감싸기** 와 같은 다른 옵션도 나열됩니다.

![옵션](media/database-engine-query-editor-sql-server-management-studio/context-menu.png)

### <a name="insert-snippet-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 코드 조각 삽입

[T-SQL 코드 조각](../scripting/add-transact-sql-snippets.md)은 쿼리 편집기에서 새 Transact-SQL 문을 작성할 때 시작점으로 사용할 수 있는 템플릿입니다.

### <a name="surround-with-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 코드 감싸기

코드 감싸기 조각은 일련의 Transact-SQL 문을 BEGIN, IF 또는 WHILE 블록으로 묶을 때 시작점으로 사용할 수 있는 템플릿입니다.

### <a name="connection-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 연결

![Connections](media/database-engine-query-editor-sql-server-management-studio/context-menu-connections.png)

SSMS의 도구 모음 옵션에 비해 상황에 맞는 메뉴에 더 많은 **연결** 옵션이 있습니다.

- **연결** - 서버에 연결 대화 상자를 엽니다. 이 대화 상자를 사용하여 서버에 연결합니다.

- **연결 끊기** - 현재 쿼리 편집기와 서버 간의 연결을 끊습니다.

- **모든 쿼리 연결 끊기** - 모든 쿼리 연결을 끊습니다.

- **연결 변경** - 서버에 연결 대화 상자를 엽니다. 이 대화 상자를 사용하여 다른 서버에 연결합니다.

### <a name="open-server-in-object-explorer-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 개체 탐색기에서 서버 열기

개체 탐색기는 각 SQL Server 인스턴스에서 개체를 보고 관리하는 계층적 사용자 인터페이스를 제공합니다. 개체 탐색기 정보 창은 인스턴스 개체의 테이블 형식 뷰와 특정 개체를 검색하는 기능을 제공합니다. 개체 탐색기의 기능은 서버의 유형에 따라 조금씩 다르지만 일반적으로 데이터베이스를 위한 개발 기능과 모든 서버 유형을 위한 관리 기능을 포함합니다.

### <a name="execute-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 실행

선택한 코드를 실행하거나, 코드를 선택하지 않은 경우 쿼리 편집기에 있는 모든 코드를 실행합니다.

### <a name="display-estimated-execution-plan-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 예상 실행 계획 표시

쿼리를 실제로 실행하지 않고 쿼리 프로세서에서 쿼리 실행 계획을 요청한 다음 **실행 계획** 창에 계획을 표시합니다. 이 계획은 인덱스 통계를 사용하여 쿼리 실행의 각 부분에서 반환될 것으로 예상되는 행 수를 계산합니다. 실제 사용되는 쿼리 계획은 예상 실행 계획과 다를 수 있습니다. 반환되는 행 수가 예상치와 달라 쿼리 프로세서가 계획을 더 효율적으로 변경할 경우 이러한 차이가 발생할 수 있습니다.

### <a name="intellisense-enabled-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 IntelliSense 사용 설정

데이터베이스 엔진 쿼리 편집기에서 IntelliSense 기능을 사용할지를 지정합니다. 이 옵션은 기본적으로 설정되어 있습니다.

### <a name="trace-query-in-sql-server-profiler-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 SQL Server Profiler에서 쿼리 추적

SQL Server Profiler는 추적을 작성 및 관리하고 추적 결과를 분석 및 재생하기 위한 인터페이스입니다. 이벤트는 추적 파일에 저장되며 이 파일은 나중에 분석되거나 문제를 진단할 때 특정 단계를 다시 수행하기 위해 사용할 수 있습니다.

### <a name="analyze-query-in-database-engine-tuning-advisor-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 데이터베이스 엔진 튜닝 관리자에서 쿼리 분석

Microsoft DTA(데이터베이스 엔진 튜닝 관리자)는 데이터베이스를 분석하여 쿼리 성능을 최적화하는 데 활용할 수 있는 권장 사항을 제공합니다. 데이터베이스 구조나 SQL Server의 내부 구조를 전문적으로 이해하지 못해도 데이터베이스 엔진 튜닝 관리자를 사용하여 인덱스, 인덱싱된 뷰 또는 테이블 파티션의 최적 집합을 선택 및 작성할 수 있습니다. DTA를 사용하여 다음과 같은 태스크를 수행할 수 있습니다.

### <a name="design-query-in-editor-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 편집기에서 쿼리 디자인

쿼리 및 뷰 디자이너는 뷰의 정의를 열거나, 쿼리 또는 뷰의 결과를 표시하거나, 쿼리를 만들거나 열 때 나타납니다.

### <a name="include-actual-execution-plan-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 실제 실행 계획 포함

쿼리를 실행하고, 쿼리 결과를 반환하고, 쿼리 실행 계획을 사용합니다. 쿼리는 **실행 계획** 창에 그래픽 쿼리 계획으로 표시됩니다.

### <a name="include-live-query-statistics-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 활성 쿼리 통계 포함

제어권이 한 쿼리 계획 연산자에서 다른 연산자로 흘러갈 때 쿼리 실행 프로세스를 실시간으로 파악할 수 있습니다.

### <a name="include-client-statistics-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 클라이언트 통계 포함

쿼리 통계와 네트워크 패킷 통계 및 쿼리 경과 시간이 표시된 **클라이언트 통계** 창을 포함합니다.

### <a name="results-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 결과 생성

![결과 옵션](media/database-engine-query-editor-sql-server-management-studio/context-menu-results.png)

상황에 맞는 메뉴에서 원하는 *결과* 옵션을 선택할 수 있습니다.

- **텍스트로 결과 표시** - **결과** 창에 쿼리 결과를 텍스트로 표시합니다.

- **표 형태로 결과 표시** - **결과** 창에 쿼리 결과를 하나 이상의 표로 표시합니다.

- **파일로 결과 저장** - 쿼리를 실행하면 **결과 저장** 대화 상자가 열립니다. **저장 위치** 에서 파일을 저장할 폴더를 선택합니다. **파일 이름** 에 파일 이름을 입력하고 **저장** 을 선택하여 쿼리 결과를 **보고서** 파일(확장명 .rpt)로 저장합니다. 고급 옵션을 보려면 **저장** 단추의 아래쪽 화살표를 선택한 다음 **인코딩하여 저장** 을 선택합니다.

### <a name="properties-window-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하는 속성 창

[속성 창](../menu-help/properties-window-f1-help-management-studio.md)은 연결 또는 실행 계획 연산자와 같은 SQL Server Management Studio 내 항목의 상태와 테이블, 뷰, 디자이너와 같은 데이터베이스 개체에 대한 정보를 설명합니다.

현재 연결의 속성을 보려면 속성 창을 사용합니다. 대부분의 속성은 속성 창에서 읽기 전용이지만 Management Studio의 다른 위치에서 변경할 수 있습니다. 예를 들어 쿼리의 데이터베이스 속성은 속성 창에서 읽기 전용이지만 도구 모음에서 변경할 수 있습니다.

### <a name="query-options-using-the-context-menu"></a>상황에 맞는 메뉴를 사용하여 쿼리 옵션 구성

**쿼리 옵션** 대화 상자를 엽니다. 이 대화 상자를 사용하여 쿼리 실행 및 쿼리 결과에 대한 기본 옵션을 구성합니다.

## <a name="transact-sql-f1-help"></a>Transact-SQL F1 도움말

쿼리 편집기에서 F1 키를 선택하면 특정 Transact-SQL 문에 대한 참조 항목을 연결할 수 있습니다. 이렇게 하려면 Transact-SQL 문의 이름을 강조 표시하고 F1 키를 선택합니다. 그러면 도움말 검색 엔진에서 강조 표시된 문자열과 일치하는 F1 도움말 특성을 가진 항목을 검색합니다.

도움말 검색 엔진에서 강조 표시된 문자열과 정확히 일치하는 F1 도움말 키워드를 포함하는 항목을 찾을 수 없을 경우 이 항목이 표시됩니다. 이 경우 다음과 같은 두 가지 방법으로 원하는 도움말을 찾을 수 있습니다.

- 편집기에서 선택한 문자열을 복사한 다음 SQL Server 온라인 설명서의 검색 탭에 붙여 넣고 검색을 수행합니다.

- 항목에 적용되는 F 도움말 키워드와 일치할 것으로 예상되는 Transact-SQL 문 부분만 선택한 다음 F1 키를 다시 누릅니다. 그러면 검색 엔진에서 강조 표시된 문자열과 항목에 할당된 F1 도움말 키워드를 정확하게 일치시킵니다. 강조 표시된 문자열에 열이나 매개 변수 이름과 같이 사용자 환경 고유의 요소가 포함되어 있을 경우 검색 엔진에서 일치하는 항목을 찾을 수 없습니다. 선택할 수 있는 문자열의 예는 다음과 같습니다.

  - SELECT, CREATE DATABASE, BEGIN TRANSACTION 등의 Transact-SQL 문 이름

  - SERVERPROPERTY, @@VERSION 등의 기본 제공 함수 이름

  - sys.data_spaces, sp_tableoption 등의 시스템 저장 프로시저 테이블 또는 뷰 이름

## <a name="editor-tasks"></a>편집기 태스크

| 태스크 설명 | 항목 |
|------------------|-------|
| SSMS에서 편집기를 여는 다양한 방법에 대해 설명합니다.| [편집기 열기](../scripting/open-an-editor-sql-server-management-studio.md) |
| 줄 번호 매기기 및 IntelliSense 옵션과 같은 다양한 편집기 옵션을 구성합니다. | [편집기 구성](../scripting/configure-editors-sql-server-management-studio.md) |
| 자동 줄 바꿈, 창 분할, 탭 등과 같은 뷰 모드를 관리하는 방법입니다.| [편집기 및 보기 모드 관리](../scripting/manage-the-editor-and-view-mode.md) |
| 숨겨진 텍스트 또는 들여쓰기 같은 서식 옵션을 설정합니다. | [코드 서식 관리](../scripting/manage-code-formatting.md) |
| 증분 검색, 이동 등과 같은 기능을 사용하여 편집기 창에서 편집기를 탐색합니다. | [코드 및 텍스트 이동](../scripting/navigate-code-and-text.md) |
| 복잡한 문을 쉽게 읽을 수 있도록 다양한 구문에 대한 색 구분 옵션을 설정합니다. | [쿼리 편집기에서 코드 색상 지정](../scripting/color-coding-in-query-editors.md) |
| 텍스트를 스크립트의 한 위치에서 다른 위치로 끌어서 놓습니다.| [텍스트 끌어다 놓기](../scripting/drag-and-drop-text.md) |
| 코드의 중요 한 부분을 더 쉽게 찾기 위해 책갈피를 설정하는 방법입니다. | [책갈피 관리](../scripting/manage-bookmarks.md) |
| 창 또는 표에서 스크립트 또는 결과를 인쇄하는 방법입니다.| [코드 및 결과 인쇄](../scripting/print-code-and-results.md) |
| MDX 쿼리 편집기에서 기본 기능을 보거나 사용합니다. | [Analysis Services 스크립트 만들기](/analysis-services/instances/create-analysis-services-scripts-in-management-studio) |
| DMX 쿼리 편집기에서 기본 기능을 보거나 사용합니다. | [DMX 쿼리 만들기](/analysis-services/data-mining/create-a-dmx-query-in-sql-server-management-studio) |
| XML/A 쿼리 편집기에서 기본 기능을 보거나 사용합니다. | [XML 편집기](../scripting/xml-editor-sql-server-management-studio.md) |
| 데이터베이스 엔진 쿼리 편집기에서 sqlcmd 기능을 사용하는 방법입니다.| [SQLCMD 스크립트 편집](../scripting/edit-sqlcmd-scripts-with-query-editor.md) |
| 데이터베이스 엔진 쿼리 편집기에서 코드 조각을 사용하는 방법입니다. 코드 조각은 일반적으로 사용되는 문 또는 블록에 대한 템플릿이며, 사이트별 코드 조각을 포함하도록 사용자 지정하거나 확장할 수 있습니다.| [T-SQL 코드 조각](../scripting/add-transact-sql-snippets.md) |
| Transact\-SQL 디버거를 사용하여 코드를 단계별로 처리하고 변수 및 매개 변수 값과 같은 디버깅 정보를 보는 방법입니다.| [T-SQL 디버거](../scripting/transact-sql-debugger.md) |

## <a name="see-also"></a>참고 항목

- [메뉴 및 바로 가기 키 사용자 지정](../customize-menus-and-shortcut-keys.md)
- [SQL Server Management Studio 바로 가기 키](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)