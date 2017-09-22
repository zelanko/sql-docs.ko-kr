---
title: '@@SPID (Transact SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@SPID'
- '@@SPID_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SPID function'
- session_id
- server process IDs [SQL Server]
- IDs [SQL Server], user processes
- SPID
- session IDs [SQL Server]
- process ID of current user process
ms.assetid: df955d32-8194-438e-abee-387eebebcbb7
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: db822ff8405a24981def755f49844a8ff7b789c2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40spid-transact-sql"></a>& #x 40; & #x 40; SPID (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 사용자 프로세스의 세션 ID를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
@@SPID  
```  
  
## <a name="return-types"></a>반환 형식  
 **smallint**  
  
## <a name="remarks"></a>주의  
 @@SPID 의 출력에 현재 사용자 프로세스를 식별 하는 데 사용 될 **sp_who**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 사용자 프로세스의 세션 ID, 로그인 이름 및 사용자 이름을 반환합니다.  
  
```  
SELECT @@SPID AS 'ID', SYSTEM_USER AS 'Login Name', USER AS 'User Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ID     Login Name                     User Name                       
------ ------------------------------ ------------------------------  
54     SEATTLE\joanna                 dbo                             
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 이 예제에서는 반환 된 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] 세션 ID는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 노드 세션 ID, 로그인 이름 및 현재 사용자 프로세스에 대 한 사용자 이름을 제어 합니다.  
  
```  
SELECT SESSION_ID() AS ID, @@SPID AS 'Control ID', SYSTEM_USER AS 'Login Name', USER AS 'User Name';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [구성 함수](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_lock&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
  


