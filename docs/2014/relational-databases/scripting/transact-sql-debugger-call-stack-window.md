---
title: 호출 스택 창 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Call Stack Window [Transact-SQL]
ms.assetid: ddb0b19c-87cd-4883-bcb8-ec09ffb30369
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed3fbddcf91fe63920b349224a0dde73141c6d75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66063523"
---
# <a name="call-stack-window"></a>호출 스택 창
  **호출 스택** 창에는 호출 스택의 모듈, 모듈에 전달되는 매개 변수의 값 및 데이터 형식이 표시됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈은 저장 프로시저, 함수 및 트리거를 포함합니다. 호출 스택을 표시하려면 디버그 모드여야 합니다.  
  
## <a name="task-list"></a>작업 목록  
 **호출 스택 창에 액세스하려면**  
  
-   **디버그** 메뉴에서 **창**을 선택한 다음 **호출 스택**을 클릭합니다.  
  
 **현재 호출 스택 프레임을 변경하려면**  
  
 다음 절차 중 하나를 사용하여 스택 프레임을 현재 프레임으로 지정할 수 있습니다.  
  
-   스택 프레임을 마우스 오른쪽 단추로 클릭하고 **프레임으로 전환**을 클릭합니다.  
  
-   스택 프레임을 두 번 클릭합니다.  
  
 **현재 프레임이 아닌 프레임 원본을 보려면**  
  
-   스택 프레임을 마우스 오른쪽 단추로 클릭한 다음 **소스 코드로 이동**을 클릭합니다.  
  
## <a name="stack-frames"></a>스택 프레임  
 **호출 스택** 창의 각 행은 스택 프레임이라고 하며 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 파일에서의 모듈 호출 또는 모듈 사이의 호출을 나타냅니다. 화면의 맨 아래 스택 프레임은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창에서 스택으로 처음 호출을 수행한 줄을 나타냅니다. 맨 위 행은 디버거가 실행을 일시 중지한 행을 나타내며 창의 왼쪽 여백에 노란 화살표로 표시됩니다. 각 중간 행은 모듈과 다음으로 높은 스택 프레임을 호출한 원본 코드의 줄 번호를 나타냅니다.  
  
 **지역**, **조사식**및 **간략한 조사식** 창의 모든 식은 현재 스택 프레임을 기준으로 평가됩니다. 현재 프레임에 대한 코드는 쿼리 편집기 창에 표시됩니다. 기본적으로 현재 스택 프레임은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거가 실행을 일시 중지한 프레임입니다. 현재 스택 프레임에서 다른 프레임으로 변경하면 **지역**, **조사식**및 **간략한 조사식** 창의 식은 새 프레임의 컨텍스트에서 다시 평가되고 새 프레임의 원본 코드가 쿼리 편집기 창에 표시됩니다.  
  
## <a name="columns"></a>열  
 **이름**  
 호출 스택의 모듈에 대한 정보를 표시합니다.  
  
 호출 스택의 맨 아래 행에서 **이름** 에는 쿼리 편집기 원본 창과 스택으로 처음 호출을 수행한 줄 번호가 표시됩니다. 다른 행에서 **이름** 형식은 **Module(Instance.Database)(ParmList) LineNumber**입니다.  
  
 **모듈**  
 해당 저장 프로시저 또는 함수의 이름이나 다음 프레임으로 호출되는 저장 프로시저의 이름입니다.  
  
 **Instance.Database**  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 및 모듈을 포함하는 데이터베이스입니다.  
  
 **ParmList**  
 모듈 호출 중에 전달되는 각 매개 변수의 데이터 형식, 이름 및 값을 나타냅니다.  
  
 **LineNumber**  
 맨 위 행을 제외한 모든 행에서 **LineNumber** 는 모듈에서 프레임으로 호출된 줄을 나타냅니다. 맨 위 행에서 **LineNumber** 는 현재 디버거의 포커스가 있는 줄을 나타냅니다.  
  
 **언어**  
 **의 경우** Transact-SQL [!INCLUDE[tsql](../../includes/tsql-md.md)]을 표시합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Transact-SQL 디버거](transact-sql-debugger.md)   
 [Transact-SQL 디버거 정보](transact-sql-debugger-information.md)   
 [Transact-SQL 코드 단계별 실행](step-through-transact-sql-code.md)  
