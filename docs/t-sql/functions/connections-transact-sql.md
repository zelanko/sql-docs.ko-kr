---
title: '@@CONNECTIONS (Transact SQL) | Microsoft Docs'
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
- '@@CONNECTIONS'
- '@@CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@CONNECTIONS function'
- connections [SQL Server], number of
- connections [SQL Server], attempted
- number of connection attempts
- attempted connections
ms.assetid: c59836a8-443c-4b9a-8b96-8863ada97ac7
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: d70742d1afeed9148a0118d928797ca529f05cdc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40connections-transact-sql"></a>&#x40;&#x40;연결 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

마지막으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 시작한 후 시도한 연결 수를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
@@CONNECTIONS  
```  
  
## <a name="return-types"></a>반환 형식
**integer**
  
## <a name="remarks"></a>주의  
연결은 사용자와 다릅니다. 예를 들어 응용 프로그램은 연결을 관찰하는 사용자 없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와의 연결 여러 개를 열 수 있습니다.
  
몇 가지를 포함 하는 보고서를 표시 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통계를 실행 하는 연결 시도 포함 하 여 **sp_monitor**합니다.
  
@@MAX_CONNECTIONS 서버에 동시에 허용 되는 연결의 최대 수입니다. @@CONNECTIONS 증가 각 로그인 시도와 따라서 @@CONNECTIONS 보다 클 수 @@MAX_CONNECTIONS 합니다.
  
## <a name="examples"></a>예  
다음 예에서는 현재 날짜 및 시간의 로그인 시도 수를 반환합니다.
  
```sql
SELECT GETDATE() AS 'Today''s Date and Time',   
@@CONNECTIONS AS 'Login Attempts';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
  
Today's Date and Time  Login Attempts  
---------------------- --------------  
12/5/2006 10:32:45 AM  211023         
```  
  
## <a name="see-also"></a>참고 항목
[시스템 통계 함수 &#40; Transact SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
[sp_monitor &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)
  
  

