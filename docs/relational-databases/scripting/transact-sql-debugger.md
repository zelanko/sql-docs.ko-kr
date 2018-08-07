---
title: Transact-SQL 디버거 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, introduction
ms.assetid: 6e914699-0d85-46c2-aa2d-3e339ac2c4ce
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 2655734f79a198d7033df77cc8fb015bf5fbce79
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39564297"
---
# <a name="transact-sql-debugger"></a>Transact-SQL 디버거
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거를 사용하면 코드의 런타임 동작을 조사하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드에서 오류를 찾을 수 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창을 디버그 모드로 설정한 후 코드의 특정 줄에서 실행을 일시 중지하여 해당 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 사용하거나 반환하는 정보 및 데이터를 검사할 수 있습니다.  
  
## <a name="stepping-through-transact-sql-code"></a>Transact-SQL 코드 단계별 실행  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 편집기 창이 디버그 모드일 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 코드를 탐색하는 데 사용할 수 있는 다음 옵션을 제공합니다.  
  
-   개별 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 중단점을 설정합니다.  
  
     중단점은 데이터를 검사할 수 있도록 실행을 일시 중지할 지점을 지정합니다. 디버거를 시작하면 쿼리 편집기 창의 코드 첫 번째 줄에서 일시 중지됩니다. 설정한 첫 번째 중단점까지 실행하려면 **계속** 기능을 사용합니다. 또한 **계속** 기능을 사용하면 창이 현재 일시 중지된 위치에서 다음 중단점까지 실행할 수 있습니다. 중단점에서 실행을 일시 중지할 조건, **출력** 창에 표시할 정보, 중단점 위치 변경 등의 동작을 지정하여 중단점을 편집할 수 있습니다.  
  
-   다음 문을 한 단계씩 코드 실행합니다.  
  
     이 옵션을 사용하면 문 집합을 하나씩 탐색하고, 이동할 때마다 해당 동작을 관찰할 수 있습니다.  
  
-   저장 프로시저 또는 함수를 한 단계씩 코드 실행하거나 프로시저 단위로 실행합니다.  
  
     저장 프로시저에 오류가 없으면 저장 프로시저를 프로시저 단위로 실행할 수 있습니다. 프로시저 전체가 실행되고 결과가 코드로 반환됩니다.  
  
     저장 프로시저 또는 함수를 디버깅하려는 경우 모듈을 한 단계씩 코드 실행할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 모듈에 대한 원본 코드로 채워지는 새 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창이 열리고, 창이 디버그 모드로 지정된 다음 모듈의 첫 번째 문에서 실행이 일시 중지됩니다. 그리고 나서 중단점을 설정하거나 코드를 단계별로 실행하여 모듈 코드를 탐색할 수 있습니다.  
  
 디버거를 사용하여 코드를 탐색하는 방법은 [Transact-SQL 코드 단계별 실행](../../relational-databases/scripting/step-through-transact-sql-code.md)을 참조하세요.  
  
## <a name="viewing-debugger-information"></a>디버거 정보 보기  
 디버거가 특정 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 실행을 일시 중지할 때마다 다음 디버거 창을 사용하여 현재 실행 상태를 볼 수 있습니다.  
  
-   **지역** 및 **조사식** 이 창에서는 현재 할당된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식을 표시합니다. 식은 단일 스칼라 식으로 계산되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 절입니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 변수, 매개 변수 또는 이름이 @@로 시작하는 기본 제공 함수를 참조하는 식을 볼 수 있습니다. 이 창에서는 식에 현재 할당된 데이터 값도 표시합니다.  
  
-   **간략한 조사식.** 이 창에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식 값을 표시하고 해당 식을 **조사식** 창에 저장합니다.  
  
-   **중단점.** 이 창에서는 현재 설정된 중단점을 표시하고 이 중단점을 관리할 수 있습니다.  
  
-   **호출 스택.** 이 창에서는 현재 실행 위치를 표시합니다. 그리고 원래 쿼리 편집기 창에서 전달된 실행이 함수, 저장 프로시저 또는 트리거를 통해 현재 실행 위치에 도달하는 방법에 대한 정보도 제공합니다.  
  
-   **출력.** 이 창에서는 디버거의 시스템 메시지와 같은 여러 메시지 및 프로그램 데이터를 표시합니다.  
  
-   **결과** 및 **메시지** 쿼리 편집기 창의 이러한 탭에서는 이전에 실행한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 결과를 표시합니다.  
  
## <a name="transact-sql-debugger-tasks"></a>Transact-SQL 디버거 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|원격 디버깅을 위해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거를 구성하는 방법을 설명합니다.|[TSQL 디버거를 실행 하기 전에 방화벽 규칙 구성](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md)|  
|디버거 작동을 시작, 중지 및 제어하는 방법을 설명합니다.|[Transact-SQL 디버거 실행](../../relational-databases/scripting/run-the-transact-sql-debugger.md)|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거를 사용하여 코드를 단계별로 실행하는 방법을 설명합니다.|[Transact-SQL 코드 단계별 실행](../../relational-databases/scripting/step-through-transact-sql-code.md)|  
|디버거를 사용하여 매개 변수 및 변수와 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 데이터와 시스템 정보를 보는 방법을 설명합니다.|[Transact-SQL 디버거 정보](../../relational-databases/scripting/transact-sql-debugger-information.md)|  
  
## <a name="see-also"></a>참고 항목  
 [쿼리 및 텍스트 편집기&#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
