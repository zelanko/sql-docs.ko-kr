---
title: '@@MAX_CONNECTIONS (Transact SQL) | Microsoft Docs'
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
- '@@MAX_CONNECTIONS'
- '@@MAX_CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- simultaneous connections [SQL Server]
- maximum number of simultaneous user connections
- '@@MAX_CONNECTIONS function'
- connections [SQL Server], simultaneous
- number of simultaneous user connections
ms.assetid: 57eb9f4b-548f-4212-9684-a11d831c4732
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 29910f9bc06335c4df10acf7663bfef92edffce2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40maxconnections-transact-sql"></a>& #x 40; & #x 40; MAX_CONNECTIONS (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에서 허용되는 최대 동시 사용자 연결 수를 반환합니다. 반환된 연결 수는 반드시 현재 구성된 연결 수가 아니어도 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@MAX_CONNECTIONS  
```  
  
## <a name="return-types"></a>반환 형식  
 **integer**  
  
## <a name="remarks"></a>주의  
 허용되는 실제 사용자 연결 수는 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전과 응용 프로그램 및 하드웨어의 제한에 따라 달라집니다.  
  
 다시 구성 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 적은 수의 연결에 대 한 사용 하 여 **sp_configure**합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 최대 사용자 연결 수를 반환합니다. 이 예에서는 사용자 연결 수를 줄이기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 구성하지 않은 것으로 가정합니다.  
  
```  
SELECT @@MAX_CONNECTIONS AS 'Max Connections';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Max Connections  
---------------  
32767            
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [구성 함수](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [user connections 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
  
  

