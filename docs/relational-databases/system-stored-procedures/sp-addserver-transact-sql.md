---
title: sp_addserver (Transact-sql) | Microsoft Docs
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
ms.openlocfilehash: 1d89da6675fba33af3c6e2d1c054273b6e420ec3
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78172289"
---
# <a name="sp_addserver-transact-sql"></a>sp_addserver(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스 이름을 정의합니다. 를 호스팅하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 컴퓨터의 이름이 변경 되 면 **sp_addserver** 를 사용 하 여 새 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 컴퓨터 이름에 대 한 인스턴스를 알립니다. 이 프로시저는 해당 컴퓨터에서 호스팅되는 모든 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 실행해야 합니다. 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스 이름은 변경할 수 없습니다. 명명된 인스턴스의 인스턴스 이름을 변경하려면 원하는 이름의 새 인스턴스를 설치하고 이전 인스턴스에서 데이터베이스 파일을 분리한 다음 새 인스턴스에 데이터베이스를 연결하고 이전 인스턴스를 삭제합니다. 또는 클라이언트 별칭 이름을 클라이언트 컴퓨터에서 만들어 서버 컴퓨터에서 인스턴스의 이름을 변경하지 않고 다른 서버 및 인스턴스 이름 또는 **서버:포트** 조합으로 연결을 리디렉션할 수 있습니다.

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```

sp_addserver [ @server = ] 'server' ,
     [ @local = ] 'local' 
     [ , [ @duplicate_ok = ] 'duplicate_OK' ]
```

## <a name="arguments"></a>인수
`[ @server = ] 'server'`서버 이름입니다. 서버 이름은 고유해야 하며 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 컴퓨터 이름에 관한 규칙을 준수해야 합니다. 단, 공백은 사용할 수 없습니다. *서버* 는 **sysname**이며 기본값은 없습니다.

 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 여러 개 설치되어 있으면 각 인스턴스는 별개의 서버에 있는 것처럼 작동합니다. *서버* 를 *servername\instancename*로 참조 하 여 명명 된 인스턴스를 지정 합니다.

`[ @local = ] 'LOCAL'`로컬 서버로 추가 되는 서버를 지정 합니다. local은 **varchar (10)** 이며 기본값은 NULL입니다. ** \@** Local ** \@as** **local** 을 지정 하면 ** \@server** 가 로컬 서버의 이름으로 정의 되 고 @@SERVERNAME 함수가 *서버*값을 반환 합니다.

 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 설치 중에 이 변수를 컴퓨터 이름으로 설정합니다. 기본적으로 이 컴퓨터 이름을 사용하면 추가 구성 없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있습니다.

 로컬 정의는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 다시 시작해야 적용됩니다. 각 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에서 로컬 서버는 하나만 정의할 수 있습니다.

`[ @duplicate_ok = ] 'duplicate_OK'`중복 된 서버 이름을 사용할 수 있는지 여부를 지정 합니다. duplicate_OK는 **varchar (13)** 이며 기본값은 NULL입니다. ** \@** duplicate_OK은 **duplicate_OK** 또는 NULL 값만 가질 수 있습니다. ** \@** **Duplicate_OK** 를 지정 하 고 추가 하려는 서버 이름이 이미 있는 경우 오류가 발생 하지 않습니다. 명명 된 매개 변수가 사용 되지 않는 경우 ** \@local** 을 지정 해야 합니다.

## <a name="return-code-values"></a>반환 코드 값
 0(성공) 또는 1(실패)

## <a name="remarks"></a>설명
 서버 옵션을 설정 하거나 해제 하려면 **sp_serveroption**을 사용 합니다.

 사용자 정의 트랜잭션 내에서는 **sp_addserver** 를 사용할 수 없습니다.

 원격 서버를 추가 하기 위해 **sp_addserver** 를 사용 하는 것은 중단 되지 않습니다. 대신 [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 를 사용 해야 합니다.

## <a name="permissions"></a>사용 권한
 
  **setupadmin** 고정 서버 역할의 멤버 자격이 필요합니다.

## <a name="examples"></a>예
 다음 예에서는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 를 호스팅하는 컴퓨터 이름의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 항목을 `ACCOUNTS`로 변경합니다.

```
sp_addserver 'ACCOUNTS', 'local';
```

## <a name="see-also"></a>참고 항목
 [&#41;&#40;sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) [SQL Server의 독립 실행형 인스턴스를 호스팅하는 컴퓨터의 이름을 바꿉니다](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md) . transact-sql sp_dropserver [&#40;&#41;transact-sql](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md) [Sp_helpserver &#40;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)&#41;Transact-sql &#40;[시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)&#41;transact-sql &#40;[보안 저장 프로시저](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)&#41;transact-sql


