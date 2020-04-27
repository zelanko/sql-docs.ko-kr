---
title: '옵션 (텍스트 편집기: 편집기 탭 및 상태 표시줄 페이지) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqleditors.editorcontextsettings
- VS.ToolsOptionsPages.Text_Editor.EditorTabAndStatusBar
ms.assetid: e4815678-7885-4631-878f-c6a2b857ee05
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 01098f2181085f17788429608afb7bdda15fb504
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089238"
---
# <a name="options-text-editor-editor-tab-and-status-bar-page"></a>옵션(텍스트 편집기: 편집기 탭 및 상태 표시줄 페이지)
  **편집기 탭 및 상태 표시줄** 페이지를 사용하여 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 쿼리 편집기에 표시되는 정보를 사용자 지정할 수 있습니다. 쿼리 편집기 창의 탭 및 상태 표시줄에 표시되는 정보의 수준을 지정하고 상태 표시줄을 편집기 창의 위쪽에 표시할지, 아래쪽에 표시할지를 지정할 수 있습니다.  
  
## <a name="option-settings-by-editor"></a>편집기별 옵션 설정  
 편집기 탭 및 상태 표시줄은 모든 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 편집기에서 사용할 수 있지만 기능 수준은 저마다 다릅니다.  
  
 데이터베이스 엔진 쿼리 편집기는 서버 그룹에 연결하므로 서버 그룹에 있는 모든 인스턴스에 대한 연결을 열고 각 연결에서 동일한 쿼리를 동시에 실행할 수 있습니다. 하나의 인스턴스가 아닌 여러 인스턴스에 연결하는 경우 이 대화 상자를 사용하여 상태 표시줄이 각기 다른 색으로 나타나도록 지정할 수 있습니다. 다중 서버 결과 옵션을 변경하려면 [옵션(쿼리 결과/SQL Server/다중 서버)](../../2014/database-engine/options-query-results-sql-server-multi-server.md) 페이지를 사용합니다.  
  
## <a name="status-bar-content"></a>상태 표시줄 내용  
 쿼리 편집기 상태 표시줄에 표시할 정보를 지정합니다.  
  
 **실행 시간 표시**  
 스크립트 실행 시간을 포함합니다. 설정은 다음과 같습니다.  
  
 **없음**  
 상태 표시줄에서 시간 정보를 표시하지 않습니다.  
  
 **종단**  
 상태 표시줄에서 스크립트가 실행 중인 현재 시간을 표시합니다. 스크립트가 완료되면 스크립트가 완료된 시간을 표시합니다.  
  
 **시간**  
 상태 표시줄에서 스크립트가 실행된 기간을 표시합니다. 스크립트가 완료되면 스크립트를 실행하는 데 걸린 시간을 표시합니다.  
  
 **데이터베이스 이름 포함**  
 연결된 현재 데이터베이스의 이름을 포함합니다. 쿼리 편집기를 처음 연 경우 로그인의 기본 데이터베이스입니다. Transact-SQL USE 문을 사용하여 나중에 데이터베이스 컨텍스트를 변경할 수 있습니다.  
  
 **로그인 이름 포함**  
 로그인 이름을 포함합니다.  
  
 **행 개수 포함**  
 현재 실행하고 있는 스크립트에서 처리한 행 수를 포함합니다.  
  
 **서버 이름 포함**  
 서버 이름을 포함합니다. 로컬 연결의 경우 인스턴스 이름입니다. 원격 연결의 경우 원격 컴퓨터 이름 및 인스턴스 이름입니다.  
  
## <a name="status-bar-layout-and-colors"></a>상태 표시줄 레이아웃 및 색  
 쿼리 편집기 상태 표시줄에서 항목의 색을 지정합니다.  
  
 **그룹 연결**  
 쿼리 편집기가 둘 이상의 서버에 연결된 경우 상태 표시줄 색을 설정합니다.  
  
 **단일 서버 연결**  
 쿼리 편집기가 하나의 서버에 연결된 경우 상태 표시줄 색을 설정합니다.  
  
 **상태 표시줄 위치**  
 상태 표시줄 위치를 지정합니다. 설정은 다음과 같습니다.  
  
 **맨 위로**  
 상태 표시줄이 쿼리 편집기 창 위쪽에 표시됩니다.  
  
 **하위별**  
 상태 표시줄이 쿼리 편집기 창 아래쪽에 표시됩니다.  
  
## <a name="tab-text"></a>탭 텍스트  
 쿼리 편집기 창 위쪽에 있는 탭에 표시할 텍스트를 지정합니다. 텍스트가 너무 길어 일부가 표시되지 않은 경우 마우스를 탭으로 이동하면 표시되는 도구 설명에서 전체 문자열을 볼 수 있습니다.  
  
 **데이터베이스 이름 포함**  
 연결된 현재 데이터베이스의 이름을 포함합니다. 쿼리 편집기를 처음 연 경우 로그인의 기본 데이터베이스입니다. Transact-SQL USE 문을 사용하여 나중에 데이터베이스 컨텍스트를 변경할 수 있습니다.  
  
 **파일 이름 포함**  
 스크립트가 저장된 파일의 이름을 포함합니다.  
  
 **폴더 이름 포함**  
 스크립트 파일이 저장된 폴더의 경로를 포함합니다.  
  
 **로그인 이름 포함**  
 로그인 이름을 포함합니다.  
  
 **서버 이름 포함**  
 서버 이름을 포함합니다. 로컬 연결의 경우 인스턴스 이름입니다. 원격 연결의 경우 원격 컴퓨터 이름 및 인스턴스 이름입니다.  
  
## <a name="see-also"></a>참고 항목  
 [옵션 &#40;환경: 글꼴 및 색 페이지&#41;](../ssms/menu-help/options-environment-fonts-and-colors-page.md)   
 [쿼리 편집기에서 코드 색상 지정](../relational-databases/scripting/color-coding-in-query-editors.md)  
  
  
