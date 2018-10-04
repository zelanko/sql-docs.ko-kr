---
title: sp_dropserver (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: b486237208e5a374d5cae6da6fd82a22ee0ebe18
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47658871"
---
# <a name="spdropserver-transact-sql"></a>sp_dropserver(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 알려진 원격 서버 및 연결된 서버 목록에서 서버를 제거합니다.  
  
 ![링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql  
sp_dropserver [ @server = ] 'server'   
     [ , [ @droplogins = ] { 'droplogins' | NULL} ]  
```  
  
## <a name="arguments"></a>인수  
 *server*  
 제거할 서버입니다. *server* 은 **sysname**이며 기본값은 없습니다. *서버* 존재 해야 합니다.  
  
 *droplogins*  
 원격 및 연결 된 서버 로그인에 대 한 관련 있는 여부를 나타냅니다 *서버* 경우에 제거 해야 **droplogins** 지정 됩니다. **`@droplogins`** 됩니다 **char(10)**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 실행 하는 경우 **sp_dropserver** 원격 및 연결 된 서버 로그인 항목이 연결 된 또는 복제 게시자로 구성 되는 서버에서 오류 메시지가 반환 됩니다. 서버를 제거 하는 경우 서버에 대 한 모든 원격 및 연결 된 서버 로그인을 제거 하려면 사용 합니다 **droplogins** 인수입니다.  
  
 **sp_dropserver** 사용자 정의 트랜잭션 내에서 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 ALTER ANY LINKED SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 원격 서버 `ACCOUNTS`와 모든 연관된 원격 로그인을 제거합니다.  
  
```  
sp_dropserver 'ACCOUNTS', 'droplogins';  
```  
  
## <a name="see-also"></a>관련 항목  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
