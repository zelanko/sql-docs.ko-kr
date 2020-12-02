---
description: FILEPROPERTYEX (Transact-SQL)
title: FILEPROPERTYEX (Transact-SQL) | Microsoft Docs
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILEPROPERTYEX_TSQL
- FILEPROPERTYEX
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file properties
- displaying file properties
- file properties [SQL Server]
- FILEPROPERTYEX function
- file names [SQL Server], FILEPROPERTYEX
author: stevestein
ms.author: sstein
ms.openlocfilehash: 802963395caa096d6a5e26a506e45d7c282ea7cc
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128428"
---
# <a name="filepropertyex-transact-sql"></a>FILEPROPERTYEX (Transact-SQL)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  현재 데이터베이스의 파일 이름과 속성 이름이 지정되면 지정된 파일 이름 속성 값을 반환합니다. 현재 데이터베이스에 없는 파일 또는 존재하지 않는 확장 파일 속성에 대한 NULL을 반환합니다. 현재 확장된 파일 속성은 Azure Blob 스토리지에 있는 데이터베이스에만 적용됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
FILEPROPERTYEX ( name , property )  
```  
  
## <a name="arguments"></a>인수  
 *name*  
 속성 정보를 반환할 현재 데이터베이스에 관련된 파일 이름이 포함된 식입니다. *file_name* 은 **nchar (128)** 입니다.  
  
 *property*  
 반환할 파일 속성의 이름이 포함된 식입니다. *속성* 은 **varchar(128)** 이며 다음 값 중 하나일 수 있습니다.  


  
|값|Description|
|-----------|-----------------|  
|**BlobTier**|대상 Azure 페이지 Blob의 계층입니다. Azure 페이지 Blob 스토리지를 사용하는 표준 및 GeneralPurpose 데이터베이스에만 적용됩니다.|
|**AccountType**|스토리지 계정 유형은 BLOB 스토리지인지 파일 스토리지인지, 프리미엄 스토리지인지 표준 스토리지인지를 나타냅니다.|
|**IsInferredTier**|계층이 데이터 크기에 따라 증가할 수 있는 암시적(기호적) 계층인지 또는 명시적(고정) 계층인지를 나타냅니다.|
|**IsPageBlob**|대상 BLOB이 페이지 Blob인지 여부를 나타냅니다.|
  
## <a name="return-types"></a>반환 형식  
 **sql_variant**  
  
## <a name="remarks"></a>설명  
 *file_name* 은 **sys.master_files** 또는 **sys.database_files** 카탈로그 뷰의 **이름** 열에 해당됩니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 데이터베이스 파일의 설정 상태를 반환하는 방법을 보여 줍니다.
```sql
SELECT s.file_id,
       s.type_desc,
       s.name,
       FILEPROPERTYEX(s.name, 'BlobTier') AS BlobTier,
       FILEPROPERTYEX(s.name, 'AccountType') AS AccountType,
       FILEPROPERTYEX(s.name, 'IsInferredTier') AS IsInferredTier,
       FILEPROPERTYEX(s.name, 'IsPageBlob') AS IsPageBlob
FROM sys.database_files AS s
WHERE s.type_desc IN ('ROWS', 'LOG');
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
file_id  type_desc  name  BlobTier  AccountType  IsInferredTier  IsPageBlob
--------------------------------------------------------------------------------------
1     ROWS      data_0  P30  PremiumBlobStorage  0   1
2     LOG       log     P30  PremiumBlobStorage  0   1

(2 rows affected)
```  
  
## <a name="see-also"></a>참고 항목  
 [FILEGROUPPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/filegroupproperty-transact-sql.md)   
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_spaceused&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
