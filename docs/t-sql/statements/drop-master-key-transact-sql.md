---
title: DROP MASTER KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP MASTER KEY
- DROP_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing Database Master Keys
- database master key [SQL Server], removing
- encryption [SQL Server], Database Master Key
- DROP MASTER KEY statement
- cryptography [SQL Server], Database Master Key
- dropping Database Master Keys
- deleting Database Master Keys
ms.assetid: 5ccef797-408f-4964-80da-965d8e1ccba7
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6722becf2b18b1c81576b6f3173be2474e94cc73
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044134"
---
# <a name="drop-master-key-transact-sql"></a>DROP MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  현재 데이터베이스에서 마스터 키를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DROP MASTER KEY  
```  
  
## <a name="arguments"></a>인수  
 이 문에는 인수가 필요하지 않습니다.  
  
## <a name="remarks"></a>Remarks  
 데이터베이스의 프라이빗 키가 마스터 키로 보호되면 삭제가 실패합니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks2012` 데이터베이스에서 마스터 키를 제거합니다.  
  
```  
USE AdventureWorks2012;  
DROP MASTER KEY;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 마스터 키를 제거합니다.  
  
```  
USE master;  
DROP MASTER KEY;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-master-key-transact-sql.md)   
 [RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

