---
title: SET ANSI_DEFAULTS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET ANSI_DEFAULTS
- ANSI_DEFAULTS
- SET_ANSI_DEFAULTS_TSQL
- ANSI_DEFAULTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ANSI_DEFAULTS option
- SET ANSI_DEFAULTS statement
ms.assetid: bd721d97-6e23-488b-8c8c-c0453d5b3b86
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 170fb1f5a95b9f6fe4fbe596906595475175b1a2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="set-ansidefaults-transact-sql"></a>SET ANSI_DEFAULTS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  몇몇 ISO 표준 동작을 전체적으로 지정하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 그룹을 제어합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server  
  
SET ANSI_DEFAULTS { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET ANSI_DEFAULTS ON;  
```  
  
## <a name="remarks"></a>주의  
 SET ANSI_DEFAULTS는 클라이언트가 수정하지 않는 서버 쪽 설정입니다. 클라이언트는 자체 설정을 관리합니다. 기본적으로 이러한 설정은 서버 설정의 반대입니다. 사용자가 서버 설정을 수정하면 안 됩니다. 이 동작을 변경하려면 사용자는 SQL_COPT_SS_PRESERVE_CURSORS를 사용해야 합니다. 자세한 내용은 참조 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)합니다.  
  
 이 옵션이 설정(ON)되어 있는 경우 다음 ISO 설정을 사용할 수 있습니다.  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_NULL_DFLT_ON|SET IMPLICIT_TRANSACTIONS|  
|SET ANSI_PADDING|SET QUOTED_IDENTIFIER|  
|SET ANSI_WARNINGS||  
  
 또한 이러한 ISO 표준 SET 옵션은 사용자 작업 세션 기간, 실행 중인 트리거, 저장 프로시저에 대해 쿼리 처리 환경을 정의합니다. 하지만 이러한 SET 옵션에는 ISO 표준을 따르는 데 필요한 모든 옵션이 포함되어 있지 않습니다.  
  
 계산 열이나 인덱싱된 뷰의 인덱스를 처리할 때 네 가지 기본값(ANSI_NULLS, ANSI_PADDING, ANSI_WARNINGS 및 QUOTED_IDENTIFIER)을 ON으로 설정해야 합니다. 이 기본값은 계산 열과 인덱싱된 뷰에서 인덱스를 만들고 변경할 때 필요한 값이 할당되어야 할 7가지 SET 옵션에 포함됩니다. 다른 SET 옵션은 ARITHABORT (ON), CONCAT_NULL_YIELDS_NULL (ON) 및 NUMERIC_ROUNDABORT (OFF)입니다. 계산된 열에 인덱스 및 인덱싱된 뷰에 필요한 SET 옵션 설정에 대 한 자세한 내용은 "고려 사항 때 설정 문 사용"의 참조 [SET 문 &#40; Transact SQL &#41; ](../../t-sql/statements/set-statements-transact-sql.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 될 때 자동으로 ANSI_DEFAULTS를 ON으로 설정 합니다. 그런 다음 CURSOR_CLOSE_ON_COMMIT과 IMPLICIT_TRANSACTIONS를 OFF로 설정합니다. ODBC 데이터 원본과 ODBC 연결 특성 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하기 전에 응용 프로그램에 설정된 OLE DB 연결 속성에서 SET CURSOR_CLOSE_ON_COMMIT 및 SET IMPLICIT_TRANSACTIONS를 OFF로 설정할 수 있습니다. DB-Library 응용 프로그램의 연결에 대한 SET ANSI_DEFAULTS 기본값은 OFF입니다.  
  
 SET ANSI_DEFAULTS가 실행되면 SET QUOTED_IDENTIFIER 옵션은 구문 분석 시 설정되고 다음 옵션은 실행 시 설정됩니다.  
  
|||  
|-|-|  
|SET ANSI_NULLS|SET ANSI_WARNINGS|  
|SET ANSI_NULL_DFLT_ON|SET CURSOR_CLOSE_ON_COMMIT|  
|SET ANSI_PADDING|SET IMPLICIT_TRANSACTIONS|  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `SET ANSI_DEFAULTS ON`을 설정하고 `DBCC USEROPTIONS` 문을 사용하여 이러한 설정을 표시합니다.  
  
```  
-- SET ANSI_DEFAULTS ON.  
SET ANSI_DEFAULTS ON;  
GO  
-- Display the current settings.  
DBCC USEROPTIONS;  
GO  
-- SET ANSI_DEFAULTS OFF.  
SET ANSI_DEFAULTS OFF;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [DBCC USEROPTIONS &#40; Transact SQL &#41;](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_NULL_DFLT_ON &#40; Transact SQL &#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md)   
 [SET ANSI_NULLS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET cursor_close_on_commit 옵션 &#40; Transact SQL &#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)   
 [SET implicit_transactions 옵션 &#40; Transact SQL &#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  

