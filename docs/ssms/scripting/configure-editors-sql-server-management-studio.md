---
title: 편집기 구성(SQL Server Management Studio)
description: 옵션 대화 상자에서 옵션을 설정하여 SQL Server Management Studio 편집기의 작업을 사용자 지정하는 방법을 알아봅니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: e7c7a8ef-f561-4258-a7b6-c445dba69f87
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6da583c30bae7c58c463a9518545f36274e19ce6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476914"
---
# <a name="configure-editors-sql-server-management-studio"></a>편집기 구성(SQL Server Management Studio)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

각 편집기에 대한 옵션을 구성하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 편집기 작업을 사용자 지정할 수 있습니다.  
  
## <a name="setting-editor-options"></a>편집기 옵션 설정  
 대부분의 편집기 옵션은 **도구** 메뉴에서 **옵션...** 을 선택하여 표시되는 **옵션** 대화 상자에서 설정합니다. **옵션** 대화 상자의 왼쪽 창에서 **텍스트 편집기** 노드를 열어서 코드 및 텍스트 편집 옵션을 설정합니다. 텍스트 편집기 아래의 노드가 특정 편집기에 적용됩니다.  
  
1.  **모든 언어** – 이 노드를 사용하여 설정한 옵션이 모든 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 편집기에 적용됩니다. 다른 노드를 통해 특정 편집기에 대한 다른 옵션을 설정하여 이러한 설정을 무시할 수 있습니다.  
  
2.  **일반 텍스트** – 이 노드를 사용하여 설정한 옵션은 MDX, DMX 및 텍스트 편집기에 적용됩니다.  
  
3.  **Transact-SQL** - 이 노드를 사용하여 설정한 옵션은 데이터베이스 엔진 쿼리 편집기에 적용됩니다.  
  
4.  **XML** – 이 노드를 사용하여 설정한 옵션은 XML for Analysis 편집기에 적용됩니다.  
  
 **쿼리 실행** 또는 **쿼리 결과** 노드를 열어서 쿼리 실행과 결과 표시 방법을 사용자 지정할 수 있습니다.  
  
## <a name="editor-configuration-tasks"></a>편집기 구성 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|Windows 탐색기에서 지정된 확장명을 가진 파일을 두 번 클릭하여 편집기를 열도록 지정하는 방법에 대해 설명합니다.|[파일 확장명을 코드 편집기에 연결](./associate-file-extensions-to-a-code-editor.md)|  
|코드와 텍스트를 더 쉽게 읽을 수 있도록 글꼴을 사용자 지정하는 방법에 대해 설명합니다.|[글꼴 색상, 크기 및 스타일 변경](./change-font-color-size-and-style.md)|  
|속성을 보는 방법에 대해 설명합니다.|[Management Studio에서 속성 창 사용](./use-the-properties-window-in-management-studio.md)|  
|편집기 옵션 대화 상자의 F1 도움말 페이지 위치|[쿼리 옵션 페이지 F1 도움말](../f1-help/f1-help-for-server-connections-sql-server-management-studio.md)|