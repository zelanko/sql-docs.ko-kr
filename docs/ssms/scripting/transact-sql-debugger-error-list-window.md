---
title: 오류 목록 창(Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- error list window
- SQL Server Management Studio [SQL Server], error list window
ms.assetid: fae6327d-e268-44ae-a474-4a8f8f843129
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dcf0886a58e1e735e95ed0383313769f4796bd24
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68253628"
---
# <a name="transact-sql-debugger---error-list-window"></a>Transact-SQL 디버거 - 오류 목록 창
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **오류 목록** 은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기의 IntelliSense 코드에서 생성된 구문 및 의미 체계 오류를 표시합니다.  
  
## <a name="features-of-the-error-list"></a>오류 목록의 기능  
 **오류 목록** 은 다음 기능을 제공합니다.  
  
-   스크립트를 편집할 때 **오류 목록** 은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기의 IntelliSense에 의해 생성되는 오류 및 경고를 표시합니다.  
  
-   오류 메시지 항목을 두 번 클릭하여 오류를 생성한 스크립트 파일의 탭에 포커스를 두고 오류 위치로 이동할 수 있습니다.  
  
-   표시되는 항목 및 각 항목에 대해 표시되는 정보 열을 필터링할 수 있습니다.  
  
-   오류를 수정하면 해당 오류 항목이 **오류 목록**에서 제거됩니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일 탭을 닫으면 해당 파일에 대한 오류가 **오류 목록**에서 제거됩니다.  
  
## <a name="working-with-the-error-list"></a>오류 목록 작업  
 **오류 목록**을 표시하려면 다음 중 하나를 수행합니다.  
  
-   **보기** 메뉴에서 **오류 목록**을 클릭합니다.  
  
-   Ctrl+\\, Ctrl+E 바로 가기 키를 누릅니다.  
  
 **오류 목록**을 연 후에는 다음 동작을 수행하여 보기를 사용자 지정할 수 있습니다.  
  
-   목록을 정렬하려면 열 머리글을 클릭합니다. 추가 열을 기준으로 다시 정렬하려면 Shift 키를 누른 상태에서 다른 열 머리글을 클릭합니다.  
  
-   표시할 열과 숨길 열을 선택하려면 바로 가기 메뉴에서 **열 표시** 를 선택합니다.  
  
-   열이 표시되는 순서를 변경하려면 열 머리글을 왼쪽이나 오른쪽으로 끕니다.  
  
 **오류 목록** 은 특정 오류에 대한 추가 정보로 연결되지 않습니다.  
  
## <a name="transact-sql-errors-in-management-studio"></a>Management Studio의 Transact-SQL 오류  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트에 대한 오류를 다음 위치에 표시합니다.  
  
-   **오류 목록** 에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 편집기의 IntelliSense에서 발견한 모든 구문 및 의미 체계 오류가 포함됩니다. 이 오류 목록은 사용자가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 편집할 때 동적으로 업데이트됩니다. 목록에는 편집기가 각 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트에서 발견한 모든 오류가 포함됩니다. 편집기는 스크립트에서 오류를 발견해도 파일의 구문 분석을 중지하지 않습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 편집기의 IntelliSense는 일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문 요소를 지원하지 않습니다. **오류 목록** 에는 IntelliSense에서 지원하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문의 오류만 포함됩니다.  
  
-   **쿼리 편집기 창의 아래쪽에 있는** 메시지 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 탭에는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 스크립트가 실행될 때 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 반환하는 모든 오류 및 메시지가 표시됩니다. 이 목록은 스크립트를 다시 실행하기 전에는 변경되지 않습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 한 개 또는 두 개의 컴파일 오류를 발견한 경우 일괄 처리 구문 분석을 중지하므로 **메시지** 탭에 포함되지 않는 스크립트 오류가 있을 수 있습니다.  
  
 두 위치 모두에 오류가 나열되는 경우도 있습니다. 예를 들어 스크립트 파일에 **오류 목록**에 나열된 구문 오류가 포함될 수 있습니다. 이 오류를 수정하기 전에 스크립트를 실행하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 파서가 동일한 조건을 검색하고 **메시지** 탭에 똑같은 오류 메시지를 반환할 수 있습니다.  
  
> [!NOTE]  
>  **오류 목록** 에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기의 오류만 표시되며 MDX, DMX 또는 XML/A 편집기의 오류는 표시되지 않습니다. 모든 MDX, DMX 및 XML/A 오류는 해당 편집기의 **메시지** 탭에 표시됩니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **오류 목록** 을 열면 다음 열에 정보가 표시됩니다.  
  
 **기본 순서**  
 항목이 생성된 순서를 나타내는 정수를 표시합니다.  
  
 **설명**  
 오류 항목의 텍스트를 표시합니다. 설명이 길어지면 다음 줄로 줄 바꿈됩니다.  
  
 **파일**  
 오류를 생성한 스크립트 파일의 이름을 표시합니다.  
  
 **선**  
 오류가 포함된 코드 줄을 나타내는 정수를 표시합니다.  
  
 **열**  
 코드 줄에서 오류의 위치를 나타내는 정수를 표시합니다.  
  
 **프로젝트**  
 스크립트 파일이 포함된 프로젝트의 이름을 표시합니다.  
