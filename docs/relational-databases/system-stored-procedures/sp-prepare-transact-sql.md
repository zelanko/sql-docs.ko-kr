---
title: sp_prepare (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepare
ms.assetid: f328c9eb-8211-4863-bafa-347e1bf7bb3f
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 38093990d6b011113ca63764cb43a08c664c7fe5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spprepare-transact-sql"></a>sp_prepare(Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  매개 변수가 있는 준비 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 문을 반환 하 고 *처리* 실행 합니다. sp_prepare가 ID를 지정 하 여 호출 = 표 형식 데이터 TDS (stream) 패킷의 11입니다.  
  
 ![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_prepare handle OUTPUT, params, stmt, options  
```  
  
## <a name="arguments"></a>인수  
 *handle*  
 SQL Server에서 생성 *준비 된 핸들* 식별자입니다. *처리* 은 필수 매개 변수는 **int** 값을 반환 합니다.  
  
 *params*  
 매개 변수가 있는 문을 식별합니다. *params* 문에 매개 변수 표식에 대 한 변수 정의 바뀝니다. *params* 필요로 하는 필수 매개 변수는 **ntext**, **nchar**, 또는 **nvarchar** 값을 입력 합니다. 문에 매개 변수가 없으면 NULL 값을 입력합니다.  
  
 *stmt*  
 커서 결과 집합을 정의합니다. *stmt* 호출에 대 한 필수 매개 변수 이며 프로그램 **ntext**, **nchar**, 또는 **nvarchar** 값을 입력 합니다.  
  
 *options*  
 커서 결과 집합 열의 설명을 반환하는 선택적 매개 변수입니다. *옵션* 다음 int 입력된 값을 필요로 합니다.  
  
|Value|Description|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
## <a name="examples"></a>예  
 다음 예제에서는 간단한 문을 준비하고 실행합니다.  
  
```  
Declare @P1 int;  
Exec sp_prepare @P1 output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name=@P1 AND state_desc = @P2';  
Exec sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```  

  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

