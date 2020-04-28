---
title: 병합 게시에서 데이터를 테이블로 대량 로드 (복제 Transact-sql 프로그래밍) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- bulk load [SQL Server replication]
- merge replication bulk loading [SQL Server replication]
- sp_addtabletocontents
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 09e535057fcf573dfa189b7e5fdc0e0df06e5d4a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62721765"
---
# <a name="bulk-load-data-into-tables-in-a-merge-publication-replication-transact-sql-programming"></a>병합 게시에서 데이터를 테이블로 대량 로드(복제 Transact-SQL 프로그래밍)
  [bcp 유틸리티](../../tools/bcp-utility.md) 또는 [BULK INSERT](/sql/t-sql/statements/bulk-insert-transact-sql) 명령을 사용하여 데이터를 테이블로 로드할 경우 기본적으로 [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql) 시스템 테이블의 추적 데이터를 유지 관리하는 병합 복제 트리거가 발생하지 않습니다. 데이터가 로드될 때 병합 복제 트리거가 강제로 발생하도록 하거나 복제 저장 프로시저를 사용하여 대량 복사 작업을 수행한 후 생성된 복제 메타데이터를 프로그래밍 방식으로 삽입할 수 있습니다.  
  
### <a name="to-bulk-load-data-into-tables-published-by-merge-replication-using-the-bcp-utility"></a>bcp 유틸리티를 사용하여 병합 복제를 통해 게시된 테이블로 데이터를 대량으로 로드하려면  
  
1.  게시자나 구독자에서 [bcp Utility](../../tools/bcp-utility.md) 또는 [BULK INSERT](/sql/t-sql/statements/bulk-insert-transact-sql) 를 실행하여 병합 복제를 통해 게시된 테이블에 데이터를 삽입합니다.  
  
2.  다음 방법 중 하나를 사용하여 삽입된 데이터에 대한 복제 메타데이터가 생성되도록 합니다.  
  
    -   FIRE_TRIGGERS 옵션을 사용하여 대량 복사를 실행합니다.  
  
    -   데이터가 삽입된 데이터베이스에서 [sp_addtabletocontents&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql)를 실행합니다. 데이터가 삽입 된 테이블 이름을 지정 **@table_name**합니다.  
  
  
