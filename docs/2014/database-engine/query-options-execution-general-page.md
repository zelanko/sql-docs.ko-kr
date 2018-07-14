---
title: 쿼리 옵션 실행 (일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.general.f1
ms.assetid: 858a0263-2f04-4692-b8bf-63e93c998ead
caps.latest.revision: 29
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: a6e8e45ea1ba74aeef1f063ad03154a9574bc9e5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37269809"
---
# <a name="query-options-execution-general-page"></a>쿼리 옵션 실행(일반 페이지)
  이 페이지를 사용하여 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리를 실행하는 옵션을 지정할 수 있습니다. 이 대화 상자에 액세스하려면 쿼리 편집기 창의 본문을 마우스 오른쪽 단추로 클릭한 다음 **쿼리 옵션**을 클릭합니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **SET ROWCOUNT**  
 기본값 0은 모든 결과를 받을 때까지 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 결과를 기다린다는 것을 나타냅니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에서 지정한 행 수를 받은 후 쿼리를 중단하려면 0보다 큰 값을 지정합니다. 모든 행이 반환될 수 있도록 이 옵션을 해제하려면 SET ROWCOUNT 0을 지정합니다.  
  
 **SET TEXTSIZE**  
 기본값 2,147,483,647바이트는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 `text`, `ntext`, `nvarchar(max)` 및 `varchar(max)` 데이터 필드의 제한까지 전체 데이터 필드를 제공한다는 것을 나타냅니다. XML 데이터 형식에는 영향을 주지 않습니다. 값이 클 경우 결과를 제한하려면 보다 작은 수를 지정합니다. 지정한 수보다 많은 열은 잘립니다.  
  
 **실행 제한 시간**  
 쿼리를 취소할 때까지 기다리는 시간(초)을 나타냅니다. 값 0은 무한 대기 또는 제한 시간 없음을 의미합니다.  
  
 **일괄 처리 구분 기호**  
 Transact-SQL 문을 일괄 처리로 구분하는 데 사용할 단어를 입력합니다. 기본값은 GO입니다.  
  
 **기본적으로 SQLCMD 모드로 새 쿼리 열기**  
 SQLCMD 모드로 새 쿼리를 열려면 이 확인란을 선택합니다. 이 확인란은 **도구** 메뉴를 통해 대화 상자를 연 경우에만 표시됩니다.  
  
 이 옵션을 선택할 경우 다음과 같은 제한 사항에 유의해야 합니다.  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)] 쿼리 편집기에서 IntelliSense는 해제되어 있습니다.  
  
-   쿼리 편집기를 명령줄에서 실행하지 못하므로 변수와 같은 명령줄 매개 변수를 전달할 수 없습니다.  
  
-   쿼리 편집기는 운영 체제 프롬프트에 응답할 수 없으므로 대화형 문을 실행하지 않도록 주의해야 합니다.  
  
 **기본값으로 다시 설정**  
 이 페이지의 모든 값을 원래 기본값으로 다시 설정합니다.  
  
  
