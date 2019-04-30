---
title: OPENROWSET 대량 행 집합 공급자 (SQL Server)를 사용 하 여 큰 개체 데이터를 대량 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 441c13a725b69d70b4267ec90d7eaeeace2b3070
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140641"
---
# <a name="bulk-import-large-object-data-by-using-the-openrowset-bulk-rowset-provider-sql-server"></a>OPENROWSET 대량 행 집합 공급자를 사용하여 큰 개체 데이터 대량 가져오기(SQL Server)
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
  
## <a name="see-also"></a>관련 항목  
 [BULK INSERT 또는 OPENROWSET&#40;BULK...&#41;를 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [대량 가져오기 수행 중 Null 유지 또는 기본값 사용&#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)   
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)  
  
  
