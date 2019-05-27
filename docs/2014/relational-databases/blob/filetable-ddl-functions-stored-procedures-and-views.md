---
title: FileTable DDL, 함수, 저장 프로시저 및 뷰 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], database objects
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 85e0c761f5dc784698b3aed361ce50488a93e366
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66010097"
---
# <a name="filetable-ddl-functions-stored-procedures-and-views"></a>FileTable DDL, 함수, 저장 프로시저 및 뷰
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 FileTable 기능을 지원하기 위해 추가되거나 변경된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스 개체를 나열합니다.  
  
 다음 표의 상태 열은 항목이 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 신규 항목인지, 아니면 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 있었지만 의미 체계 검색을 지원하기 위해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 에서 변경되었는지를 나타냅니다.  
  
 FILESTREAM을 지원하는 문과 데이터베이스 개체의 목록은 [FILESTREAM DDL, Functions, Stored Procedures, and Views](../views/views.md)를 참조하세요.  
  
##  <a name="ddl"></a> Transact-SQL DDL(데이터 정의 언어) 문  
  
|Object|상태|추가 정보|  
|------------|------------|----------------------|  
|[ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)<br /><br /> [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)|변경됨|[FileTable의 필수 구성 요소를 사용하도록 설정](enable-the-prerequisites-for-filetable.md)<br /><br /> [FileTable 관리](manage-filetables.md)|  
|[ALTER TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)|변경됨|[FileTable 만들기, 변경 및 삭제](create-alter-and-drop-filetables.md)<br /><br /> [FileTable 관리](manage-filetables.md)|  
|[CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)|변경됨|[FileTable의 필수 구성 요소를 사용하도록 설정](enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)|변경됨|[FileTable 만들기, 변경 및 삭제](create-alter-and-drop-filetables.md)|  
|[RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)<br /><br /> [RESTORE 인수&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)|변경됨||  
  
##  <a name="func"></a> 함수  
  
|Object|상태|추가 정보|  
|------------|------------|----------------------|  
|[FileTableRootPath&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/filetablerootpath-transact-sql)|**추가됨**|[FileTable에서 디렉터리 및 경로 작업](work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql)|**추가됨**|[FileTable에서 디렉터리 및 경로 작업](work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator&#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/getpathlocator-transact-sql)|**추가됨**|[FileTable에서 디렉터리 및 경로 작업](work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="sproc"></a> 저장 프로시저  
  
|Object|상태|추가 정보|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles)|**추가됨**|[FileTable 관리](manage-filetables.md)|  
  
##  <a name="cv"></a> 카탈로그 뷰  
  
|Object|상태|추가 정보|  
|------------|------------|----------------------|  
|[sys.database_filestream_options&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql)|**추가됨**|[FileTable의 필수 구성 요소를 사용하도록 설정](enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql)|**추가됨**|[FileTable 만들기, 변경 및 삭제](create-alter-and-drop-filetables.md)<br /><br /> [FileTable 관리](manage-filetables.md)|  
|[sys.filetables&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetables-transact-sql)|**추가됨**|[FileTable 관리](manage-filetables.md)|  
|[sys.tables&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|변경됨|[FileTable 관리](manage-filetables.md)|  
  
##  <a name="dmv"></a> 동적 관리 뷰  
  
|Object|상태|추가 정보|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql)|**추가됨**|[FileTable 관리](manage-filetables.md)|  
  
## <a name="see-also"></a>관련 항목  
 [FileTable 관리](manage-filetables.md)  
  
  
