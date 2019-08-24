---
title: SET REMOTE_PROC_TRANSACTIONS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- REMOTE_PROC_TRANSACTIONS_TSQL
- SET REMOTE_PROC_TRANSACTIONS
- REMOTE_PROC_TRANSACTIONS
- SET_REMOTE_PROC_TRANSACTIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote stored procedures [SQL Server]
- SET REMOTE_PROC_TRANSACTIONS statement
- distributed transactions [SQL Server], starting
- REMOTE_PROC_TRANSACTIONS option
- active transactions
ms.assetid: 4d284ae9-3f5f-465a-b0dd-1328a4832a03
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0d94799898517b2d75ce6a1add308f0831b112ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132820"
---
# <a name="set-remote_proc_transactions-transact-sql"></a>SET REMOTE_PROC_TRANSACTIONS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로컬 트랜잭션이 활성 트랜잭션일 때 원격 저장 프로시저를 실행하면 MS DTC([!INCLUDE[tsql](../../includes/tsql-md.md)] Distributed Transaction Manager)에서 관리하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 분산 트랜잭션이 시작되도록 지정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 이 옵션은 원격 저장 프로시저를 사용하는 애플리케이션에 대해 이전 버전과의 호환성을 위해 제공됩니다. 원격 저장 프로시저 호출을 실행하는 대신 연결된 서버를 참조하는 분산 쿼리를 사용합니다. 이러한 분산 쿼리는 [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)를 사용하여 정의됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
SET REMOTE_PROC_TRANSACTIONS { ON | OFF }   
```  
  
## <a name="arguments"></a>인수  
 ON | OFF  
 ON으로 설정하면 로컬 트랜잭션에서 원격 저장 프로시저를 실행할 때 [!INCLUDE[tsql](../../includes/tsql-md.md)] 분산 트랜잭션이 시작됩니다. OFF로 설정하면 로컬 트랜잭션에서 원격 저장 프로시저를 호출해도 [!INCLUDE[tsql](../../includes/tsql-md.md)] 분산 트랜잭션이 시작되지 않습니다.  
  
## <a name="remarks"></a>Remarks  
 REMOTE_PROC_TRANSACTIONS 옵션을 ON으로 설정할 경우 원격 저장 프로시저를 호출하면 분산 트랜잭션이 시작되고 MS DTC를 사용해 이 트랜잭션을 참여시킵니다. 원격 저장 프로시저를 호출하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 트랜잭션 주관자이며 트랜잭션의 완료를 제어합니다. 이후 연결에 대해 COMMIT TRANSACTION 또는 ROLLBACK TRANSACTION 문을 실행하면 제어 인스턴스는 MS DTC에서 관련 컴퓨터 간의 분산 트랜잭션 완료를 관리하도록 요청합니다.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 분산 트랜잭션이 시작되면 원격 서버로 정의된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 인스턴스에 대해 원격 저장 프로시저를 호출할 수 있습니다. 원격 서버를 모두 [!INCLUDE[tsql](../../includes/tsql-md.md)] 분산 트랜잭션에 참여시키고 MS DTC는 각 원격 서버에 대해 트랜잭션이 완료되도록 합니다.  
  
 REMOTE_PROC_TRANSACTIONS는 인스턴스 수준의 **sp_configure remote proc trans** 옵션보다 우선 적용하는 데 사용할 수 있는 연결 수준 설정입니다.  
  
 REMOTE_PROC_TRANSACTIONS 옵션을 OFF로 설정하면 원격 저장 프로시저가 로컬 트랜잭션의 일부로 호출되지 않습니다. 원격 저장 프로시저에서 수정한 내용은 저장 프로시저가 완료될 때 커밋되거나 롤백됩니다. 이후 원격 저장 프로시저를 호출한 연결에서 실행한 COMMIT TRANSACTION이나 ROLLBACK TRANSACTION 문은 프로시저에서 완료한 처리에 영향을 주지 않습니다.  
  
 REMOTE_PROC_TRANSACTIONS 옵션은 **sp_addserver**를 사용하여 원격 서버로 정의된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 호출되는 원격 저장 프로시저에만 영향을 주는 호환성 옵션입니다. 이 옵션은 **sp_addlinkedserver**를 사용하여 연결된 서버로 정의된 인스턴스에서 저장 프로시저를 실행하는 분산 쿼리에는 적용되지 않습니다.  
  
 SET REMOTE_PROC_TRANSACTIONS 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [BEGIN DISTRIBUTED TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
