---
description: 다이어그램에서 테이블 간의 관계 만들기(Visual Database Tools)
title: 다이어그램에서 테이블 간 관계 만들기
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- diagrams [SQL Server], designing
ms.assetid: 28e9630c-dff4-46cc-bb0e-fe77998b6ac2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: a90f644aeaf17bd51c8963f355c9932c85da7c58
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468439"
---
# <a name="create-relationships-between-tables-on-a-diagram-visual-database-tools"></a>다이어그램에서 테이블 간의 관계 만들기(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
다이어그램 디자이너에서 테이블 간에 열을 끌어 서로 다른 테이블의 열 간에 관계를 만들 수 있습니다.  
  
### <a name="to-create-a-relationship-graphically"></a>관계를 그래픽으로 만들려면  
  
1.  데이터베이스 디자이너에서 다른 테이블의 열에 관련시킬 하나 이상의 데이터베이스 열에 대한 행 선택기를 클릭합니다.  
  
2.  선택한 열을 관련 테이블로 끌어 옵니다.  
  
3.  **외래 키 관계** 대화 상자가 나타나고 포그라운드에 **테이블 및 열**대화 상자가 나타납니다.  
  
4.  **관계 이름**에는 FK_*localtable*\_*foreigntable* 형식으로 시스템에서 제공된 이름이 표시됩니다. 이 값은 변경할 수 있습니다.  
  
5.  **기본 키 테이블** 이 정확한 테이블을 지정하는지 확인합니다.  
  
6.  표에 로컬 열 및 일치하는 외래 열이 표시됩니다. 테이블 열을 추가 또는 제거하거나 매핑을 변경할 수 있습니다.  
  
7.  **확인**을 선택합니다.  
  
    **외래 키 관계** 대화 상자가 나타납니다. **선택한 관계** 에는 만든 관계가 표시됩니다.  
  
8.  표에서 관계 속성을 변경합니다.  
  
9. **확인** 을 선택하여 관계를 만듭니다.  
  
    데이터베이스 디자이너에서는 선택한 열 간의 관계를 보여 줍니다.  
  
## <a name="see-also"></a>참고 항목  
[테이블 및 열 대화 상자&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/tables-and-columns-dialog-box-visual-database-tools.md)  
[제약 조건 작업](https://msdn.microsoft.com/637098af-2567-48f8-90f4-b41df059833e)  
[데이터베이스 다이어그램에서 테이블 작업&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
  
