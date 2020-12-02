---
description: SUSER_NAME(Transact-SQL)
title: SUSER_NAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUSER_NAME
- SUSER_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- identification names for logins [SQL Server]
- users [SQL Server], logins
- SUSER_NAME function
- logins [SQL Server], names
- names [SQL Server], logins
ms.assetid: ae598d9f-9baa-49b8-b1c1-042854206de4
author: VanMSFT
ms.author: vanto
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1044f594889c8d7a6698c0ffc5a09692ed734a47
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91379784"
---
# <a name="suser_name-transact-sql"></a>SUSER_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

사용자의 로그인 ID 이름을 반환합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
SUSER_NAME ( [ server_user_id ] )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
_server\_user\_id_  
사용자의 로그인 ID입니다. _server\_user\_id_ 는 선택 사항이며 **int** 입니다. _server\_user\_id_ 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있는 권한을 가진 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자나 그룹 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 로그인 ID 번호일 수 있습니다. _server\_user\_id_ 를 지정하지 않으면 현재 사용자에 대한 로그인 ID 이름이 반환됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다.  
  
## <a name="return-types"></a>반환 형식  
**nvarchar(128)**  
  
## <a name="remarks"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 7.0에서는 SUID(서버 사용자 ID) 대신 SID(보안 ID)가 사용됩니다.  
  
SUSER_NAME은 **syslogins** 시스템 테이블에 항목이 있는 로그인에 대해서만 로그인 이름을 반환합니다.  
  
SUSER_NAME은 SELECT 목록이나 WHERE 절, 그리고 식이 사용되는 모든 곳에 사용할 수 있습니다. 매개 변수를 지정하지 않더라도 SUSER_NAME 뒤에 괄호를 사용합니다.  

> [!NOTE]
> SUSER_NAME 함수는 Azure SQL Database에서 지원되지만, Azure SQL Database에서 SUSER_NAME과 함께 *Execute as* 를 사용할 수는 없습니다. 
  
## <a name="examples"></a>예제  
다음 예에서는 로그인 ID가 `1`인 사용자의 로그인 ID 이름을 반환합니다.  
  
```sql
SELECT SUSER_NAME(1);  
```  
  
## <a name="see-also"></a>관련 항목  
[SUSER_ID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-id-transact-sql.md)   
[보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
