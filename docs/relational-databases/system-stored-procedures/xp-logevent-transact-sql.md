---
title: xp_logevent (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_logevent
- xp_logevent_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logevent
ms.assetid: 7b379ad0-5b12-4d2e-9c52-62465df1fdbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 77275ee539a6367d7e2e04d03354155a5eff721d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68116638"
---
# <a name="xp_logevent-transact-sql"></a>xp_logevent(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그 파일 및 Windows 이벤트 뷰어에 사용자 정의 메시지를 기록 합니다. xp_logevent를 사용 하 여 클라이언트에 게 메시지를 보내지 않고 경고를 보낼 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_logevent { error_number , 'message' } [ , 'severity' ]  
```  
  
## <a name="arguments"></a>인수  
 *error_number*  
 50,000을 초과하는 사용자 정의 오류 번호입니다. 최대값은 2147483647(2^31 - 1)입니다.  
  
 **'** *message* **'**  
 최대 2048자의 문자열입니다.  
  
 **'** *심각도* **'**  
 는 세 문자열 (정보, 경고 또는 오류) 중 하나입니다. *심각도* 는 선택 사항이 며 기본값은 정보입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 xp_logevent는 포함된 코드 예제에 대해 다음과 같은 오류 메시지를 반환합니다.  
  
 `The command(s) completed successfully.`  
  
## <a name="remarks"></a>설명  
 프로시저, 트리거, 일괄 [!INCLUDE[tsql](../../includes/tsql-md.md)] 처리 등에서 메시지를 보낼 때 XP_LOGEVENT 대신 RAISERROR 문을 사용 합니다. xp_logevent은 클라이언트의 메시지 처리기를 호출 하거나 @@ERROR를 설정 하지 않습니다. Windows 이벤트 뷰어와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그 파일에 메시지를 기록하려면 RAISERROR 문을 실행하십시오.  
  
## <a name="permissions"></a>사용 권한  
 master 데이터베이스에서 db_owner 고정 데이터베이스 역할의 멤버이거나 sysadmin 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예는 메시지로 전달된 변수와 함께 메시지를 Windows 이벤트 뷰어에 로깅합니다.  
  
```  
DECLARE @@TABNAME varchar(30), @@USERNAME varchar(30), @@MESSAGE varchar(255);  
SET @@TABNAME = 'customers';  
SET @@USERNAME = USER_NAME();  
SELECT @@MESSAGE = 'The table ' + @@TABNAME + ' is not owned by the user   
   ' + @@USERNAME + '.';  
  
USE master;  
EXEC xp_logevent 60000, @@MESSAGE, informational;  
```  
  
## <a name="see-also"></a>참고 항목  
 [PRINT&#40;Transact-SQL&#41;](../../t-sql/language-elements/print-transact-sql.md)   
 [RAISERROR&#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;일반 확장 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
