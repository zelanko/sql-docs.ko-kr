---
title: 명명되지 않은 매개 변수를 사용하여 쿼리 만들기(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5200924d784d8d28f99c83bca7ee1dca4a5787c4
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43817689"
---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>명명되지 않은 매개 변수를 사용하여 쿼리 만들기(Visual Database Tools)
  리터럴 값에 대한 자리 표시자로 물음표(?)를 지정하면 명명되지 않은 매개 변수를 사용하여 쿼리를 만들 수 있습니다. 쿼리 및 뷰 디자이너에서 이러한 매개 변수에 임시 이름이 지정됩니다. 쿼리에서 지정할 수 있는 명명되지 않은 매개 변수의 수에는 제한이 없습니다.  
  
 쿼리 및 뷰 디자이너에서 쿼리를 실행하면 임시 이름이 적용된 쿼리 매개 변수 대화 상자가 표시됩니다.  
  
### <a name="to-specify-an-unnamed-parameter"></a>명명되지 않은 매개 변수를 지정하려면  
  
1.  검색하려는 열이나 식을 [조건 창](visual-database-tools.md)에 추가합니다. 검색 열이나 식이 쿼리 출력에 표시되지 않도록 하려면 이를 출력 열에서 제거합니다.  
  
2.  검색할 데이터 열이나 식이 포함된 행을 찾은 다음 표 형태의 **필터** 열에 물음표(?)를 입력합니다.  
  
     쿼리 및 뷰 디자이너에서는 "=" 연산자가 기본적으로 추가됩니다. 셀을 편집하여 이 연산자를 ">", "<" 또는 임의의 다른 SQL 비교 연산자로 바꿀 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [매개 변수를 사용하여 쿼리&#40;Visual Database Tools&#41;](query-with-parameters-visual-database-tools.md)  
  
  
