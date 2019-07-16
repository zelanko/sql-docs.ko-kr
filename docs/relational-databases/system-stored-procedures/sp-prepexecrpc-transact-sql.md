---
title: sp_prepexecrpc (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexecrpc
- sp_cursor_prepexecrpc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexecrpc
ms.assetid: 35d686f2-ef31-4eaa-baa9-9cef5d6c87c2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6fea210183ae67179dcc6f686e25f939cd00713b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056329"
---
# <a name="spprepexecrpc-transact-sql"></a>sp_prepexecrpc(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  RPC 식별자를 사용하여 지정된 매개 변수가 있는 저장 프로시저 호출을 준비 및 실행합니다. sp_prepexecrpc ID를 호출한 = 14 tabular data TDS (stream) 패킷에서를 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_prepexecrpc handle OUTPUT, RPCCall  
    [ , bound_param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>인수  
 *handle*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 생성하는 준비된 핸들 식별자입니다. *처리할* 은 필수 매개 변수를 **int** 값을 반환 합니다.  
  
 *RPCCall*  
 ODBC 정식 구문을 사용하여 저장 프로시저를 정의합니다. *RPCCall* 필요로 하는 필수 매개 변수를 **ntext** 문자열 값을 입력 합니다.  
  
 *bound_param*  
 추가 매개 변수의 선택적 사용을 나타냅니다. *bound_param* 사용 중인 추가 매개 변수를 지정 하려면 모든 데이터 형식의 입력된 값에 대 한 호출 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
