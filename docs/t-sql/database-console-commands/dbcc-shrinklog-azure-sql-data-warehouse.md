---
title: DBCC SHRINKLOG(병렬 데이터 웨어하우스) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d2cf30f4f01a30d8171e58cce3052e45fefa6179
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67930312"
---
# <a name="dbcc-shrinklog-parallel-data-warehouse"></a>DBCC SHRINKLOG(병렬 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

현재 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스에 대한 *어플라이언스에서* 트랜잭션 로그의 크기를 줄입니다. 트랜잭션 로그를 축소하기 위해 데이터를 조각 모음합니다. 시간이 지남에 따라 데이터베이스 트랜잭션 로그가 조각화되고 비효율적일 수 있습니다. DBCC SHRINKLOG를 사용하여 조각화를 줄이고 로그 크기를 줄입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC SHRINKLOG   
    [ ( SIZE = { target_size [ MB | GB | TB ]  } | DEFAULT ) ]   
    [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>인수  
SIZE = { *target_size* [ MB | **GB** | TB ]  } | **DEFAULT**.  
*target_size*는 DBCC SHRINKLOG 완료 후 모든 컴퓨팅 노드에 있는 트랜잭션 로그에 대해 원하는 크기입니다. 0보다 큰 정수여야 합니다.  
로그 크기는 MB(메가바이트), GB(기가바이트) 또는 TB(테라바이트) 단위로 측정됩니다. 모든 컴퓨팅 노드의 트랜잭션 노드에 대한 결합된 크기입니다.  
기본적으로 DBCC SHRINKLOG는 트랜잭션 로그를 데이터베이스에 대한 메타데이터에 저장된 로그 크기로 줄입니다. 메타데이터의 로그 크기는 [CREATE DATABASE&#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) 또는 [ALTER DATABASE&#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)의 LOG_SIZE 매개 변수에 따라 결정됩니다. `SIZE=DEFAULT`가 지정되거나 `SIZE` 절이 생략된 경우, DBCC SHRINKLOG는 트랜잭션 로그 크기를 기본 크기로 줄입니다.
  
WITH NO_INFOMSGS  
정보 메시지는 DBCC SHRINKLOG 결과에 표시되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
ALTER SERVER STATE 권한이 필요합니다.
  
## <a name="general-remarks"></a>일반적인 주의 사항  
DBCC SHRINKLOG는 데이터베이스에 대한 메타데이터에 저장된 로그 크기를 변경하지 않습니다. 메타데이터는 CREATE DATABASE 또는 ALTER DATABASE 문에 지정된 LOG_SIZE 매개 변수를 계속 포함합니다.
  
## <a name="examples"></a>예 
### <a name="a-shrink-the-transaction-log-to-the-original-size-specified-by-create-database"></a>A. CREATE DATABASE로 지정된 원래 크기로 트랜잭션 로그를 축소합니다.  
트랜잭션 로그에 대해 주소 데이터베이스를 만들 때 주소 데이터베이스를 100MB로 설정했다고 가정합니다. 즉, 주소에 대한 CREATE DATABASE 문이 LOG_SIZE = 100MB입니다. 이제, 로그가 150MB로 증가했으며 다시 100MB로 축소하려고 합니다.
  
다음 명령문들은 각각 주소 데이터베이스에 대한 트랜잭션 로그를 100MB의 기본 크기로 축소하려고 합니다. 로그를 100MB로 축소하여 데이터가 손실될 경우, DBCC SHRINKLOG는 데이터 손실 없이 로그를 100MB 이하의 가능한 가장 작은 크기로 축소합니다.
  
```sql
USE Addresses;  
DBCC SHRINKLOG ( SIZE = 100 MB );  
DBCC SHRINKLOG ( SIZE = DEFAULT );  
DBCC SHRINKLOG;  
```  
  
  
