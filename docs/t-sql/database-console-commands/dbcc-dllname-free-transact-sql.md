---
title: DBCC dllname(FREE)(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- dbcc_dllname_(FREE)_TSQL
- dllname
- dbcc dllname (FREE)
- FREE
- dbcc_dllname(FREE)_TSQL
- FREE_TSQL
- dllname_TSQL
- dbcc dllname(FREE)
dev_langs:
- TSQL
helpviewer_keywords:
- DLL unloading [SQL Server]
- DBCC dllname (FREE)
- freeing DLLs
- unloading DLLs
ms.assetid: 1eb71c17-fe15-430b-8916-e4e312dcf9c0
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: a7c52da362443dabaf6e9ee4782cdabe82e20fb8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840080"
---
# <a name="dbcc-dllname-free-transact-sql"></a>DBCC dllname(FREE)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
지정된 확장 저장 프로시저 DLL을 메모리에서 언로드합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
```sql
DBCC <dllname> ( FREE ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>인수  
 \<*dllname*>  
 메모리에서 해제할 DLL의 이름입니다.  
  
 WITH NO_INFOMSGS  
 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="remarks"></a>Remarks
확장 저장 프로시저를 실행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 로드한 DLL은 서버가 종료될 때까지 그대로 유지됩니다. 이 문은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 종료하지 않아도 메모리에서 DLL을 언로드할 수 있도록 허용합니다. 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 로드한 DLL 파일을 표시하려면 **sp_helpextendedproc**를 실행하십시오.
  
## <a name="result-sets"></a>결과 집합  
유효한 DLL을 지정하면 DBCC *dllname*(FREE)이 다음을 반환합니다.
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
**sysadmin** 고정 서버 역할의 멤버 또는 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.
  
## <a name="examples"></a>예  
다음 예에서는 `xp_sample`을 xp_sample.dll로 구현하고 실행했다고 가정합니다. DBCC \<*dllname*>(FREE)은 `xp_sample` 확장 프로시저와 연결된 xp_sample.dll 파일을 언로드합니다.
  
```sql  
DBCC xp_sample (FREE);  
```  
  
## <a name="see-also"></a>참고 항목  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[확장 저장 프로시저의 실행 특징](../../relational-databases/extended-stored-procedures-programming/execution-characteristics-of-extended-stored-procedures.md)  
[sp_addextendedproc&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)  
[sp_dropextendedproc&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
[sp_helpextendedproc&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)  
[확장 저장 프로시저 DLL 언로드](../../relational-databases/extended-stored-procedures-programming/unloading-an-extended-stored-procedure-dll.md)
  
  
