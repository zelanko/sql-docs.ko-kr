---
title: 다이어그램에서 테이블 간의 관계 만들기 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- diagrams [SQL Server], designing
ms.assetid: 28e9630c-dff4-46cc-bb0e-fe77998b6ac2
author: stevestein
ms.author: sstein
ms.openlocfilehash: ebc443cd44ca439497d11936b732141ae3f5a960
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058038"
---
# <a name="create-relationships-between-tables-on-a-diagram-visual-database-tools"></a>다이어그램에서 테이블 간의 관계 만들기(Visual Database Tools)
  다이어그램 디자이너에서 테이블 간에 열을 끌어 서로 다른 테이블의 열 간에 관계를 만들 수 있습니다.  
  
### <a name="to-create-a-relationship-graphically"></a>관계를 그래픽으로 만들려면  
  
1.  데이터베이스 디자이너에서 다른 테이블의 열에 관련시킬 하나 이상의 데이터베이스 열에 대한 행 선택기를 클릭합니다.  
  
2.  선택한 열을 관련 테이블로 끌어 옵니다.  
  
3.  **외래 키 관계** 대화 상자가 나타나고 포그라운드에 **테이블 및 열**대화 상자가 나타납니다.  
  
4.  **관계 이름** 에는 FK_*localtable*_*foreigntable*형식으로 시스템에서 제공한 이름이 표시됩니다. 이 값은 변경할 수 있습니다.  
  
5.  **기본 키 테이블** 이 정확한 테이블을 지정하는지 확인합니다.  
  
6.  표에 로컬 열 및 일치하는 외래 열이 표시됩니다. 테이블 열을 추가 또는 제거하거나 매핑을 변경할 수 있습니다.  
  
7.  **확인**을 선택합니다.  
  
     **외래 키 관계** 대화 상자가 나타납니다. **선택한 관계** 에는 만든 관계가 표시됩니다.  
  
8.  표에서 관계 속성을 변경합니다.  
  
9. **확인** 을 선택하여 관계를 만듭니다.  
  
     데이터베이스 디자이너에서는 선택한 열 간의 관계를 보여 줍니다.  
  
## <a name="see-also"></a>참고 항목  
 [테이블 및 열 대화 상자 &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Unique 제약 조건 및 Check 제약 조건](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [데이터베이스 다이어그램에서 테이블 작업&#40;Visual Database Tools&#41;](work-with-tables-in-database-diagram-visual-database-tools.md)  
  
  
