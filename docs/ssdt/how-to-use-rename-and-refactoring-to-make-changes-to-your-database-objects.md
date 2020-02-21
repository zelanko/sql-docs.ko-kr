---
title: 데이터베이스 개체를 변경하기 위한 이름 바꾸기 및 리팩터링
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.dbrefactoring.previewdialog
- sql.data.tools.editor.howto.refactoring
- sql.data.tools.dbrefactoring.renamedialog
- sql.data.tools.dbrefactoring.moveschemadialog
- sql.data.tools.dbrefactoring.renameserverdatabasedialog
ms.assetid: f35520e6-8e6e-47b1-87a3-22c0cf2cabdb
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: ac10530cf2fa3831a26733e7470b6bd107d17121
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244238"
---
# <a name="how-to-use-rename-and-refactoring-to-make-changes-to-your-database-objects"></a>방법: 이름 바꾸기 및 리팩터링을 사용하여 데이터베이스 개체 변경

Transact\-SQL 편집기의 리팩터링 상황에 맞는 메뉴를 사용하여 개체의 이름을 바꾸거나 개체를 다른 스키마로 이동하고, 변경 내용을 커밋하기 전에 영향을 받는 모든 영역을 미리 볼 수 있습니다. 리팩터링 메뉴를 사용하여 데이터베이스 개체에 대한 모든 참조를 정규화하거나 데이터베이스 프로젝트에서 `SELECT` 문의 와일드카드 문자를 확장할 수도 있습니다.  
  
> [!NOTE]  
> 다음 절차에서는 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 및 [프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md) 섹션의 이전 절차에서 만들어진 엔터티를 활용합니다.  
  
### <a name="to-rename-a-type"></a>테이블의 이름을 바꾸려면  
  
1.  **솔루션 탐색기**에서 **Products** 테이블(Products.sql)을 마우스 오른쪽 단추로 클릭하고 **코드 보기**를 선택하여 Transact\-SQL 편집기에서 스크립트를 엽니다.  
  
2.  스크립트의 `[Products]`를 마우스 오른쪽 단추로 클릭하고 **리팩터링**, **이름 바꾸기**를 차례로 선택합니다.  
  
3.  **새 이름** 필드에서 이름을 **Product**로 변경합니다. **변경 내용 미리 보기** 옵션을 선택된 상태로 두고 **확인**을 클릭합니다.  
  
4.  다음 화면에서 이 이름 바꾸기 작업으로 인해 영향을 받을 스크립트의 목록을 미리 볼 수 있습니다. 특히, `Products`를 참조하는 모든 위치가 강조 표시됩니다. 이는 이전 절차의 모든 참조 찾기 작업과 매우 비슷합니다. 위쪽 창의 아무 곳이나 클릭하고 아래쪽 창에서 녹색으로 강조 표시된 스크립트의 실제 변경 내용을 확인합니다.  
  
5.  **적용**을 클릭합니다.  
  
6.  테이블 디자이너나 Transact\-SQL 편집기에 이미 열려 있는 스크립트 파일의 경우 Transact\-SQL 편집기에서 변경이 발생한 위치가 강조 표시되고 그 왼쪽에 녹색 막대가 표시됩니다.  
  
7.  **솔루션 탐색기**에 **TradeDev.refactorlog**가 추가되었는지 확인합니다. 이 로그를 두 번 클릭하여 엽니다. 여기에는 이 세션의 모든 변경 내용에 대한 XML 표현이 포함되어 있습니다.  
  
8.  F5 키를 눌러 프로젝트를 빌드하고 로컬 데이터베이스에 배포합니다.  
  
9. **SQL Server 개체 탐색기**의 **로컬** 아래에서 **TradeDev** 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새로 고침**을 선택합니다.  
  
10. **테이블**을 확장하고 **Products** 테이블의 이름이 바뀌었는지 확인합니다.  
  
11. **Product**를 마우스 오른쪽 단추로 클릭하고 **데이터 보기**를 선택합니다. 기존 데이터가 이름 바꾸기 작업에 관계없이 그대로 유지되어 있는지 확인합니다.  
  
### <a name="to-expand-wildcards"></a>와일드카드를 확장하려면  
  
1.  **솔루션 탐색기**에서 **함수** 노드를 확장하고 **GetProductsBySupplier.sql**을 두 번 클릭합니다.  
  
2.  커서를 이 줄의 별표에 놓고 마우스 오른쪽 단추를 클릭합니다. **리팩터링** 및 **와일드카드 확장**을 선택합니다.  
  
    ```  
    SELECT * from Product p  
    ```  
  
3.  **변경 내용 미리 보기** 대화 상자의 위쪽 창에서 `SELECT * from Product p`를 클릭하여 강조 표시합니다.  
  
4.  아래의 **변경 내용 미리 보기** 창에서 스크립트의 `*`가 다음까지 확장되었는지 확인합니다.  
  
    ```  
    [Id], [Name], [ShelfLife], [SupplierId], [CustomerId]  
    ```  
  
5.  **적용** 단추를 클릭합니다.  확장 작업으로 변경된 내용이 포함된 줄이 다시 강조 표시되고 그 왼쪽에 녹색 막대가 표시됩니다.  
  
### <a name="to-fully-qualify-database-object-names"></a>데이터베이스 개체 이름을 정규화하려면  
  
1.  **GetProductsBySupplier.sql**이 여전히 Transact\-SQL 편집기에 열려 있는지 확인합니다.  
  
2.  커서를 이 줄의 `Product`에 놓고 마우스 오른쪽 단추를 클릭합니다. **리팩터링** 및 **이름 정규화**를 선택합니다.  
  
    ```  
    SELECT [Id], [Name], [ShelfLife], [SupplierId], [CustomerId] from Product p  
    ```  
  
3.  **변경 내용 미리 보기** 대화 상자에서 **적용** 단추를 클릭합니다.  모든 개체 참조가 업데이트되어 개체의 스키마 이름과 부모 이름(개체에 부모가 있는 경우)이 포함되었는지 확인합니다.  
  
    ```  
    SELECT [p].[Id], [p].[Name], [p].[ShelfLife], [p].[SupplierId], [p].[CustomerId] from [dbo].[Product] p  
    ```  
  
### <a name="to-move-schema"></a>스키마를 이동하려면  
  
1.  이동할 개체를 마우스 오른쪽 단추로 클릭합니다. **리팩터링** 및 **스키마 이동**을 선택합니다.  
  
2.  **새 스키마** 목록에서 개체를 이동할 대상 스키마의 이름을 클릭합니다. 확인을 클릭합니다.  
  
    **변경 내용 미리 보기** 확인란을 선택한 경우 **변경 내용 미리 보기** 대화 상자가 나타납니다. 그렇지 않으면 개체 이름이 업데이트되고 개체는 새 스키마로 이동합니다.  
  
