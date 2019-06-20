---
title: 옵션 (쿼리 실행-SQL Server-일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionGeneral
ms.assetid: 3f8d59bc-3f97-4e5d-8b86-5ac670d20780
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 83c0d1ad4d63d361754c5e2183081c30c7c51f2b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089988"
---
# <a name="options-query-execution-sql-server-general-page"></a>옵션 (쿼리 실행-SQL Server-일반 페이지)
  이 페이지를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리를 실행하는 옵션을 지정할 수 있습니다. 이러한 옵션의 변경 사항은 새로운 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리에만 적용됩니다. 현재 쿼리에 대한 옵션을 변경하려면 **쿼리** 메뉴에서 **쿼리 옵션** 을 클릭하거나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 창에서 마우스 오른쪽 단추를 클릭한 다음 **쿼리 옵션**을 선택합니다.  
  
## <a name="options"></a>변수  
 **SET ROWCOUNT**  
 기본값 0은 모든 결과를 받을 때까지 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 결과를 기다린다는 것을 나타냅니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 지정한 행 수를 받은 후 쿼리를 중단하려면 0보다 큰 값을 지정합니다. 모든 행이 반환될 수 있도록 이 옵션을 해제하려면 SET ROWCOUNT 0을 지정합니다.  
  
 **SET TEXTSIZE**  
 기본값인 2,147,483,647바이트는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 `text` 및 `ntext` 데이터 필드의 상한에 이르는 전체 데이터 필드를 제공한다는 것을 나타냅니다. 값이 클 경우 결과를 제한하려면 보다 작은 수를 지정합니다. 지정한 수보다 많은 열은 잘립니다.  
  
 **실행 제한 시간**  
 **새 연결** 대화 상자에서 기본값을 설정합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 쿼리를 취소하기 전에 대기할 시간을 초 단위로 지정하려면 이 스핀 상자를 사용합니다. 값 0은 무한 대기 또는 제한 시간 없음을 의미합니다. 새로 설치하는 경우 이 값은 0입니다.  
  
 **일괄 처리 구분 기호**  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 일괄 처리로 구분하는 데 사용할 단어를 입력합니다. 기본값은 GO입니다.  
  
 **기본적으로 SQLCMD 모드로 새 쿼리를 엽니다.**  
 SQLCMD 모드로 새 쿼리를 열려면 이 확인란을 선택합니다. SQLCMD 모드에 대한 자세한 내용은 [쿼리 편집기로 SQLCMD 스크립트 편집](../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)을 참조하세요.  
  
 이 옵션을 선택할 경우 다음과 같은 제한 사항에 유의해야 합니다.  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)] 쿼리 편집기에서 IntelliSense는 해제되어 있습니다.  
  
-   쿼리 편집기를 명령줄에서 실행하지 못하므로 변수와 같은 명령줄 매개 변수를 전달할 수 없습니다.  
  
-   쿼리 편집기는 운영 체제 프롬프트에 응답할 수 없으므로 대화형 문을 실행하지 않도록 주의해야 합니다.  
  
 **기본값으로 다시 설정**  
 이 페이지의 모든 값을 원래 기본값으로 다시 설정하려면 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sqlcmd Utility](../tools/sqlcmd-utility.md)  
  
  
