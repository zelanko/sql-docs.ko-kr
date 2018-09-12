---
title: 매개 변수 쿼리(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- parameter queries [SQL Server]
ms.assetid: 4897c41a-324a-47b8-a30b-cbc9e9e19a8b
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e8e1f6503ba431314f7addd0b33d2c607a32fb9c
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43812299"
---
# <a name="parameter-queries-visual-database-tools"></a>매개 변수 쿼리(Visual Database Tools)
  경우에 따라 매번 다른 값으로 여러 번 사용할 수 있는 쿼리를 만들 필요가 있습니다. 예를 들어, 한 명의 저자가 저술한 책의 `title_ids` 를 모두 찾기 위해 쿼리하는 경우가 종종 있습니다. 각 요청에 대해 매번 저자의 ID 또는 이름만 다른 동일한 쿼리를 실행할 수 있습니다.  
  
 매번 다른 값을 가질 수 있는 쿼리를 만들려면 쿼리에 매개 변수를 사용합니다. 매개 변수는 쿼리를 실행할 때 제공되는 값에 대한 자리 표시자입니다. 매개 변수를 사용하는 SQL 문은 다음과 같습니다. 여기에서 "?"는 저자의 ID에 대한 매개 변수입니다.  
  
```  
SELECT title_id  
FROM titleauthor  
WHERE (au_id = ?)  
```  
  
## <a name="where-you-can-use-parameters"></a>매개 변수를 사용할 수 있는 위치  
 매개 변수를 리터럴 텍스트 값 또는 리터럴 숫자 값에 대한 자리 표시자로 사용할 수 있습니다. 매개 변수는 일반적으로 SQL 문의 WHERE 절 또는 HAVING 절에 있는 개별 행이나 그룹에 대한 검색 조건에서 자리 표시자로 사용됩니다.  
  
 매개 변수를 식의 자리 표시자로 사용할 수 있습니다. 예를 들어, 쿼리를 실행할 때마다 다른 할인 가격을 제공하여 할인된 가격을 계산할 수 있습니다. 이렇게 하려면 다음과 같은 식을 지정합니다.  
  
```  
(price * ?)  
```  
  
## <a name="specifying-unnamed-and-named-parameters"></a>명명되지 않은 매개 변수 및 명명된 매개 변수 지정  
 명명되지 않은 매개 변수와 명명된 매개 변수와 같이 두 가지 형식의 매개 변수를 지정할 수 있습니다. 명명되지 않은 매개 변수는 리터럴 값을 입력하거나 이를 대체할 쿼리의 임의 위치에 넣는 물음표(?)입니다. 예를 들어 `titleauthor` 테이블에서 저자의 ID를 검색하기 위해 명명되지 않은 매개 변수를 사용하는 경우 [SQL 창](visual-database-tools.md) 에 나타나는 결과 문은 다음과 같습니다.  
  
```  
SELECT title_id  
FROM titleauthor  
WHERE (au_id = ?)  
```  
  
 [쿼리 및 뷰 디자이너](query-and-view-designer-tools-visual-database-tools.md)에서 쿼리를 실행하면 [쿼리 매개 변수 대화 상자](query-parameters-dialog-box-visual-database-tools.md) 에 매개 변수 이름으로 "?"가 나타납니다.  
  
 또는 매개 변수에 이름을 할당할 수도 있습니다. 명명된 매개 변수는 쿼리에 여러 개의 매개 변수가 있는 경우 특히 유용합니다. 예를 들어, 명명된 매개 변수를 사용하여 `authors` 테이블에서 저자의 이름과 성을 검색하는 경우 SQL 창에 나타나는 결과 문은 다음과 같습니다.  
  
```  
SELECT au_id  
FROM authors  
WHERE au_fname = %first name% AND  
      au_lname = %last name%  
```  
  
> [!TIP]  
>  명명된 매개 변수 쿼리를 만들기 전에 접두사와 접미사를 정의해야 합니다.  
  
 쿼리 및 뷰 디자이너에서 쿼리를 실행하면 [쿼리 매개 변수 대화 상자](query-parameters-dialog-box-visual-database-tools.md) 에 명명된 매개 변수의 목록이 나타납니다.  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 매개 변수를 사용 하 여 &#40;Visual Database Tools&#41;](query-with-parameters-visual-database-tools.md)   
 [지원 되는 쿼리 유형 &#40;Visual Database Tools&#41;](supported-query-types-visual-database-tools.md)   
 [쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
