---
description: sp_dropserver(Transact-SQL)
title: sp_dropserver (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropserver_TSQL
- sp_dropserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropserver
ms.assetid: 0fc83e35-0caa-49a3-a4b6-a1890d4f46ef
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017
ms.openlocfilehash: e3caee2593f6b02688ab82fcfd72686670c493dd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466814"
---
# <a name="sp_dropserver-transact-sql"></a>sp_dropserver(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 알려진 원격 서버 및 연결된 서버 목록에서 서버를 제거합니다.  
  
 ![링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql  
sp_dropserver [ @server = ] 'server'   
     [ , [ @droplogins = ] { 'droplogins' | NULL} ]  
```  
  
## <a name="arguments"></a>인수  
 *server*  
 제거할 서버입니다. *server* 은 **sysname** 이며 기본값은 없습니다. *서버* 가 있어야 합니다.  
  
 *droplogins*  
 **Droplogins** 가 지정 된 경우 *서버* 에 대 한 관련 원격 및 연결 된 서버 로그인도 제거 해야 함을 나타냅니다. **`@droplogins`** 는 **char (10)** 이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 연결 된 원격 및 연결 된 서버 로그인 항목이 있거나 복제 게시자로 구성 된 서버에서 **sp_dropserver** 를 실행 하는 경우 오류 메시지가 반환 됩니다. 서버를 제거할 때 서버에 대 한 모든 원격 및 연결 된 서버 로그인을 제거 하려면 **droplogins** 인수를 사용 합니다.  
  
 **sp_dropserver** 은 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 ALTER ANY LINKED SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 원격 서버 `ACCOUNTS`와 모든 연관된 원격 로그인을 제거합니다.  
  
```  
sp_dropserver 'ACCOUNTS', 'droplogins';  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_addserver &#40;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [Transact-sql&#41;sp_dropremotelogin &#40;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [Transact-sql&#41;sp_helpremotelogin &#40;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
