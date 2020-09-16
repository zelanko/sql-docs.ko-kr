---
description: 결과 창에서 행 삭제(Visual Database Tools)
title: 결과 창에서 행 삭제
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- removing rows
- row removal [SQL Server], Visual Database Tools Results pane
- row deletions [SQL Server], Visual Database Tools Results pane
- Query Designer [SQL Server], Results pane
- deleting rows
- Results pane
ms.assetid: a1147905-fe4a-4fac-b576-a17622477e66
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 53d0e10900f918c16148f09853bf3c45d8c0bc21
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480035"
---
# <a name="delete-rows-in-the-results-pane-visual-database-tools"></a>결과 창에서 행 삭제(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
데이터베이스에서 레코드를 삭제하려면 결과 창에서 행을 삭제합니다. 삭제 쿼리를 사용하면 행 전체를 삭제할 수 있습니다. 자세한 내용은 [삭제 쿼리 만들기&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md)를 참조하세요. 결과 창에서 행을 제거만 하려면 쿼리 조건을 변경합니다. 자세한 내용은 [검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)를 참조하세요.  
  
### <a name="to-delete-a-row-or-rows"></a>하나 이상의 행을 삭제하려면  
  
1.  결과 창에서 삭제할 행 왼쪽에 있는 상자를 선택합니다.  
  
2.  Delete 키를 누릅니다.  
  
3.  삭제 확인 메시지가 대화 상자에 나타나면 **예**를 클릭합니다.  
  
> [!CAUTION]  
> 이런 방법으로 삭제하는 행은 데이터베이스에서 영구적으로 제거되므로 복원할 수 없습니다.  
  
> [!NOTE]  
> 데이터베이스에서 선택한 행 중 삭제할 수 없는 행이 하나라도 있으면 나머지 행도 삭제되지 않습니다. 이 경우 삭제할 수 없는 행에 대한 정보가 메시지로 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
[삭제 쿼리 만들기&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-delete-queries-visual-database-tools.md)  
[검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
