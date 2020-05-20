---
title: sys. sp_rda_reconcile_columns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_reconcile_columns
- sys.sp_rda_reconcile_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_columns stored procedure
ms.assetid: 60d9cc4e-1828-450b-9d88-5b8485800d73
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8410cde58d5f6bcf6b2a48fcc7169210a41afe0a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814687"
---
# <a name="syssp_rda_reconcile_columns-transact-sql"></a>sys. sp_rda_reconcile_columns (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  원격 Azure 테이블의 열을 스트레치 사용 SQL Server 테이블의 열로 조정 합니다.  
    
  **Sp_rda_reconcile_columns** 확장 가능 SQL Server 테이블에 있지만 원격 테이블에는 없는 열을 원격 테이블에 추가 합니다. 이러한 열은 원격 테이블에서 실수로 삭제 한 열 일 수 있습니다. 그러나 **sp_rda_reconcile_columns** 는 원격 테이블에는 있지만 SQL Server 테이블에는 없는 열은 삭제 하지 않습니다.
  
  > [!IMPORTANT]
  > **sp_rda_reconcile_columns** 가 원격 테이블에서 실수로 삭제한 열을 다시 만드는 경우 이전에 삭제된 열에 있었던 데이터를 복원하지 않습니다.
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>구문  
  
```  
  
sp_rda_reconcile_columns @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>인수  
 \@objname = '* \@ objname*'  
 스트레치 사용 SQL Server 테이블의 이름입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0 (성공) 또는 >0 (실패)  
  
## <a name="permissions"></a>권한  
 Db_owner 권한이 필요 합니다.  
   
## <a name="remarks"></a>설명  
 스트레치 지원 SQL Server 테이블에 더 이상 존재하지 않는 열이 원격 Azure 테이블에 있는 경우 이러한 추가 열 때문에 Stretch Database가 제대로 작동하지 않는 것은 아닙니다. 필요에 따라 추가 열을 수동으로 제거할 수 있습니다.  
  
## <a name="example"></a>예제  
 원격 Azure 테이블의 열을 조정 하려면 다음 문을 실행 합니다.  
  
```sql  
EXEC sp_rda_reconcile_columns @objname = N'StretchEnabledTableName';  
```  
  
  
