---
title: 쿼리에 TOP 절 지정(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- TOP clause, queries
- percentage of rows returned [SQL Server]
- number of rows
- search conditions [SQL Server], TOP clause
- restricting rows returned
- search criteria [SQL Server], limiting rows returned
- inspecting portion of results
- limiting rows returned
- search criteria [SQL Server], TOP clause
ms.assetid: ba7d7c10-9bb3-4d9b-90b0-5fa94ecae59b
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1bcf376898866238839c0658d9b445e11b05c70e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33049480"
---
# <a name="specify-the-top-clause-in-queries-visual-database-tools"></a>쿼리에 TOP 절 지정(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
TOP 절은 쿼리에서 처음 *n*개 또는 *n%* 의 행만 반환합니다. TOP 절은 쿼리 결과를 모두 반환하는 데 필요한 리소스를 사용하지 않은 채 쿼리가 의도한 대로 올바르게 작동하는지 확인하기 위해 결과의 일부만 검사하려는 경우에 유용합니다.  
  
### <a name="to-specify-the-top-clause-in-queries"></a>쿼리에 TOP 절을 지정하려면  
  
1.  솔루션 탐색기에서 쿼리를 열거나 새 쿼리를 만듭니다.  
  
2.  **보기** 메뉴에서 **속성 창**을 클릭합니다.  
  
3.  **속성 창**에서 **Top 사양** 속성을 찾아 확장합니다.  
  
4.  **(Top)** 자식 속성을 클릭하고 이를 **예**로 설정합니다.  
  
5.  **식** 자식 속성에 숫자 결과가 있는 식(예: "10" 또는 "2*5")을 입력합니다.  
  
6.  **Percent** 자식 속성을 클릭하고 **식** 속성을 반환된 행 전체의 백분율로 간주할지(예) 반환된 행의 절대 수로 간주할지(아니요) 여부를 지정합니다.  
  
7.  쿼리에 ORDER BY 절이 사용되는 경우 그룹의 일부만 포함된 상태에서 그룹의 행 전체를 표시하려면 **With Ties** 자식 속성을 클릭한 다음 **예** 를 선택하고 표시되지 않은 행을 잘라내려면 **아니요** 를 선택합니다.  
  
위에서 설명한 작업을 진행할 때는 SQL 창에 표시된 TOP 절이 속성의 현재 설정을 반영하도록 변경되는 것을 확인할 수 있습니다.  
  
> [!NOTE]  
> SQL 창에서 TOP 절을 편집하여 **Top 사양** 의 자식 속성 값을 변경할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[쿼리 속성&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-properties-visual-database-tools.md)  
  
