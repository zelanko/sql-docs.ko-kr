---
title: SUSER_NAME (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a8d4eae9424d5c5cb2dbb2e7851d4e660fa0ba72
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="susername-transact-sql"></a>SUSER_NAME(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  사용자의 로그인 ID 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SUSER_NAME ( [ server_user_id ] )   
```  
  
## <a name="arguments"></a>인수  
 *server_user_id*  
 사용자의 로그인 ID입니다. *server_user_id*는 선택 사항이 며 **int**합니다. *server_user_id* id 일 수 있습니다는 로그인의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 또는 그룹의 인스턴스에 연결할 수 있는 권한을 가진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 경우 *server_user_id* 은 지정 하지 않으면 현재 사용자에 대 한 로그인 id 이름을 반환 됩니다. 매개 변수에 NULL이라는 단어가 포함되어 있으면 NULL이 반환됩니다.  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar (128)**  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 7.0에서는 SUID(서버 사용자 ID) 대신 SID(보안 ID)가 사용됩니다.  
  
 SUSER_NAME에 항목이 있는 로그인에 대 한 로그인 이름을 반환는 **syslogins** 시스템 테이블입니다.  
  
 SUSER_NAME은 WHERE 절의 SELECT 목록 및 식 어디에나 사용될 수 있으며 매개 변수를 지정하지 않아도 항상 뒤에 괄호가 와야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 로그인 ID가 `1`인 사용자의 로그인 ID 이름을 반환합니다.  
  
```  
SELECT SUSER_NAME(1);  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SUSER_ID &#40; Transact SQL &#41;](../../t-sql/functions/suser-id-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

