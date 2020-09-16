---
title: 중단점 조건 지정
description: 중단점이 적중되고 적중 횟수가 도달되면 디버거가 중단점 작업을 수행할지 여부를 제어하는 중단점 조건을 설정하는 방법을 알아봅니다.
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint conditions
ms.assetid: b43d8a2b-99a3-4fb7-8848-99c042ea7ef7
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.reviewer: ''
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 451776ba842c38ca306c17291404355908cb5202
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901595"
---
# <a name="specify-a-breakpoint-condition"></a>중단점 조건 지정

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

중단점 조건은 중단점에 도달할 때마다 디버거가 평가하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 식입니다. 지정한 조건을 만족하고 지정한 적중 횟수에 도달하면 디버거는 중단점에 대해 지정된 동작을 중단하거나 수행합니다.  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="specifying-conditions"></a>조건 지정

부울 값으로 평가되는 올바른 Transact-SQL 식을 지정해야 합니다. 자세한 내용은 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.  
  
 올바르지 않은 구문을 사용하여 중단점 조건을 지정하면 즉시 경고 메시지가 나타납니다. 구문은 올바르지만 의미 체계가 올바르지 않은 조건을 지정하면 처음 중단점에 도달할 때 경고 메시지가 표시됩니다. 두 경우 모두 올바르지 않은 중단점에 도달하면 디버거가 실행을 중지합니다.  
  
#### <a name="to-specify-a-condition"></a>조건을 지정하려면
  
1. 편집기 창에서 중단점 문자 모양을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **조건** 을 클릭합니다.  
  
     또는  
  
     **중단점** 창에서 중단점 문자 모양을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **조건** 을 클릭합니다.  
  
2. **중단점 조건** 대화 상자에서 **조건** 상자에 올바른 부울 식을 입력합니다.  
  
3. 식의 결과가 **true** 일 경우 중단하려면 **참인 경우**를 선택하고, 식의 값이 변경될 경우 중단하려면 **이(가) 변경된 경우** 를 선택합니다.  
  
    > [!NOTE]  
    >  중단점에 처음 도달할 때까지 디버거는 부울 식을 평가하지 않습니다. **이(가) 변경된 경우**를 선택한 경우 디버거는 첫 번째 평가를 변경으로 간주하지 않으므로 첫 번째 평가 시에는 중단하지 않습니다.  
  
## <a name="see-also"></a>참고 항목

- [적중 횟수 지정](../../relational-databases/scripting/specify-a-hit-count.md)
- [중단점 동작 지정](../../relational-databases/scripting/specify-a-breakpoint-action.md)
