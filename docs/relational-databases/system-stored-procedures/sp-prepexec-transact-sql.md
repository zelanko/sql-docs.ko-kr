---
title: sp_prepexec (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexec
- sp_cursor_prepexec_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexec
ms.assetid: f9141850-a62b-43bf-8e46-b2f92b75ca56
caps.latest.revision: 6
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a6af0534ef82b09032d3c34ee8e1e5b377428be0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spprepexec-transact-sql"></a>sp_ prepexec(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  준비 및 실행 매개 변수가 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문. sp_prepexec은 sp_prepare 및 sp_execute의 기능을 결합합니다. TDS(Tabular Data Stream) 패킷에서 ID =13을 사용하여 호출합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_prepexec handle OUTPUT, params , stmt  
    [ , bound param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>인수  
 *handle*  
 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-생성 된 *처리* 식별자입니다. *처리* 은 필수 매개 변수는 **int** 값을 반환 합니다.  
  
 *params*  
 매개 변수가 있는 문을 식별합니다. *params* 문에 매개 변수 표식에 대 한 변수 정의 바뀝니다. *params* 필요로 하는 필수 매개 변수는 **ntext**, **nchar**, 또는 **nvarchar** 값을 입력 합니다. 문에 매개 변수가 없으면 NULL 값을 입력합니다.  
  
 *stmt*  
 커서 결과 집합을 정의합니다. *stmt* 호출에 대 한 필수 매개 변수 이며 프로그램 **ntext**, **nchar** 또는 **nvarchar** 값을 입력 합니다.  
  
 *bound_param*  
 추가 매개 변수의 선택적 사용을 나타냅니다. *bound_param* 사용 중인 추가 매개 변수를 지정 하려면 모든 데이터 형식의 입력된 값을 필요로 합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 간단한 문을 준비하고 실행합니다.  
  
```  
Declare @P1 int;  
EXEC sp_prepexec @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name  
      FROM sys.databases  
      WHERE name=@P1 AND state_desc = @P2',   
@P1 = 'tempdb', @P2 = 'ONLINE';   
EXEC sp_unprepare @P1;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_execute &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
