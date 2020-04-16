---
title: OPENROWSET 대량 행 집합 공급자를 사용하여 대형 개체 데이터 대량 가져오기
description: SQL Server OPENROWSET 대량 행 집합 공급자를 사용하면 대형 개체 데이터로 대량 가져오기가 가능합니다. 지원되는 형식은 varbinary(max), varchar(max), nvarchar(max)입니다.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- SINGLE_NCLOB option
- bulk rowset providers [SQL Server]
- bulk importing [SQL Server], data formats
- OPENROWSET function, bulk importing large data
- SINGLE_CLOB option
- data formats [SQL Server], large-object data
- large data, bulk imports
- SINGLE_BLOB option
ms.assetid: 171cdd5c-1e47-4bd7-b99a-4f0fd4e10526
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: a91dbe991241e9cf837fe325a76fd0e1ae3242d7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80980511"
---
# <a name="bulk-import-large-object-data-with-openrowset-bulk-rowset-provider-sql-server"></a>OPENROWSET 대량 행 집합 공급자를 사용하여 대형 개체 데이터 대량 가져오기(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OPENROWSET 대량 행 집합 공급자를 사용하여 데이터 파일을 큰 개체 데이터로 대량으로 가져올 수 있습니다.  
  
 OPENROWSET 대량 행 집합 공급자에서 지원되는 큰 개체 데이터 형식은 **varbinary**(max) 또는 **image**, **varchar**(max) 또는 **text**, **nvarchar**(max) 또는 **ntext**입니다.  
  
> [!NOTE]  
>  **image**, **text** 및 **ntext** 데이터 형식은 사용되지 않습니다.  
  
 OPENROWSET BULK 절은 데이터 파일의 내용을 단일 행/단일 열로 된 행 집합으로 가져올 수 있는 3개의 옵션을 지원합니다. 서식 파일을 사용하는 대신 이 큰 개체 옵션 중 하나를 지정할 수 있습니다. 옵션은 다음과 같습니다.  
  
 SINGLE_BLOB  
 *data_file* 의 내용을 단일 행으로 읽은 후 **varbinary(max)** 형식의 단일 열로 된 행 집합으로 반환합니다.  
  
 SINGLE_CLOB  
 지정한 데이터 파일의 내용을 문자로 읽은 후 텍스트나 **Word 문서와 같은 현재 데이터베이스의 데이터 정렬을 사용하여**varchar(max) [!INCLUDE[msCoName](../../includes/msconame-md.md)] 형식의 단일 행/열로 된 행 집합으로 반환합니다.  
  
 SINGLE_NCLOB  
 지정한 데이터 파일의 내용을 유니코드로 읽은 후 현재 데이터베이스의 데이터 정렬을 사용하여 **nvarchar(max)** 형식의 단일 행/열로 된 행 집합으로 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [BULK INSERT 또는 OPENROWSET&#40;BULK...&#41;를 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)   
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
  
