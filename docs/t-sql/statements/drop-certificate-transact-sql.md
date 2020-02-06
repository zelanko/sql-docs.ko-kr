---
title: DROP CERTIFICATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/18/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP CERTIFICATE
- DROP_CERTIFICATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], removing
- removing certificates
- dropping certificates
- DROP CERTIFICATE statement
- deleting certificates
ms.assetid: 5704aa04-68a3-4b29-b62b-8868af487817
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2ea8b8b77ac4445bc40bea2a2dcc9359de0f6a09
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67898273"
---
# <a name="drop-certificate-transact-sql"></a>DROP CERTIFICATE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  데이터베이스에서 인증서를 제거합니다.  
  
> [!IMPORTANT]  
>  데이터베이스에 암호화를 사용할 수 없는 경우에도 데이터 암호화에 사용되는 인증서의 백업을 보관해야 합니다. 데이터베이스가 더 이상 암호화되지 않더라도 트랜잭션 로그 부분은 그대로 보호될 수 있으며, 일부 작업의 경우 데이터베이스 전체 백업을 수행할 때까지는 인증서가 필요할 수 있습니다. 데이터베이스 암호화 시 생성된 백업에서 복원하려면 인증서도 필요합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DROP CERTIFICATE certificate_name  
```  
  
## <a name="arguments"></a>인수  
 *certificate_name*  
 데이터베이스에서 인증서를 식별하는 고유한 이름입니다.  
  
## <a name="remarks"></a>설명  
 연결된 엔터티가 없는 인증서만 삭제할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 인증서에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Shipping04` 데이터베이스에서 `AdventureWorks` 인증서를 삭제합니다.  
  
```  
USE AdventureWorks2012;  
DROP CERTIFICATE Shipping04;  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>예제: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 다음 예에서는 `Shipping04`인증서를 삭제합니다.  
  
```
USE master;  
DROP CERTIFICATE Shipping04;  
```  
  
## <a name="see-also"></a>참고 항목  
 [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
