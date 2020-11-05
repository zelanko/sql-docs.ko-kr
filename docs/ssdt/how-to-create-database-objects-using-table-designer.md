---
title: 테이블 디자이너를 사용하여 데이터베이스 개체 만들기
description: SQL Server 개체 탐색기에서 새 데이터베이스를 만드는 방법을 알아봅니다. 테이블 디자이너에서 새 테이블, 제약 조건 및 외래 키 참조를 만드는 방법을 확인합니다.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.design.table.scriptpanel
- sql.data.tools.design.table.context.view
- Microsoft.Data.Relational.Design.PW.RelationshipsDescriptor.OnDelete
ms.assetid: 9c9479c1-9bfc-4039-837e-e53fce67723d
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 410b2674f407018b895ed84781bedf5fa8766feb
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364395"
---
# <a name="how-to-create-database-objects-using-table-designer"></a>방법: 테이블 디자이너를 사용하여 데이터베이스 개체 만들기

**SQL Server 개체 탐색기** 의 새 **SQL Server** 노드는 시각적으로 SSMS와 매우 비슷할 뿐만 아니라 SSMS와 비슷하게 동작하는 상황에 맞는 메뉴를 사용하여 새 개체를 만들 수도 있습니다.  
  
예를 들어 **데이터베이스** 노드 아래에 새 데이터베이스를 만들 수 있습니다. 마찬가지로 특정 데이터베이스를 선택하고 새 테이블 디자이너를 사용하여 즉시 테이블 정의와 관련 프로그래밍 개체를 만들거나 편집할 수 있습니다. 테이블 디자이너에서 이 테이블을 정의하는 스크립트를 직접 편집할 수 있는 스크립트 창으로 전환할 수도 있습니다.  
  
### <a name="to-create-a-new-database"></a>새 데이터베이스를 만들려면  
  
1.  **SQL Server 개체 탐색기** 의 **SQL Server** 노드에서 연결된 서버 인스턴스를 확장합니다.  
  
2.  **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭하고 **새 데이터베이스 추가** 를 선택합니다.  
  
3.  새 데이터베이스의 이름을 **Trade** 로 바꿉니다.  
  
### <a name="to-create-new-tables-using-the-table-designer"></a>테이블 디자이너를 사용하여 새 테이블을 만들려면  
  
1.  새로 만든 **Trade** 노드를 확장합니다. **테이블** 노드를 마우스 오른쪽 단추로 클릭하고 **새 테이블 추가** 를 선택합니다.  
  
2.  테이블 디자이너가 새 창에서 열립니다. 이 디자이너는 열 표, 스크립트 창 및 컨텍스트 창으로 구성되어 있습니다. 열 표에는 테이블의 모든 열이 나열됩니다. 디자이너의 다른 구성 요소는 이후 절차에서 설명합니다.  
  
3.  스크립트 창에서 새 테이블의 이름을 `Suppliers`로 바꿉니다. 예를 들어 아래 코드를  
  
    ```  
    CREATE TABLE [dbo].[Table1]  
    ```  
  
    다음과 같이 바꿉니다.  
  
    ```  
    CREATE TABLE [dbo].[Suppliers]  
    ```  
  
4.  열 표의 빈 행을 클릭하여 테이블에 새 열을 추가합니다.  **이름** 필드에 **CompanyName** 을 입력하고 **데이터 형식** 에 **nvarchar(128)** 을 입력한 후 **Null 허용** 필드의 선택을 취소합니다. Tab 키로 필드 바깥쪽으로 이동하면 스크립트 창이 즉시 업데이트됩니다.  
  
