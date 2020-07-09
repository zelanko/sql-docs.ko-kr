---
title: FILEPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILEPROPERTY_TSQL
- FILEPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file properties
- names [SQL Server], files
- displaying file properties
- file properties [SQL Server]
- FILEPROPERTY function
- file names [SQL Server], FILEPROPERTY
ms.assetid: b82244ed-d623-431f-aa06-8017349d847f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 518751aa443d2a2a93843fb79c5bcfdd2196db08
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882637"
---
# <a name="fileproperty-transact-sql"></a>FILEPROPERTY(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스의 파일 이름과 속성 이름이 지정되면 지정된 파일 이름 속성 값을 반환합니다. 현재 데이터베이스에 없는 파일에 대해서는 NULL을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
FILEPROPERTY ( file_name , property )  
```  
  
## <a name="arguments"></a>인수  
 *file_name*  
 속성 정보를 반환할 현재 데이터베이스에 관련된 파일 이름이 포함된 식입니다. *file_name*은 **nchar (128)** 입니다.  
  
 *property*  
 반환할 파일 속성의 이름이 포함된 식입니다. *속성*은 **varchar(128)** 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|반환 값|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|파일 그룹이 읽기 전용입니다.|1 = True<br /><br /> 0 = False<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsPrimaryFile**|파일이 주 파일입니다.|1 = True<br /><br /> 0 = False<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**IsLogFile**|파일이 로그 파일입니다.|1 = True<br /><br /> 0 = False<br /><br /> NULL = 입력이 잘못되었습니다.|  
|**SpaceUsed**|지정된 파일이 사용하는 공간의 크기입니다.|파일에 할당된 페이지 수|  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>설명  
 *file_name*은 **sys.master_files** 또는 **sys.database_files** 카탈로그 뷰의 **이름** 열에 해당됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `IsPrimaryFile` 데이터베이스에 있는 `AdventureWorks_Data` 파일 이름에 대한 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 속성의 설정을 반환합니다.  
  
```  
  
SELECT FILEPROPERTY('AdventureWorks2012_Data', 'IsPrimaryFile')AS [Primary File];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Primary File   
-------------  
1  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>참고 항목  
 [FILEGROUPPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/filegroupproperty-transact-sql.md)   
 [메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_spaceused&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.database_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
