---
description: sys.fn_helpcollations(Transact-SQL)
title: sys.fn_helpcollations (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_helpcollations
- fn_helpcollations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_helpcollations function
- collations [SQL Server], supported
- fn_helpcollations function
ms.assetid: b5082e81-1fee-4e2c-b567-5412eaee41c1
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016|| = azure-sqldw-latest ||=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f85aa0ff207a2748f755975ce61e69a6782f43e2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478984"
---
# <a name="sysfn_helpcollations-transact-sql"></a>sys.fn_helpcollations(Transact-SQL)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  지원 되는 모든 데이터 정렬 목록을 반환 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```
fn_helpcollations ()  
```  
  
## <a name="tables-returned"></a>반환된 테이블

 **fn_helpcollations** 는 다음 정보를 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|Name|**sysname**|표준 데이터 정렬 이름입니다.|  
|설명|**nvarchar(1000)**|데이터 정렬에 대한 설명입니다.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 Windows 데이터 정렬을 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지원 되는 Windows 데이터 정렬 전에 개발 된 데이터 정렬 (<80)의 제한 된 수 ()도 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 정렬은 이전 버전과의 호환성을 위해 계속 지원 되지만 새로운 개발 작업에는 사용할 수 없습니다. Windows 데이터 정렬에 대한 자세한 내용은 [Windows Collation Name &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)을 참조하세요. 데이터 정렬에 대한 자세한 내용은 [데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
## <a name="examples"></a>예

 다음 예에서는 `L` 문자로 시작하는 이진 정렬 방식의 모든 데이터 정렬 이름을 반환합니다.

> [!Note]
> Fn_helpcollations ()에 대 한 Azure Synapse Analytics 쿼리는 master 데이터베이스에서 실행 되어야 합니다.  
  
```sql  
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name like 'L%' AND Description LIKE '% binary sort';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Name                   Description  
 -------------------    ------------------------------------  
 Lao_100_BIN            Lao-100, binary sort  
 Latin1_General_BIN     Latin1-General, binary sort  
 Latin1_General_100_BIN Latin1-General-100, binary sort  
 Latvian_BIN            Latvian, binary sort  
 Latvian_100_BIN        Latvian-100, binary sort  
 Lithuanian_BIN         Lithuanian, binary sort  
 Lithuanian_100_BIN     Lithuanian-100, binary sort  
  
 (7 row(s) affected)  
 ```
  
## <a name="see-also"></a>참고 항목

[COLLATE&#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
[COLLATIONPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/collation-functions-collationproperty-transact-sql.md)  
[Azure Synapse Analytics에 대 한 데이터베이스 데이터 정렬 지원](https://azure.microsoft.com/blog/database-collation-support-for-azure-sql-data-warehouse-2)  
