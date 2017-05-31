---
title: "FILESTREAM 데이터 저장용 테이블 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], table storage
ms.assetid: 029c3059-5c83-43e2-a859-9027031b7de1
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7dd390bcb61a1e8f320fb6aa3a4c0209dfab3d77
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-table-for-storing-filestream-data"></a>FILESTREAM 데이터 저장용 테이블 만들기
  이 항목에서는 FILESTREAM 데이터 저장용 테이블을 만드는 방법을 보여 줍니다.  
  
 데이터베이스에 FILESTREAM 파일 그룹이 있으면 FILESTREAM 데이터를 저장하는 테이블을 만들거나 수정할 수 있습니다. FILESTREAM 데이터를 포함하는 열을 지정하려면 **varbinary(max)** 열을 만들고 FILESTREAM 특성을 추가합니다.  
  
### <a name="to-create-a-table-to-store-filestream-data"></a>FILESTREAM 데이터를 저장할 테이블을 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **새 쿼리** 를 클릭하여 쿼리 편집기를 표시합니다.  
  
2.  다음 예에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 복사하여 쿼리 편집기에 붙여 넣습니다. 이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드는 Records라는 FILESTREAM 사용 테이블을 만듭니다.  
  
3.  테이블을 만들려면 **실행**을 클릭합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 `Records`라는 테이블을 만드는 방법을 보여 줍니다. `Id` 열은 `ROWGUIDCOL` 열로서 Win32 API에서 FILESTREAM 데이터를 사용하는 데 필요합니다. `SerialNumber` 열은 `UNIQUE INTEGER`입니다. `Chart` 열은 `FILESTREAM` 열로서 파일 시스템에 `Chart` 를 저장하는 데 사용됩니다.  
  
> [!NOTE]  
>  이 예제에서는 [FILESTREAM 사용 데이터베이스 만들기](../../relational-databases/blob/create-a-filestream-enabled-database.md)에서 만든 Archive 데이터베이스를 참조합니다.  
  
 [!code-sql[FILESTREAM#FS_CreateTable](../../relational-databases/blob/codesnippet/tsql/create-a-table-for-stori_1.sql)]  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
