---
title: 조사식 창 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Watch Window [Transact-SQL]
ms.assetid: 23f3baa4-14c2-4262-92f7-3f43fcfa0436
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 54b34b87f48f43bfbbe5ca40d423f8b017905601
ms.sourcegitcommit: c29150492383f48ef484fa02a483cde1cbc68aca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65821652"
---
# <a name="transact-sql-debugger---watch-window"></a>Transact-SQL 디버거 - 조사식 창
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  **조사식** 창은 선택한 식에 대한 정보를 표시합니다. 조사식 창은 **조사식 1**, **조사식 2, 조사식 3** 및 **조사식 4**의 최대 4개의 창으로 구성할 수 있습니다. 식은 **호출 스택** 창에서 선택한 현재 호출 스택 프레임 범위 내에서 평가됩니다. 변수 및 식을 조사하려면 디버그 모드여야 합니다.  
  
## <a name="task-list"></a>작업 목록  
 **조사식 창에 액세스하려면**  
  
-   **디버그** 메뉴에서 **창**, **조사식**을 차례로 클릭하고 **조사식 1**, **조사식 2, 조사식 3**또는 **조사식 4**를 클릭합니다.  
  
 **식 값을 변경하려면**  
  
-   식을 마우스 오른쪽 단추로 클릭하고 **값 편집**을 선택합니다.  
  
## <a name="columns"></a>열  
 **이름**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거에 표시된 식입니다. 지원되는 식은  
  
-   변수  
  
-   매개 변수.  
  
-   이름이 @@로 시작하는 시스템 함수  
  
-   @IntegerCounter + 1 또는 FirstName + LastName과 같이 하나 이상의 변수, 매개 변수 또는 시스템 함수에 연산자를 적용하여 빌드한 식  
  
-   SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1과 같이 단일 값을 반환하는 Transact-SQL 문  
  
 **Value**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거에서 **이름**에 지정된 식을 평가한 후 반환되는 값을 표시합니다.  
  
 식의 길이가 **값** 열의 너비보다 큰 경우 해당 식의 **값** 셀 위로 포인터를 움직이면 도구 설명에 전체 값이 표시됩니다.  
  
 **디버거 시각화 도우미를 사용할 수 있는 경우** 값 [!INCLUDE[tsql](../../includes/tsql-md.md)] 셀에 돋보기 모양의 아이콘이 표시됩니다. 목록에서 **텍스트 시각화 도우미**, **XML 시각화 도우미**또는 **HTML 시각화 도우미**중에서 지정할 수 있습니다. 디버거 시각화 도우미를 시작하려면 돋보기 모양의 아이콘을 클릭합니다. 그러면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거에서 데이터 형식에 적합한 형식으로 데이터를 표시하는 대화 상자가 열립니다.  
  
 **형식**  
 식의 데이터 형식을 표시합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-SQL 디버거](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL 디버거 정보](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [지역 창](../../relational-databases/scripting/transact-sql-debugger-locals-window.md)   
 [호출 스택 창](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [간략한 조사식 대화 상자](../../relational-databases/scripting/transact-sql-debugger-quickwatch-dialog-box.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
