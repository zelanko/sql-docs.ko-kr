---
title: 중단점 창
description: 데이터베이스 엔진 쿼리 편집기의 중단점 창을 사용하여 Transact-SQL 디버거 중단점을 관리하는 방법을 알아봅니다.
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Breakpoints Window [Transact-SQL]
ms.assetid: bad88d10-fdd5-4d3d-b5ea-a4f063847485
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 07/22/2020
monikerRange: '>= sql-server-2016'
ms.openlocfilehash: 915ad9a9429c9200613a0bb443b42237162ea9c7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476824"
---
# <a name="transact-sql-debugger---breakpoints-window"></a>Transact-SQL 디버거 - 중단점 창

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

**중단점** 창에서는 현재 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에 설정된 모든 중단점을 표시합니다. 중단점을 관리하려면 **중단점** 창의 도구 모음을 사용합니다. 여기서 중단점은 디버깅 데이터를 볼 수 있도록 디버그 모드에서 실행을 일시 중지하는 코드의 특정 위치를 의미합니다.

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>작업 목록

**중단점 창에 액세스하려면**

- **디버그** 메뉴에서 **Windows** 을 선택한 다음, **중단점** 을 선택합니다.

## <a name="breakpoints-window-columns"></a>중단점 창 열

기본적으로 **중단점** 창에는 다음과 같은 열이 표시됩니다.  

**이름**  
중단점의 이름을 표시합니다. 중단점 이름은 디버거에서 지정됩니다. 이 이름에는 중단점을 포함하는 데이터베이스 엔진 쿼리 편집기 창의 이름과 중단점이 설정된 쿼리 편집기의 줄 번호가 포함됩니다.  

**Condition**  
**(조건 없음)** 을 표시합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거는 중단점 조건 설정을 지원하지 않습니다.

**적중 횟수**  
**항상 중단** 을 표시합니다.

**열** 목록에서 다음 열을 선택하여 해당 열을 추가하거나 제거할 수 있습니다.  

**Filter**  
**(없음)** 을 표시합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거는 중단점 필터 설정을 지원하지 않습니다.

**적중될 때**  
**중단** 을 표시합니다.

**언어**  
**의 경우** Transact-SQL [!INCLUDE[tsql](../../includes/tsql-md.md)]을 표시합니다.  

**Function**  
중단점이 설정된 줄의 번호를 표시합니다.  

**최근에 사용한 파일**  
중단점을 포함하는 원본 파일 이름과 중단점이 설정된 줄의 번호를 표시합니다.

**주소**  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거는 이 기능을 지원하지 않습니다.  

**처리**  
**[SQL]** 을 표시하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 프로세스임을 나타냅니다. 코드를 실행하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 이름 뒤에 나옵니다.

## <a name="breakpoints-window-toolbar"></a>중단점 창 도구 모음

현재 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창에 활성 상태의 중단점이 있으면 중단점을 관리하는 데 사용할 수 있는 도구 모음이 **중단점** 창에 표시됩니다.

**Delete**  
선택한 중단점을 삭제합니다.

**모든 중단점 삭제**  
**중단점** 창에 표시된 모든 중단점을 삭제합니다.  

**모든 중단점 해제**  
더 이상 코드 실행을 중지하지 않도록 모든 중단점을 해제하지만 중단점은 그대로 남아 있습니다. 모든 중단점을 해제하면 **모든 중단점 설정** 단추로 바뀝니다.

**모든 중단점 설정**  
코드 실행을 중지하도록 모든 중단점을 설정합니다. 모든 중단점이 설정되면 **모든 중단점 해제** 단추로 바뀝니다.  

**소스 코드로 이동**  
쿼리 편집기에서 선택한 중단점을 포함하는 줄에 커서를 놓습니다.

**열**  
**중단점** 창에 표시할 수 있는 모든 열을 표시합니다. 확인란은 표시된 열을 나타냅니다. **중단점** 창에서 열을 추가하거나 제거하려면 목록에서 열을 선택합니다.

## <a name="see-also"></a>참고 항목

[Transact-SQL 디버거](./transact-sql-debugger.md)