5.  다른 새 열을 추가합니다. **이름** 필드에 **Address** 를 입력하고 **데이터 형식** 에 **nvarchar(MAX)** 을 입력한 후 **Null 허용** 필드의 선택을 취소합니다.  
  
    > [!WARNING]  
    > 연결된 데이터베이스의 개체를 편집하는 경우에는 변경 내용을 로컬 드라이브에 저장하지 마십시오. 데이터베이스의 변경 내용을 올바르게 저장하려면 다음에 나오는 [방법: 파워 버퍼를 사용하여 연결된 데이터베이스 업데이트](../ssdt/how-to-update-a-connected-database-with-power-buffer.md) 절차의 단계를 따릅니다.  
  
6.  위의 단계를 반복하여 **Customer** 라는 다른 테이블을 만듭니다. 이번에는 열 표를 사용하여 Customer 테이블에 다음 열을 추가 합니다. 그런 다음, 테이블의 이름이 `[dbo].[Customer]`가 되도록 스크립트를 변경해야 합니다.  
  
    |Name|데이터 형식|**Null 허용**|  
    |--------|-------------|-------------------|  
    |Id|int|선택 취소|  
    |Name|nvarchar(128)|선택 취소|  
  
7.  **Products** 라는 테이블을 하나 이상 만듭니다. 열 표를 사용하여 Products 테이블에 다음 열을 추가 합니다. 그런 다음, 테이블의 이름이 `[dbo].[Products]`가 되도록 스크립트를 변경해야 합니다.  
  
    |Name|데이터 형식|**Null 허용**|  
    |--------|-------------|-------------------|  
    |Id|int|선택 취소|  
    |Name|nvarchar(128)|선택 취소|  
    |ShelfLife|int|선택|  
    |SupplierId|int|선택|  
    |CustomerId|int|선택|  
  
### <a name="to-create-a-new-check-constraint-using-the-table-designer"></a>테이블 디자이너를 사용하여 새 CHECK 제약 조건을 만들려면  
  
1.  테이블 디자이너의 컨텍스트 창에는 키, 인덱스, 제약 조건, 트리거 등의 테이블 정의에 대한 논리 뷰가 제공되며, 이 창에서 개체를 선택하여 개별 열과의 관계를 강조 표시할 수 있습니다.  
  
    Products 테이블에 대해 테이블 디자이너의 컨텍스트 창에서 **CHECK 제약 조건** 노드를 마우스 오른쪽 단추로 클릭하고 **새 CHECK 제약 조건 추가** 를 선택합니다.  
  
2.  노드 수는 자동으로 1씩 증가합니다.  
  
3.  스크립트 창을 클릭하고 제약 조건의 기본 정의를 다음과 같이 바꿉니다.  
  
    ```  
    CONSTRAINT [CK_Products_ShelfLife] CHECK ([ShelfLife] <5),  
    ```  
  
    이 제약 조건은 행의 ShelfLife 값을 5 미만으로 제한합니다.  
  
### <a name="to-create-new-foreign-key-references-using-the-table-designer"></a>테이블 디자이너를 사용하여 새 외래 키 참조를 만들려면  
  
1.  Products 테이블에 대해 컨텍스트 창의 **외래 키** 노드를 마우스 오른쪽 단추로 클릭하고 **새 외래 키 추가** 를 선택합니다.  
  
2.  노드 수는 자동으로 1씩 증가합니다.  
  
3.  스크립트 창을 클릭하고 외래 키 참조의 기본 정의를 다음과 같이 바꿉니다.  
  
    ```  
    CONSTRAINT [FK_Products_SupplierId] FOREIGN KEY ([SupplierId]) REFERENCES [dbo].[Suppliers] ([Id]),  
    ```  
  
4.  위의 단계를 반복하여 Products 테이블에 다른 외래 키 참조를 추가합니다. 이번에는 기본 정의를 다음과 같이 바꿉니다.  
  
    ```  
    CONSTRAINT [FK_Products_CustomerId] FOREIGN KEY ([CustomerId]) REFERENCES [dbo].[Customer] ([Id])  
    ```  
  
## <a name="see-also"></a>참고 항목  
[테이블 및 관계 관리, 오류 해결](../ssdt/manage-tables-relationships-and-fix-errors.md)  
  
