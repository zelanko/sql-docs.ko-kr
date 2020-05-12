---
title: '@@MAX_CONNECTIONS(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 77b3acdd0ca96286d626d7b2d1b69514853c5b78
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82822840"
---
# <a name="x40x40max_connections-transact-sql"></a>&#x40;&#x40;MAX_CONNECTIONS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에서 허용되는 최대 동시 사용자 연결 수를 반환합니다. 반환된 연결 수는 반드시 현재 구성된 연결 수가 아니어도 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@MAX_CONNECTIONS  
```  
  
## <a name="return-types"></a>반환 형식  
 **integer**  
  
## <a name="remarks"></a>설명  
 허용되는 실제 사용자 연결 수는 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전과 애플리케이션 및 하드웨어의 제한에 따라 달라집니다.  
  
 연결 수를 줄이기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 구성하려면 **sp_configure**를 사용합니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [구성 함수](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [user connections 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
  
  
