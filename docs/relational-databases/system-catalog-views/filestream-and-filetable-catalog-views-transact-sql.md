---
title: Filestream 및 FileTable 카탈로그 뷰 (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 710ac16c93c725c17a0f8c83d15c81f2bc45a5ab
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724941"
---
# <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Filestream 및 FileTable 카탈로그 뷰(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 섹션에서는 FileTable 기능과 관련된 카탈로그 뷰에 대해 설명합니다.  
  
## <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Filestream 및 filetable 카탈로그 뷰 (TRANSACT-SQL)
 [sys.database_filestream_options&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)  
 사용하도록 설정된 FileTable의 FILESTREAM 데이터에 대한 비트랜잭션 액세스 수준과 관련된 정보를 표시합니다. SQL Server 인스턴스의 각 데이터베이스마다 하나씩의 행을 포함합니다.  
  
 [sys.filetable_system_defined_objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)  
 FileTable과 관련된 시스템 정의 개체의 목록을 표시합니다. 시스템 정의 개체마다 하나의 행을 포함합니다.  
  
 [sys.filetables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)  
 FileTable마다 하나의 행을 반환합니다. 상속 **sys.tables**합니다.  

## <a name="see-also"></a>관련 항목
[Filestream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream 및 FileTable 동적 관리 뷰(Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 및 FileTable 시스템 저장 프로시저(Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)
  
  
