---
description: 명명되지 않은 매개 변수를 사용하여 쿼리 만들기(Visual Database Tools)
title: 명명되지 않은 매개 변수를 사용하여 쿼리 만들기
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 7182e87108952ddaee18a32dce54f1c980c2afe2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468407"
---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>명명되지 않은 매개 변수를 사용하여 쿼리 만들기(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
리터럴 값에 대한 자리 표시자로 물음표(?)를 지정하면 명명되지 않은 매개 변수를 사용하여 쿼리를 만들 수 있습니다. 쿼리 및 뷰 디자이너에서 이러한 매개 변수에 임시 이름이 지정됩니다. 쿼리에서 지정할 수 있는 명명되지 않은 매개 변수의 수에는 제한이 없습니다.  
  
쿼리 및 뷰 디자이너에서 쿼리를 실행하면 임시 이름이 적용된 쿼리 매개 변수 대화 상자가 표시됩니다.  
  
### <a name="to-specify-an-unnamed-parameter"></a>명명되지 않은 매개 변수를 지정하려면  
  
1.  검색하려는 열이나 식을 [조건 창](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)에 추가합니다. 검색 열이나 식이 쿼리 출력에 표시되지 않도록 하려면 이를 출력 열에서 제거합니다.  
  
2.  검색할 데이터 열이나 식이 포함된 행을 찾은 다음 표 형태의 **필터** 열에 물음표(?)를 입력합니다.  
  
    쿼리 및 뷰 디자이너에서는 "=" 연산자가 기본적으로 추가됩니다. 셀을 편집하여 이 연산자를 ">", "<" 또는 임의의 다른 SQL 비교 연산자로 바꿀 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[매개 변수를 사용하여 쿼리&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
