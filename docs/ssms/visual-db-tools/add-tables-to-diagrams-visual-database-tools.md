---
title: "다이어그램에 테이블 추가(Visual Database Tools) | Microsoft 문서 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- inserting tables
- adding tables
ms.assetid: 5440fdf7-ac04-4325-9f32-181f4cd402e5
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ae6c38826ce111508e88de0948ffe8e1ecb35c24
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="add-tables-to-diagrams-visual-database-tools"></a>다이어그램에 테이블 추가(Visual Database Tools)
데이터베이스 다이어그램에 테이블을 추가하여 구조를 편집하거나 다이어그램에 있는 다른 테이블에 연결할 수 있습니다. 다이어그램에 기존의 데이터베이스 테이블을 추가하거나 데이터베이스에 아직 정의되지 않은 새 테이블을 삽입할 수 있습니다.  
  
### <a name="to-insert-a-new-table-into-a-diagram"></a>다이어그램에 새 테이블을 삽입하려면  
  
1.  테이블을 만들 데이터베이스에 연결되어 있는지 확인합니다.  
  
    현재 다이어그램에 테이블을 만들려면 도구 모음에서 **새 테이블** 단추를 클릭합니다.  
  
    -또는-  
  
    다이어그램 내부를 마우스 오른쪽 단추로 클릭하고 **새 테이블**을 선택합니다.  
  
2.  **이름 선택** 대화 상자에서 시스템 할당 테이블 이름을 그대로 사용하거나 수정한 다음 **확인**을 선택합니다.  
  
    다이어그램에 새 테이블이 표준 뷰로 나타납니다.  
  
3.  새 테이블의 첫째 셀에 열 이름을 입력합니다. 그런 다음 Tab 키를 눌러 다음 셀로 이동합니다.  
  
4.  **데이터 형식**에서 해당 열의 데이터 형식을 선택합니다. 각 열에는 이름과 데이터 형식이 있어야 합니다.  
  
    테이블 디자이너에서 열의 다른 속성을 설정할 수 있습니다.  
  
5.  테이블에 추가할 각 열에 대하여 3, 4단계를 반복합니다.  
  
> [!NOTE]  
> 데이터베이스 다이어그램을 저장하면 데이터베이스에 새 테이블이 추가됩니다.  
  
### <a name="to-add-an-existing-table-to-a-diagram"></a>다이어그램에 기존 테이블을 추가하려면  
  
1.  편집할 테이블이 있는 데이터베이스에 연결되어 있는지 확인합니다.  
  
2.  **테이블** 폴더에서 테이블을 선택합니다.  
  
3.  데이터베이스 다이어그램으로 테이블을 끕니다.  
  
4.  마우스 단추를 놓습니다.  
  
> [!NOTE]  
> 다이어그램에서 선택한 테이블과 다른 테이블 사이에 관계가 있으면 자동으로 관계 선이 그려집니다.  
  
### <a name="to-add-related-tables-to-a-diagram"></a>다이어그램에 관련 테이블을 추가하려면  
  
1.  데이터베이스 다이어그램에서 외래 키 제약 조건이 있는 테이블을 하나 이상 선택합니다.  
  
2.  선택한 테이블 중 하나를 마우스 오른쪽 단추로 클릭하고 **관련 테이블 추가**를 선택합니다.  
  
> [!NOTE]  
> 선택한 테이블에서 외래 키 제약 조건에 의해 참조되는 테이블과 외래 키 제약 조건이 있는 선택된 테이블을 참조하는 테이블 모두가 다이어그램에 추가됩니다.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스 다이어그램 작업(Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[데이터베이스 다이어그램에서 테이블 작업(Visual Database Tools)](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
  

