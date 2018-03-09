---
title: "다이어그램에서 테이블 간의 관계 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: diagrams [SQL Server], designing
ms.assetid: 28e9630c-dff4-46cc-bb0e-fe77998b6ac2
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cae309a79569a4a7ca88fced9163012f54612387
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="create-relationships-between-tables-on-a-diagram-visual-database-tools"></a>다이어그램에서 테이블 간의 관계 만들기(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 다이어그램 디자이너에서 테이블 간에 열을 끌어 서로 다른 테이블의 열 간에 관계를 만들 수 있습니다.  
  
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
[테이블 및 열 대화 상자&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/tables-and-columns-dialog-box-visual-database-tools.md)  
[제약 조건 작업(Visual Database Tools)](http://msdn.microsoft.com/en-us/637098af-2567-48f8-90f4-b41df059833e)  
[데이터베이스 다이어그램에서 테이블 작업&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
  
