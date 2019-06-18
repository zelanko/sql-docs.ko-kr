---
title: FILESTREAM 사용 데이터베이스 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FILESTREAM-enabled databases
ms.assetid: 0fc16356-76f7-44b8-a58b-f0b7c43694ec
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 64f0c7006bdf5580eed6df4923ca13e8d11d33fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65094297"
---
# <a name="create-a-filestream-enabled-database"></a>FILESTREAM 사용 데이터베이스 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 FILESTREAM을 지원하는 데이터베이스를 만드는 방법을 보여 줍니다. FILESTREAM이 특별한 유형의 파일 그룹을 사용하므로 데이터베이스를 만들 때 하나 이상의 파일 그룹에 대해 CONTAINS FILESTREAM 절을 지정해야 합니다.  
  
 FILESTREAM 파일 그룹은 두 개 이상의 파일을 포함할 수 있습니다. 여러 파일을 포함하는 FILESTREAM 파일 그룹을 만드는 방법을 보여 주는 코드 예제는 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)를 참조하세요.  
  
### <a name="to-create-a-filestream-enabled-database"></a>FILESTREAM 사용 데이터베이스를 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **새 쿼리** 를 클릭하여 쿼리 편집기를 표시합니다.  
  
2.  다음 예에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 복사하여 쿼리 편집기에 붙여 넣습니다. 이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드는 Archive라는 FILESTREAM 사용 데이터베이스를 만듭니다.  
  
    > [!NOTE]  
    >  이 스크립트의 경우 C:\Data 디렉터리가 있어야 합니다.  
  
3.  데이터베이스를 작성하려면 **실행**을 클릭합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 `Archive`라는 데이터베이스를 만듭니다. 이 데이터베이스는 3개의 파일 그룹 `PRIMARY`, `Arch1`및 `FileStreamGroup1`을 포함합니다. `PRIMARY` 및 `Arch1` 은 FILESTREAM 데이터를 포함할 수 없는 일반 파일 그룹이고, `FileStreamGroup1` 은 `FILESTREAM` 파일 그룹입니다.  
  
 [!code-sql[FILESTREAM#FS_CreateDB](../../relational-databases/blob/codesnippet/tsql/create-a-filestream-enab_1.sql)]  
  
 `FILESTREAM` 은 `FILENAME` 파일 그룹의 경로를 참조합니다. 따라서 마지막 폴더 바로 위의 경로까지 있어야 하고 마지막 폴더 자체는 있으면 안 됩니다. 이 예제에서는 `c:\data` 가 있어야 합니다. 그러나 `filestream1` 문을 실행할 때 `CREATE DATABASE` 하위 폴더는 없어야 합니다. 구문에 대한 자세한 내용은 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)를 참조하세요.  
  
 위의 예를 실행하고 나면 c:\Data\filestream1 폴더에 filestream.hdr 파일과 $FSLOG 폴더가 나타납니다. filestream.hdr 파일은 FILESTREAM 컨테이너 헤더 파일입니다.  
  
> [!IMPORTANT]  
>  filestream.hdr 파일은 중요한 시스템 파일이므로 FILESTREAM 헤더 정보를 포함하고 있습니다. 이 파일은 제거하거나 수정하면 안 됩니다.  
  
 기존 데이터베이스의 경우 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문을 사용하여 FILESTREAM 파일 그룹을 추가할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
