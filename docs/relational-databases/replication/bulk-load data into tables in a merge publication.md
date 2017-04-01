---
title: "병합 게시에서 데이터를 테이블로 대량 로드(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "대량 로드 [SQL Server 복제]"
  - "병합 복제 대량 로드 [SQL Server 복제]"
  - "sp_addtabletocontents"
ms.assetid: 16e6498a-b449-4051-aec4-ea814a2ad993
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 병합 게시에서 데이터를 테이블로 대량 로드(복제 Transact-SQL 프로그래밍)
  데이터를 사용 하 여 테이블에 로드 하는 경우는 [bcp 유틸리티](../../tools/bcp-utility.md) 또는 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 의 추적 데이터를 유지 관리 하는 병합 복제 트리거를 기본적으로 명령에 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) 시스템 테이블 발생 하지 않습니다. 데이터가 로드될 때 병합 복제 트리거가 강제로 발생하도록 하거나 복제 저장 프로시저를 사용하여 대량 복사 작업을 수행한 후 생성된 복제 메타데이터를 프로그래밍 방식으로 삽입할 수 있습니다.  
  
### bcp 유틸리티를 사용하여 병합 복제를 통해 게시된 테이블로 데이터를 대량으로 로드하려면  
  
1.  게시자나 구독자에서 [bcp Utility](../../tools/bcp-utility.md) 또는 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 를 실행하여 병합 복제를 통해 게시된 테이블에 데이터를 삽입합니다.  
  
2.  다음 방법 중 하나를 사용하여 삽입된 데이터에 대한 복제 메타데이터가 생성되도록 합니다.  
  
    -   FIRE_TRIGGERS 옵션을 사용하여 대량 복사를 실행합니다.  
  
    -   데이터 삽입 된 데이터베이스에서 실행 [sp_addtabletocontents (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addtabletocontents-transact-sql.md)합니다. 에 대 한 데이터가 삽입 된 테이블 이름을 지정 **@table_name**합니다.  
  
  