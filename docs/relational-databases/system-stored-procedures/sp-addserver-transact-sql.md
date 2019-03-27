---
title: sp_addserver (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addserver
- sp_addserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addserver
- renaming servers
- machine names [SQL Server]
- computer names
ms.assetid: 160a6b29-5e80-44ab-80ec-77d4280f627c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab5c15d15c77688c06eedec1d54e82c7b8199380
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492931"
---
# <a name="spaddserver-transact-sql"></a>sp_addserver(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스 이름을 정의합니다. 때 호스팅하는 컴퓨터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 사용 하 여 이름을 바꿀 **sp_addserver** 의 인스턴스를 알리기 위해는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 새 컴퓨터 이름입니다. 이 프로시저는 해당 컴퓨터에서 호스팅되는 모든 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 실행해야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스 이름은 변경할 수 없습니다. 명명된 인스턴스의 인스턴스 이름을 변경하려면 원하는 이름의 새 인스턴스를 설치하고 이전 인스턴스에서 데이터베이스 파일을 분리한 다음 새 인스턴스에 데이터베이스를 연결하고 이전 인스턴스를 삭제합니다. 또는 클라이언트 별칭 이름을 클라이언트 컴퓨터에서 만들어 서버 컴퓨터에서 인스턴스의 이름을 변경하지 않고 다른 서버 및 인스턴스 이름 또는 **서버:포트** 조합으로 연결을 리디렉션할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addserver [ @server = ] 'server' ,  
     [ @local = ] 'local'   
     [ , [ @duplicate_ok = ] 'duplicate_OK' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @server = ] 'server'` 서버의 이름이입니다. 서버 이름은 고유해야 하며 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 컴퓨터 이름에 관한 규칙을 준수해야 합니다. 단, 공백은 사용할 수 없습니다. *server* 은 **sysname**이며 기본값은 없습니다.  
  
 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 여러 개 설치되어 있으면 각 인스턴스는 별개의 서버에 있는 것처럼 작동합니다. 참조 하 여 명명된 된 인스턴스를 지정 *server* 으로 *servername\instancename*합니다.  
  
`[ @local = ] 'LOCAL'` 지정 하는 로컬 서버로 추가할 서버입니다. **@local** 됩니다 **varchar(10)**, 기본값은 NULL입니다. 지정 **@local** 으로 **로컬** 정의 **@server** 원인을 확인 하 고 로컬 서버 이름으로는 @@SERVERNAME 값을 반환 하는 함수 *server*합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 설치 중에 이 변수를 컴퓨터 이름으로 설정합니다. 기본적으로 이 컴퓨터 이름을 사용하면 추가 구성 없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있습니다.  
  
 로컬 정의는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 다시 시작해야 적용됩니다. 각 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에서 로컬 서버는 하나만 정의할 수 있습니다.  
  
`[ @duplicate_ok = ] 'duplicate_OK'` 서버 이름 중복이 허용 되는지 여부를 지정 합니다. **@duplicate_OK** 됩니다 **varchar(13)**, 기본값은 NULL입니다. **@duplicate_OK** 값을 하나만 사용할 수 있습니다 **duplicate_OK** 또는 NULL입니다. 하는 경우 **duplicate_OK** 지정을 이미 추가 되는 서버 이름이 있으면 오류가 발생 하지 않습니다. 명명 된 매개 변수 사용 되지 않는 경우 **@local** 지정 해야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 를 설정 하거나 서버 옵션을 선택 취소 **sp_serveroption**합니다.  
  
 **sp_addserver** 사용자 정의 트랜잭션 내에서 사용할 수 없습니다.  
  
 사용 하 여 **sp_addserver** 원격 서버는 지원 되지 않는 추가 합니다. 대신 [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 를 사용하세요.  
  
## <a name="permissions"></a>사용 권한  
 **setupadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 를 호스팅하는 컴퓨터 이름의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 항목을 `ACCOUNTS`로 변경합니다.  
  
```  
sp_addserver 'ACCOUNTS', 'local';  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server의 독립 실행형 인스턴스를 호스팅하는 컴퓨터 이름 바꾸기](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)   
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_dropserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_helpserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [보안 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
