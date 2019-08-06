---
title: sp_prepexec (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexec
- sp_cursor_prepexec_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexec
ms.assetid: f9141850-a62b-43bf-8e46-b2f92b75ca56
author: stevestein
ms.author: sstein
ms.openlocfilehash: 670b64cb107610fe8b5506654b9e655b0da5fb16
ms.sourcegitcommit: bcc3b2c7474297aba17b7a63b17c103febdd0af9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794720"
---
# <a name="sp_prepexec-transact-sql"></a>sp_ prepexec(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  매개 변수가 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 준비 하 고 실행 합니다. sp_prepexec는 sp_prepare 및 sp_execute의 함수를 결합 합니다. 이 작업은 TDS (tabular data stream) 패킷에서 ID = 13에 의해 호출 됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_prepexec handle OUTPUT, params , stmt  
    [ , bound param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>인수  
 *handle*  
 는 생성 된 핸들 식별자입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *handle* 은 **int** 반환 값을 포함 하는 필수 매개 변수입니다.  
  
 *params*  
 매개 변수가 있는 문을 식별합니다. 변수의 매개 변수 정의는 문에서 매개 변수 표식을 대체 합니다. *params* 는 **ntext**, **nchar**또는 **nvarchar** 입력 값을 호출 하는 필수 매개 변수입니다. 문에 매개 변수가 없으면 NULL 값을 입력합니다.  
  
 *stmt*  
 커서 결과 집합을 정의합니다. *Stmt* 매개 변수는 필수 이며 **ntext**, **nchar**또는 **nvarchar** 입력 값에 대해를 호출 합니다.  
  
 *bound_param*  
 추가 매개 변수의 선택적 사용을 나타냅니다. *bound_param* 는 모든 데이터 형식의 입력 값을 호출 하 여 사용 중인 추가 매개 변수를 지정 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 간단한 문을 준비 하 고 실행 합니다.  
  
```  
Declare @Out int;  
EXEC sp_prepexec @Out output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name  
      FROM sys.databases  
      WHERE name=@P1 AND state_desc = @P2',   
          @P1 = 'tempdb', @P2 = 'ONLINE';   
EXEC sp_unprepare @Out;  
```  
  
## <a name="see-also"></a>참조  
 [sp_prepare &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_execute &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-execute-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
