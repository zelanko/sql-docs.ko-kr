---
title: 충돌 방지 - FILESTREAM 데이터베이스 작업 | Microsoft Docs
description: FILESTREAM 애플리케이션에서 데이터베이스 작업과의 충돌 방지
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Win32 and Transact-SQL Conflicts
ms.assetid: 8b1ee196-69af-4f9b-9bf5-63d8ac2bc39b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7b347a140c07436553945555e52d212e4751fcc4
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255577"
---
# <a name="avoid-conflicts-with-database-operations-in-filestream-applications"></a>FILESTREAM 애플리케이션에서 데이터베이스 작업과의 충돌 방지
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  FILESTREAM BLOB 데이터를 읽거나 쓰기 위해 SqlOpenFilestream()을 사용하여 Win32 파일 핸들을 여는 애플리케이션은 공통된 트랜잭션에서 관리되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과의 충돌 오류가 발생할 수 있습니다. 여기에는 실행 시간이 오래 걸리는 MARS 쿼리 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 이 포함됩니다. 이러한 유형의 충돌을 방지하도록 애플리케이션을 신중하게 디자인해야 합니다.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 또는 애플리케이션이 FILESTREAM BLOB를 열려고 하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 연결된 트랜잭션 컨텍스트를 확인합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 열기 작업이 DDL 문, DML 문, 데이터 검색 또는 트랜잭션 관리 등을 사용하는지에 따라 요청을 허용하거나 거부합니다. 다음 표에서는 트랜잭션에서 열려 있는 파일 유형에 따라 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 허용 또는 거부할지를 결정하는 방법을 보여 줍니다.  
  
|Transact-SQL 문|읽기 권한으로 열림|쓰기 권한으로 열림|  
|------------------------------|---------------------|----------------------|  
|CREATE TABLE, CREATE INDEX, DROP TABLE 및 ALTER TABLE과 같은 데이터베이스 메타데이터를 사용하는 DDL 문|허용됨|차단되고 시간 초과 오류가 발생합니다.|  
|UPDATE, DELETE 및 INSERT와 같이 데이터베이스에 저장된 데이터를 사용하는 DML 문|허용됨|거부됨|  
|SELECT|허용됨|허용됨|  
|COMMIT TRANSACTION|거부됨*|거부됨*|  
|SAVE TRANSACTION|거부됨*|거부됨*|  
|ROLLBACK|허용됨*|허용됨*|  
  
 \* 트랜잭션이 취소되고 트랜잭션 컨텍스트의 열린 핸들이 무효화됩니다. 애플리케이션은 열려 있는 모든 핸들을 닫아야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 및 FILESTREAM Win32 액세스 권한이 충돌을 발생시키는 방법을 보여 줍니다.  
  
### <a name="a-opening-a-filestream-blob-for-write-access"></a>A. 쓰기 권한으로 FILESTREAM BLOB 열기  
 다음 예에서는 쓰기 전용 권한으로 파일을 열었을 때 미치는 영향을 보여 줍니다.  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//Write some date to the FILESTREAM BLOB.  
WriteFile(dstHandle, updateData, ...);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed. The FILESTREAM BLOB is  
//returned without the modifications that are made by  
//WriteFile(dstHandle, updateData, ...).  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed. The FILESTREAM BLOB  
//is returned with the updateData applied.  
```  
  
### <a name="b-opening-a-filestream-blob-for-read-access"></a>B. 읽기 권한으로 FILESTREAM BLOB 열기  
 다음 예에서는 읽기 전용 권한으로 파일을 열었을 때 미치는 영향을 보여 줍니다.  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed. Any changes that are  
//made to the FILESTREAM BLOB will not be returned until  
//the dstHandle is closed.  
//SELECT statements will be allowed.  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="c-opening-and-closing-multiple-filestream-blob-files"></a>C. 여러 FILESTREAM BLOB 파일 열기 및 닫기  
 여러 파일이 열린 경우 가장 제한적인 규칙이 사용됩니다. 다음 예에서는 두 파일을 엽니다. 첫 번째 파일은 읽기 권한으로 열리고 두 번째 파일은 쓰기 권한으로 열립니다. 두 번째 파일이 열리기 전까지 DML 문은 거부됩니다.  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
  
dstHandle1 =  OpenSqlFilestream(dstFilePath1, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
//Close the read handle. The write handle is still open.  
CloseHandle(dstHandle);  
//DML statements are still denied because the write handle is open.  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
CloseHandle(dstHandle1);  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="d-failing-to-close-a-cursor"></a>D. 커서 닫기 실패  
 다음 예에서는 닫히지 않은 문 커서가 `OpenSqlFilestream()` 에서 쓰기 권한으로 BLOB를 열지 못하게 하는 방법을 보여 줍니다.  
  
```  
TCHAR *sqlDBQuery =  
TEXT("SELECT GET_FILESTREAM_TRANSACTION_CONTEXT(),")  
TEXT("Chart.PathName() FROM Archive.dbo.Records");  
  
//Execute a long-running Transact-SQL statement. Do not allow  
//the statement to complete before trying to  
//open the file.  
  
SQLExecDirect(hstmt, sqlDBQuery, SQL_NTS);  
  
//Before you call OpenSqlFilestream() any open files  
//that the Cursor the Transact-SQL statement is using  
// must be closed. In this example,  
//SQLCloseCursor(hstmt) is not called so that  
//the transaction will indicate that there is a file  
//open for reading. This will cause the call to  
//OpenSqlFilestream() to fail because the file is  
//still open.  
  
HANDLE srcHandle =  OpenSqlFilestream(srcFilePath,  
     Write, 0,  transactionToken,  cbTransactionToken,  0);  
  
//srcHandle will == INVALID_HANDLE_VALUE because the  
//cursor is still open.  
```  
  
## <a name="see-also"></a>참고 항목  
 [OpenSqlFilestream을 사용하여 FILESTREAM 데이터 액세스](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [MARS&#40;Multiple Active Result Sets&#41; 사용](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
  
  
