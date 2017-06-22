---
title: "인덱스 이름 바꾸기 | Microsoft 문서"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- renaming indexes
- index names [SQL Server]
- indexes [SQL Server], renaming
ms.assetid: d3d612a1-ea1b-4d99-85d2-0a2ad54f4b0e
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 59c77e43b02e26626c280f6325cdb67a11021db9
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="rename-indexes"></a>인덱스 이름 바꾸기
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 인덱스 이름을 바꾸는 방법에 대해 설명합니다. 인덱스 이름을 바꾸면 현재 인덱스 이름이 새 이름으로 바뀝니다. 지정된 이름은 테이블 또는 뷰에서 고유해야 합니다. 예를 들어 **XPK_1**이라는 인덱스가 두 테이블에 있을 수는 있지만 동일한 테이블에 **XPK_1**이라는 인덱스가 두 개 있을 수는 없습니다. 기존의 비활성 인덱스와 동일한 이름의 인덱스는 만들 수 없습니다. 인덱스 이름을 바꾼다고 인덱스가 다시 작성되는 것은 아닙니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **인덱스 이름을 바꾸려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Restrictions"></a> 제한 사항  
 테이블에서 PRIMARY KEY 또는 UNIQUE 제약 조건을 만들 때 제약 조건과 이름이 같은 인덱스가 테이블에 자동으로 만들어집니다. 인덱스 이름은 테이블에서 고유해야 하므로 테이블에서 기존의 PRIMARY KEY 또는 UNIQUE 제약 조건과 같은 이름으로 인덱스를 만들거나 인덱스 이름을 같은 이름으로 바꿀 수 없습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 인덱스에 대한 ALTER 사용 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-rename-an-index-by-using-the-table-designer"></a>테이블 디자이너를 사용하여 인덱스 이름을 바꾸려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 인덱스 이름을 바꿀 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  인덱스 이름을 바꿀 테이블을 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.  
  
4.  **테이블 디자이너** 메뉴에서 **인덱스/키**를 클릭합니다.  
  
5.  **선택한 기본/고유 키 또는 인덱스** 입력란에서 이름을 바꿀 인덱스를 선택합니다.  
  
6.  표에서 **이름** 을 클릭하고 새 이름을 입력란에 입력합니다.  
  
7.  **닫기**를 클릭합니다.  
  
8.  **파일** 메뉴에서 *table name* **저장**을 클릭합니다.  
  
#### <a name="to-rename-an-index-by-using-object-explorer"></a>개체 탐색기를 사용하여 인덱스 이름을 바꾸려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 인덱스 이름을 바꿀 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 인덱스 이름을 바꿀 테이블을 확장합니다.  
  
4.  더하기 기호를 클릭하여 **인덱스** 폴더를 확장합니다.  
  
5.  이름을 바꿀 인덱스를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택합니다.  
  
6.  인덱스의 새 이름을 입력하고 Enter 키를 누릅니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-rename-an-index"></a>인덱스 이름을 바꾸려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Renames the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table to IX_VendorID.   
  
    EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';   
    GO  
    ```  
  
 자세한 내용은 [sp_rename&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)을 참조하세요.  
  
  

