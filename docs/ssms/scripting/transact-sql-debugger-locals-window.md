---
title: 지역 창
description: Transact-SQL 디버거의 지역 창을 사용하여 현재 호출 스택 프레임에서 식을 표시하고 수정하는 방법을 알아봅니다.
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Locals Window [Transact-SQL]
ms.assetid: 59bea640-7823-4b4d-832c-f384d83cca2f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 20246ae24d3b8916537e041218dadf4bf1e3a042
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036166"
---
# <a name="transact-sql-debugger---locals-window"></a>Transact-SQL 디버거 - 지역 창

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

**지역** 창에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거의 현재 범위에 있는 지역 식에 대한 정보가 표시됩니다. 범위는 **호출 스택** 창에서 선택한 현재 호출 스택 프레임으로 설정됩니다. 지역 식을 표시하려면 디버그 모드여야 합니다.  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>작업 목록

**지역 창에 액세스하려면**
  
-   **디버그** 메뉴에서 **창**을 선택한 다음 **지역**을 클릭합니다.  
  
 **식 값을 변경하려면**  
  
-   식을 마우스 오른쪽 단추로 클릭하고 **값 편집**을 선택합니다.  
  
## <a name="columns"></a>열  
 **이름**  
 지역 식의 이름입니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거는 변수, 매개 변수 및 @@ 기호로 시작하는 시스템 함수를 표시합니다.  
  
 **값**  
 현재 지역 식에 할당된 값을 표시합니다. 식에 할당된 값이 없으면 이 열은 비어 있습니다.  
  
 식의 길이가 **값** 열의 너비보다 큰 경우 해당 식의 **값** 셀 위로 포인터를 움직이면 도구 설명에 전체 값이 표시됩니다.  
  
 **디버거 시각화 도우미를 사용할 수 있는 경우** 값 [!INCLUDE[tsql](../../includes/tsql-md.md)] 셀에 돋보기 모양의 아이콘이 표시됩니다. 목록에서 **텍스트 시각화 도우미**, **XML 시각화 도우미**또는 **HTML 시각화 도우미**중에서 지정할 수 있습니다. 디버거 시각화 도우미를 시작하려면 돋보기 모양의 아이콘을 클릭합니다. 그러면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거에서 데이터 형식에 적합한 형식으로 데이터를 표시하는 대화 상자가 열립니다.  
  
 **형식**  
 식의 데이터 형식을 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-SQL 디버거](./transact-sql-debugger.md)   
 [Transact-SQL 디버거 정보](./transact-sql-debugger-information.md)   
 [조사식 창](./transact-sql-debugger-watch-window.md)   
 [호출 스택 창](./transact-sql-debugger-call-stack-window.md)   
 [간략한 조사식 대화 상자](./transact-sql-debugger-quickwatch-dialog-box.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)