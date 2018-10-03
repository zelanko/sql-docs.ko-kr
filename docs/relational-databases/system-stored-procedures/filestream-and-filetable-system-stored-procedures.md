---
title: Filestream 및 FileTable 시스템 저장 프로시저 (TRANSACT-SQL) | Microsoft Docs
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 79d01c66d26e15518f2acdb2babfa0fa805da536
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47842371"
---
# <a name="filestream-and-filetable-system-stored-procedures-transact-sql"></a>Filestream 및 FileTable 시스템 저장 프로시저 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  이 섹션에서는 Filestream 및 FileTable 기능에는 시스템 저장 프로시저를 설명 합니다.  

## <a name="filestream-and-filetable-system-stored-procedures"></a>Filestream 및 Filetable 시스템 저장 프로시저
  [sp_filestream_force_garbage_collection (TRANSACT-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)

   FILESTREAM 가비지 수집기를 실행하고 불필요한 FILESTREAM 파일을 삭제합니다.

  [sp_kill_filestream_non_transacted_handles (TRANSACT-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)

  FileTable 데이터에 대한 비트랜잭션 핸들 파일을 닫습니다.


## <a name="see-also"></a>참고자료
[Filestream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream 및 FileTable 동적 관리 뷰(Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 및 FileTable 카탈로그 뷰(Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
  
  
