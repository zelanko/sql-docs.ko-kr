---
title: FileTable DDL, 함수, 저장 프로시저 및 뷰 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], database objects
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8d1a084a53402f53b3e217ba7d3d17a9a67859f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65094366"
---
# <a name="filetable-ddl-functions-stored-procedures-and-views"></a>FileTable DDL, 함수, 저장 프로시저 및 뷰
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 FileTable 기능을 지원하기 위해 추가되거나 변경된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스 개체를 나열합니다.  
  
 다음 표의 상태 열은 항목이 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 신규 항목인지, 아니면 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 있었지만 의미 체계 검색을 지원하기 위해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 에서 변경되었는지를 나타냅니다.  
  
 FILESTREAM을 지원하는 문과 데이터베이스 개체의 목록은 [FILESTREAM DDL, Functions, Stored Procedures, and Views](../../relational-databases/blob/filestream-ddl-functions-stored-procedures-and-views.md)를 참조하세요.  
  
##  <a name="ddl"></a> Transact-SQL DDL(데이터 정의 언어) 문  
  
|Object|상태|추가 정보|  
|------------|------------|----------------------|  
|[ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)<br /><br /> [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)|변경됨|[FileTable의 필수 구성 요소를 사용하도록 설정](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)<br /><br /> [FileTable 관리](../../relational-databases/blob/manage-filetables.md)|  
|[ALTER TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|변경됨|[FileTable 만들기, 변경 및 삭제](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [FileTable 관리](../../relational-databases/blob/manage-filetables.md)|  
|[CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)|변경됨|[FileTable의 필수 구성 요소를 사용하도록 설정](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|변경됨|[FileTable 만들기, 변경 및 삭제](../../relational-databases/blob/create-alter-and-drop-filetables.md)|  
|[RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)<br /><br /> [RESTORE 인수&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)|변경됨||  
  
##  <a name="func"></a> 함수  
  
|Object|상태|추가 정보|  
|------------|------------|----------------------|  
|[FileTableRootPath&#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|**추가됨**|[FileTable에서 디렉터리 및 경로 작업](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath&#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|**추가됨**|[FileTable에서 디렉터리 및 경로 작업](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator&#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|**추가됨**|[FileTable에서 디렉터리 및 경로 작업](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="sproc"></a> 저장 프로시저  
  
|Object|상태|추가 정보|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)|**추가됨**|[FileTable 관리](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="cv"></a> 카탈로그 뷰  
  
|Object|상태|추가 정보|  
|------------|------------|----------------------|  
|[sys.database_filestream_options&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)|**추가됨**|[FileTable의 필수 구성 요소를 사용하도록 설정](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)|**추가됨**|[FileTable 만들기, 변경 및 삭제](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [FileTable 관리](../../relational-databases/blob/manage-filetables.md)|  
|[sys.filetables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)|**추가됨**|[FileTable 관리](../../relational-databases/blob/manage-filetables.md)|  
|[sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)|변경됨|[FileTable 관리](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="dmv"></a> 동적 관리 뷰  
  
|Object|상태|추가 정보|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)|**추가됨**|[FileTable 관리](../../relational-databases/blob/manage-filetables.md)|  
  
## <a name="see-also"></a>참고 항목  
 [FileTable 관리](../../relational-databases/blob/manage-filetables.md)  
  
  
