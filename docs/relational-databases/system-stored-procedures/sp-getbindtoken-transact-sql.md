---
title: sp_getbindtoken (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_getbindtoken
- sp_getbindtoken_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_getbindtoken
ms.assetid: 5db87d77-85fa-45a3-a23a-3ea500f9a5ac
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 14fb45e2d5b7acad7cd0925ec32a9f56f10ddf55
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730061"
---
# <a name="sp_getbindtoken-transact-sql"></a>sp_getbindtoken(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  트랜잭션에 대한 고유한 식별자를 반환합니다. 이 고유 식별자는 sp_bindsession을 사용하여 세션을 바인딩하는 데 필요한 문자열입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 MARS(Multiple Active Results Sets) 또는 분산 트랜잭션을 사용하십시오. 자세한 내용은 [MARS&#40;Multiple Active Result Sets&#41; 사용](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_getbindtoken [@out_token =] 'return_value' OUTPUT   
```  
  
## <a name="arguments"></a>인수  
 [ @out_token =] '*return_value*'  
 세션을 바인딩하는 데 사용되는 토큰입니다. *return_value* 는 **varchar (255)** 이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 sp_getbindtoken은 활성 트랜잭션 내에서 저장 프로시저를 실행 하는 경우에만 유효한 토큰을 반환 합니다. 그렇지 않으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 오류 메시지를 반환합니다. 예를 들면 다음과 같습니다.  
  
```  
-- Declare a variable to hold the bind token.  
-- No active transaction.  
DECLARE @bind_token varchar(255);  
-- Trying to get the bind token returns an error 3921.  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
Server: Msg 3921, Level 16, State 1, Procedure sp_getbindtoken, Line 4  
Cannot get a transaction token if there is no transaction active.  
Reissue the statement after a transaction has been started.  
```  
  
 Sp_getbindtoken를 사용 하 여 열린 트랜잭션 내부에 분산 트랜잭션 연결을 등록 하면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동일한 토큰을 반환 합니다. 예를 들면 다음과 같습니다.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @bind_token varchar(255);  
  
BEGIN TRAN;  
  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
SELECT @bind_token AS Token;  
  
BEGIN DISTRIBUTED TRAN;  
  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
SELECT @bind_token AS Token;  
```  
  
 두 `SELECT` 문은 다음과 같이 동일한 토큰을 반환합니다.  
  
```  
Token  
-----  
PKb'gN5<9aGEedk_16>8U=5---/5G=--  
(1 row(s_) affected)  
  
Token  
-----  
PKb'gN5<9aGEedk_16>8U=5---/5G=--  
(1 row(s_) affected)  
```  
  
 바인드 토큰과 sp_bindsession을 사용하여 새 세션을 동일한 트랜잭션에 바인딩할 수 있습니다. 바인드 토큰은 각 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 내부 로컬에서만 유효하며 여러 인스턴스에서 공유할 수 없습니다.  
  
 바인드 토큰을 가져와서 전달하려면 sp_bindsession을 실행하기 전에 sp_getbindtoken을 실행하여 동일한 잠금 공간을 공유하도록 해야 합니다. 바인드 토큰을 가져온 경우에는 sp_bindsession이 올바르게 실행됩니다.  
  
> [!NOTE]  
>  외부 저장 프로시저에서 사용할 바인드 토큰을 얻는 데는 srv_getbindtoken 개방형 Data Services API(애플리케이션 프로그래밍 인터페이스)를 사용하는 것이 좋습니다.  
  
## <a name="permissions"></a>사용 권한  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 바인드 토큰을 가져오고 이름을 표시하는 방법을 보여 줍니다.  
  
```  
DECLARE @bind_token varchar(255);  
BEGIN TRAN;  
EXECUTE sp_getbindtoken @bind_token OUTPUT;  
SELECT @bind_token AS Token;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Token`  
  
 `----------------------------------------------------------`  
  
 `\0]---5^PJK51bP<1F<-7U-]ANZ`  
  
## <a name="see-also"></a>참고 항목  
 [sp_bindsession&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [srv_getbindtoken &#40;확장 저장 프로시저 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)  
  
  
