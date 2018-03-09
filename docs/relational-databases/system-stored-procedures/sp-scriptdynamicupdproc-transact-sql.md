---
title: sp_scriptdynamicupdproc (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_scriptdynamicupdproc_TSQL
- sp_scriptdynamicupdproc
helpviewer_keywords: sp_scriptdynamicupdproc
ms.assetid: b4c18863-ed92-4aa2-a04f-7ed832fc9e07
caps.latest.revision: "24"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 89a2704f20a2bdea0bb015d0280492dc594057da
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spscriptdynamicupdproc-transact-sql"></a>sp_scriptdynamicupdproc(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  동적 업데이트 저장 프로시저를 만드는 CREATE PROCEDURE 문을 생성합니다. 사용자 지정 저장 프로시저 내의 UPDATE 문은 변경할 열을 나타내는 MCALL 구문에 따라 동적으로 작성됩니다. 구독 테이블의 인덱스 수가 증가하고 변경되는 열 수가 적을 때 이 저장 프로시저를 사용합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_scriptdynamicupdproc [ @artid =] artid  
```  
  
## <a name="arguments"></a>인수  
 [  **@artid=**] *artid*  
 아티클 ID입니다. *artid* 은 **int**, 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
 단일으로 구성 된 결과 집합을 반환 **nvarchar (4000)** 열입니다. 결과 집합은 사용자 지정 저장 프로시저를 만드는 데 사용되는 완전한 CREATE PROCEDURE 문을 형성합니다.  
  
## <a name="remarks"></a>주의  
 **sp_scriptdynamicupdproc** 트랜잭션 복제에 사용 됩니다. 기본 MCALL 스크립팅 논리는 UPDATE 문 내에 모든 열을 포함하며 비트맵을 사용하여 변경된 열을 확인합니다. 변경되지 않은 열은 일반적으로 별 문제없이 원래 상태로 다시 설정됩니다. 열이 인덱싱된 경우 추가 처리가 발생합니다. 동적 방법에는 변경된 열만 포함되므로 최적의 UPDATE 문자열이 제공됩니다. 그러나 동적 UPDATE 문이 작성되는 런타임에 추가 처리가 발생합니다. 동적 방법과 정적 방법을 테스트한 다음 최적의 해결 방법을 선택하는 것이 좋습니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_scriptdynamicupdproc**합니다.  
  
## <a name="examples"></a>예  
 이 예에서는 아티클을 만듭니다 (으로 *artid* 로 설정 **1**)에 **작성자** 테이블에 **pubs** 데이터베이스를 지정 하는 업데이트 사용자 지정 저장 프로시저로 실행은 문이입니다.  
  
```  
'MCALL sp_mupd_authors'  
```  
  
 게시자에서 다음 저장 프로시저를 실행하여 구독자에서 배포 에이전트가 실행할 사용자 지정 저장 프로시저를 생성합니다.  
  
```  
EXEC sp_scriptdynamicupdproc @artid = '1'  
  
The statement returns:  
  
CREATE PROCEDURE [sp_mupd_authors]   
  @c1 varchar(11),@c2 varchar(40),@c3 varchar(20),@c4 char(12),@c5 varchar(40),@c6 varchar(20),  
  @c7 char(2),@c8 char(5),@c9 bit,@pkc1 varchar(11),@bitmap binary(2)  
as  
  
declare @stmt nvarchar(4000), @spacer nvarchar(1)  
SELECT @spacer =N''  
SELECT @stmt = N'UPDATE [authors] SET '  
  
if substring(@bitmap,1,1) & 2 = 2  
begin  
  select @stmt = @stmt + @spacer + N'[au_lname]' + N'=@2'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 4 = 4  
begin  
  select @stmt = @stmt + @spacer + N'[au_fname]' + N'=@3'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 8 = 8  
begin  
  select @stmt = @stmt + @spacer + N'[phone]' + N'=@4'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 16 = 16  
begin  
  select @stmt = @stmt + @spacer + N'[address]' + N'=@5'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 32 = 32  
begin  
  select @stmt = @stmt + @spacer + N'[city]' + N'=@6'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 64 = 64  
begin  
  select @stmt = @stmt + @spacer + N'[state]' + N'=@7'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 128 = 128  
begin  
  select @stmt = @stmt + @spacer + N'[zip]' + N'=@8'  
  select @spacer = N','  
end  
if substring(@bitmap,2,1) & 1 = 1  
begin  
  select @stmt = @stmt + @spacer + N'[contract]' + N'=@9'  
  select @spacer = N','  
end  
select @stmt = @stmt + N' where [au_id] = @1'  
exec sp_executesql @stmt, N' @1 varchar(11),@2 varchar(40),@3 varchar(20),@4 char(12),@5 varchar(40),  
                             @6 varchar(20),@7 char(2),@8 char(5),@9 bit',@pkc1,@c2,@c3,@c4,@c5,@c6,@c7,@c8,@c9  
  
if @@rowcount = 0  
   if @@microsoftversion>0x07320000  
      exec sp_MSreplraiserror 20598  
```  
  
 이 저장 프로시저를 실행한 후에 결과 스크립트를 사용하여 구독자에서 해당 저장 프로시저를 직접 만들 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
