---
title: '@@REMSERVER (Transact SQL) | Microsoft Docs'
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
- '@@REMSERVER'
- '@@REMSERVER_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], remote servers
- remote servers [SQL Server], logins
- '@@REMSERVER function'
ms.assetid: 0bb451a9-3866-4064-963d-b74a2f864049
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: fd32b0c7ebc6da51fe50787a8492d52928dd7d32
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40remserver-transact-sql"></a>& #x 40; & #x 40; REMSERVER (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 대신 연결된 서버 및 연결된 서버의 저장 프로시저를 사용하십시오.  
  
 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 서버의 이름이 로그인 레코드에 나타날 때 이 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
@@REMSERVER  
```  
  
## <a name="return-types"></a>반환 형식  
 **nvarchar (128)**  
  
## <a name="remarks"></a>주의  
 @@REMSERVER 은 프로시저가 실행 될 데이터베이스 서버의 이름을 확인 하는 저장된 프로시저를 사용 하도록 설정 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 원격 서버의 이름을 반환하는 `usp_CheckServer` 프로시저를 만듭니다.  
  
```  
CREATE PROCEDURE usp_CheckServer  
AS  
SELECT @@REMSERVER;  
```  
  
 다음 저장 프로시저는 `SEATTLE1` 로컬 서버에서 생성됩니다. 사용자는 `LONDON2` 원격 서버에 로그온하고 `usp_CheckServer`를 실행합니다.  
  
```  
EXEC SEATTLE1...usp_CheckServer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------------  
LONDON2  
```  
  
## <a name="see-also"></a>관련 항목:  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [원격 서버](../../database-engine/configure-windows/remote-servers.md)  
  
  

