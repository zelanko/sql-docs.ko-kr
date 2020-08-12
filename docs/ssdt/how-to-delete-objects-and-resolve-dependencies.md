---
title: 개체 삭제 및 종속성 해결
description: 데이터베이스 개체를 삭제하거나 개체 이름을 바꾸는 방법을 알아봅니다. SSDT가 자동으로 업데이트하는 종속 개체와 직접 업데이트해야 하는 종속성을 확인합니다.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Data.Tools.Project.HelpKeywords.SqlProjectDropDatabaseConfirmationDialog
- sql.data.tools.dropdatabaseconfirmation.dialog
- sql.data.tools.dropmultipledatabasesconfirmation.dialog
ms.assetid: fb31c2b1-ca4f-4e11-a0b6-5c26430f1c8c
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: aecacc373ccd1392217d57d51875094a5f9d4d34
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2020
ms.locfileid: "85519063"
---
# <a name="how-to-delete-objects-and-resolve-dependencies"></a>방법: 개체 삭제 및 종속성 해결

**SQL Server 개체 탐색기**에서 개체의 이름을 바꾸거나 개체를 삭제하면 SQL Server Data Tools에서는 모든 종속성 개체를 자동으로 검색하고, 필요한 경우 종속성 개체의 이름을 바꾸거나 삭제할 ALTER 스크립트를 준비합니다.  
  
> [!WARNING]  
> 다음 절차에서는 이전의 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 섹션에 나오는 절차에서 만든 엔터티를 사용합니다.  
  
### <a name="to-delete-a-database"></a>데이터베이스를 삭제하려면  
  
1.  **SQL Server 개체 탐색기**에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.  
  
2.  **데이터베이스 삭제**에서 모든 기본 설정을 그대로 사용하고 **확인**을 클릭합니다.  
  
### <a name="to-rename-a-table"></a>테이블 이름을 바꾸려면  
  
1.  `Customer` 테이블이 테이블 디자이너나 Transact\-SQL 편집기에서 열려 있지 않은지 확인합니다.  
  
2.  **SQL Server 개체 탐색기**에서 **테이블** 노드를 확장합니다. **Customer** 테이블을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택합니다.  
  
3.  테이블 이름을 **Customers**로 변경하고 Enter 키를 누릅니다.  
  
4.  **데이터베이스 업데이트** 작업이 자동으로 즉시 호출됩니다. SSDT에서는 sp_rename 저장 프로시저를 자동으로 호출하여 테이블의 이름을 바꿉니다. 외래 키 제약 조건과 같은 종속성 개체가 있는 경우 해당 개체도 업데이트됩니다.  
  
    > [!WARNING]  
    > 뷰 또는 저장 프로시저에서 사용하는 테이블에 대한 참조와 같은 스크립트 기반 종속성은 SSDT에서 자동으로 업데이트되지 않습니다. 이름을 바꾼 후 **오류 목록** 창을 사용하여 다른 모든 종속성 개체를 찾고 수동으로 수정할 수 있습니다.  
  
5.  이전 [방법: 파워 버퍼를 사용하여 연결된 데이터베이스 업데이트](../ssdt/how-to-update-a-connected-database-with-power-buffer.md) 절차의 단계에 따라 변경 내용을 적용합니다.  
  
6.  다시 **SQL Server 개체 탐색기**에서 **Customers** 테이블을 마우스 오른쪽 단추로 클릭하고 **데이터 보기**를 선택합니다. 이름 바꾸기 작업 후에도 테이블 데이터가 그대로 유지되는지 확인합니다.  
  
7.  **Products** 테이블을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 선택합니다. 외래 키 참조가 바뀐 이름을 반영하여 자동으로 `REFERENCES [dbo].[Customers] ([Id])`로 업데이트되었는지 확인합니다.  
  
### <a name="to-delete-a-table"></a>테이블 삭제  
  
1.  **SQL Server 개체 탐색기**에서 **Customers** 테이블을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.  
  
2.  **데이터베이스 업데이트 미리 보기** 대화 상자의 **사용자 작업**에서 SSDT가 모든 종속성 개체(이 경우 삭제할 외래 키 참조)를 식별했는지 확인합니다.  
  
3.  **데이터베이스 업데이트**를 클릭합니다.  
  
4.  **SQL Server 개체 탐색기**에서 **Products** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 선택합니다. `Customers` 테이블에 대한 외래 키 참조가 사라졌는지 확인합니다.  
  
    > [!WARNING]  
    > 삭제 작업이 수행될 때 **Products** 테이블이 이미 테이블 디자이너나 Transact\-SQL 편집기에 열려 있었으면 테이블이 자동으로 새로 고쳐지지 않으므로 외래 키 참조가 삭제되었는지 여부를 확인할 수 없습니다. 또한 해결되지 않은 참조에 대한 오류가 **오류 목록**에 표시될 수 있습니다. 이 문제를 해결하려면 테이블 디자이너나 Transact\-SQL 편집기를 닫고 Products 테이블을 다시 엽니다.  
  
