---
title: FILESTREAM 사용 데이터베이스 이동 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], moving a FILESTREAM-enabled database
ms.assetid: dd4d270d-9283-431a-aa6b-e571fced1893
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1e0638477dd826f2023c3728bedb2a6f846ef305
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529805"
---
# <a name="move-a-filestream-enabled-database"></a>FILESTREAM 사용 데이터베이스 이동
  이 항목에서는 FILESTREAM 사용 데이터베이스를 이동하는 방법을 보여 줍니다.  
  
> [!NOTE]  
>  이 항목의 예제에는 [FILESTREAM 사용 데이터베이스 만들기](create-a-filestream-enabled-database.md)에서 만들어진 Archive 데이터베이스가 필요합니다.  
  
### <a name="to-move-a-filestream-enabled-database"></a>FILESTREAM 사용 데이터베이스를 이동하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **새 쿼리** 를 클릭하여 쿼리 편집기를 엽니다.  
  
2.  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 쿼리 편집기에 복사한 다음 **실행**을 클릭합니다. 이 스크립트는 FILESTREAM 데이터베이스에서 사용하는 실제 데이터베이스 파일의 위치를 표시합니다.  
  
    ```sql  
    USE Archive  
    GO  
    SELECT type_desc, name, physical_name from sys.database_files  
    ```  
  
3.  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 쿼리 편집기에 복사한 다음 **실행**을 클릭합니다. 이 코드는 `Archive` 데이터베이스를 오프라인 상태로 만듭니다.  
  
    ```sql  
    USE master  
    EXEC sp_detach_db Archive  
    GO  
    ```  
  
4.  `C:\moved_location`이라는 폴더를 만든 다음 2단계에 나와 있는 파일과 폴더를 이 폴더로 이동합니다.  
  
5.  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 쿼리 편집기에 복사한 다음 **실행**을 클릭합니다. 이 스크립트는 `Archive` 데이터베이스를 온라인 상태로 설정합니다.  
  
    ```sql  
    CREATE DATABASE Archive ON  
    PRIMARY ( NAME = Arch1,  
        FILENAME = 'c:\moved_location\archdat1.mdf'),  
    FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = Arch3,  
        FILENAME = 'c:\moved_location\filestream1')  
    LOG ON  ( NAME = Archlog1,  
        FILENAME = 'c:\moved_location\archlog1.ldf')  
    FOR ATTACH  
    GO  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [sp_detach_db&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)  
  
  
