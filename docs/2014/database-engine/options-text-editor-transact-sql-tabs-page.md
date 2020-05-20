---
title: 옵션 (텍스트 편집기-Transact-sql-탭 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.Tabs
dev_langs:
- TSQL
ms.assetid: a4499784-67f7-46ef-9f7c-2d0fdd117a52
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 761c84612c207397e33ae96dfcfb088b05bc24b8
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000669"
---
# <a name="options-text-editor---transact-sql---tabs-page"></a>옵션 (텍스트 편집기-Transact-sql-탭 페이지)
  이 대화 상자를 사용하여 [!INCLUDE[ssDE](../includes/ssde-md.md)] 스크립트를 프로그래밍하는 데 사용되는 [!INCLUDE[tsql](../includes/tsql-md.md)] 쿼리 편집기의 탭 이동 동작을 변경할 수 있습니다. 이러한 설정을 표시하려면 **도구** 메뉴에서 **옵션**을 클릭하고 **텍스트 편집기** 폴더와 **Transact-SQL** 하위 폴더를 차례로 확장한 다음 **탭**을 클릭합니다.  
  
## <a name="setting-options-in-multiple-locations"></a>여러 위치에서 옵션 설정  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] 쿼리 편집기에 대한 옵션은 **모든 언어** 대화 상자(탭)에서도 설정할 수 있습니다. **모든 언어** 대화 상자를 사용 하 여 DMX 또는 MDX 편집기 등의 다른 편집기에 대해 다른 옵션을 설정 하는 경우에는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] 이 대화 상자를 사용 하 여 쿼리 편집기 옵션을 다시 설정 해야 합니다.  
  
## <a name="indenting"></a>들여쓰기  
 **없음**  
 이 옵션을 선택하면 Enter 키를 누를 때 생성되는 새 줄을 들여쓰지 않습니다. 커서는 새 줄의 첫 번째 열에 배치됩니다.  
  
 **차단**  
 이 옵션을 선택하면 Enter 키를 누를 때 생성되는 새 줄을 자동으로 앞 줄과 동일하게 들여씁니다.  
  
 **스마트**  
 이 옵션은 사용할 수 없습니다.  
  
## <a name="tabs"></a>탭  
 **탭 크기**  
 탭 정지 간의 거리를 공백 수로 설정합니다. 기본값은 공백 4개입니다.  
  
 **들여쓰기 크기**  
 자동 들여쓰기의 크기를 공백 수로 설정합니다. 기본값은 공백 4개입니다. 탭 문자나 공백 문자 또는 두 가지 문자 모두를 삽입하여 지정한 크기를 채웁니다.  
  
 **공백 삽입**  
 이 옵션을 선택하면 들여쓰기 작업에서 탭 문자 대신 공백 문자만 삽입합니다. 예를 들어 **들여쓰기 크기** 를 5로 설정 하면 TAB 키를 누르거나 주 창에서 도구 모음의 **들여쓰기** 단추를 클릭할 때마다 5 개의 공백 문자가 삽입 됩니다 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] .  
  
 **탭 유지**  
 이 옵션을 선택하면 들여쓰기 작업에서 가능한 한 많은 탭 문자를 삽입합니다. 각 탭 문자는 **탭 크기**에 지정된 공백 수를 채웁니다. **들여쓰기 크기** 가 **탭 크기**의 짝수 배수가 아니면 공백 문자가 추가되어 차이를 메웁니다.  
  
  
