---
description: SQLGetDiagField
title: SQLGetDiagField | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetDiagField function
ms.assetid: 395245ba-0372-43ec-b9a4-a29410d85a6d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 44412d332bdf3c6c35740cfcca091ce73a84c66b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465134"
---
# <a name="sqlgetdiagfield"></a>SQLGetDiagField
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 **SQLGetDiagField** 에 대해 다음과 같은 추가 진단 필드를 지정합니다. 이러한 필드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 애플리케이션에 대한 다양한 오류 보고를 지원하며 연결된 ODBC 연결 핸들과 ODBC 문 핸들에서 생성된 모든 진단 레코드에서 사용할 수 있습니다. 필드는 sqlncli.h에서 정의됩니다.  
  
|진단 레코드 필드|설명|  
|------------------------------|-----------------|  
|SQL_DIAG_SS_LINE|오류를 생성하는 저장 프로시저의 줄 번호를 보고합니다. SQL_DIAG_SS_LINE 값은 SQL_DIAG_SS_PROCNAME에서 값을 반환하는 경우에만 의미가 있습니다. 값은 부호 없는 16비트 정수로 반환됩니다.|  
|SQL_DIAG_SS_MSGSTATE|오류 메시지의 상태입니다. 오류 메시지 상태에 대한 자세한 내용은 [RAISERROR](../../t-sql/language-elements/raiserror-transact-sql.md)를 참조하십시오. 값은 부호 있는 32비트 정수로 반환됩니다.|  
|SQL_DIAG_SS_PROCNAME|필요한 경우 오류를 생성하는 저장 프로시저의 이름입니다. 값은 문자열로 반환됩니다. 문자열 길이(문자 수)는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에 따라 달라집니다. SQL_MAX_PROCEDURE_NAME_LEN의 값을 요청하는 [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md) 를 호출하여 값을 확인할 수 있습니다.|  
|SQL_DIAG_SS_SEVERITY|관련된 오류 메시지의 심각도 수준입니다. 값은 부호 있는 32비트 정수로 반환됩니다.|  
|SQL_DIAG_SS_SRVNAME|오류가 발생한 서버의 이름입니다. 값은 문자열로 반환됩니다. 문자열 길이(문자 수)는 sqlncli.h의 SQL_MAX_SQLSERVERNAME 매크로에 의해 정의됩니다.|  
  
 문자 데이터가 포함된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련 진단 필드 SQL_DIAG_SS_PROCNAME과 SQL_DIAG_SS_SRVNAME은 해당 데이터를 Null로 종결된 ANSI 또는 유니코드 문자열로 클라이언트에 반환합니다. 필요한 경우 문자 너비로 문자 수를 조정해야 합니다. 또는 이식 가능한 C 데이터 형식(예: TCHAR 또는 SQLTCHAR)을 사용하여 올바른 프로그램 변수 길이를 유지할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 마지막으로 시도된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문을 식별하는 다음과 같은 추가 동적 함수 코드를 보고합니다. 동적 함수 코드는 진단 레코드 집합의 헤더(레코드 0)에 반환되므로 성공 여부에 관계없이 실행할 때마다 사용할 수 있습니다.  
  
|동적 함수 코드|원본|  
|---------------------------|------------|  
|SQL_DIAG_DFC_SS_ALTER_DATABASE|ALTER DATABASE 문|  
|SQL_DIAG_DFC_SS_CHECKPOINT|CHECKPOINT 문|  
|SQL_DIAG_DFC_SS_CONDITION|문의 WHERE 또는 HAVING 절에서 오류 발생|  
|SQL_DIAG_DFC_SS_CREATE_DATABASE|CREATE DATABASE 문|  
|SQL_DIAG_DFC_SS_CREATE_DEFAULT|CREATE DEFAULT 문|  
|SQL_DIAG_DFC_SS_CREATE_PROCEDURE|CREATE PROCEDURE 문|  
|SQL_DIAG_DFC_SS_CREATE_RULE|CREATE RULE 문|  
|SQL_DIAG_DFC_SS_CREATE_TRIGGER|CREATE TRIGGER 문|  
|SQL_DIAG_DFC_SS_CURSOR_DECLARE|DECLARE CURSOR 문|  
|SQL_DIAG_DFC_SS_CURSOR_OPEN|OPEN 문|  
|SQL_DIAG_DFC_SS_CURSOR_FETCH|FETCH 문|  
|SQL_DIAG_DFC_SS_CURSOR_CLOSE|CLOSE 문|  
|SQL_DIAG_DFC_SS_DEALLOCATE_CURSOR|DEALLOCATE 문|  
|SQL_DIAG_DFC_SS_DBCC|DBCC 문|  
|SQL_DIAG_DFC_SS_DENY|DENY 문|  
|SQL_DIAG_DFC_SS_DROP_DATABASE|DROP DATABASE 문|  
|SQL_DIAG_DFC_SS_DROP_DEFAULT|DROP DEFAULT 문|  
|SQL_DIAG_DFC_SS_DROP_PROCEDURE|DROP PROCEDURE 문|  
|SQL_DIAG_DFC_SS_DROP_RULE|DROP RULE 문|  
|SQL_DIAG_DFC_SS_DROP_TRIGGER|DROP TRIGGER 문|  
|SQL_DIAG_DFC_SS_DUMP_DATABASE|BACKUP 또는 DUMP DATABASE 문|  
|SQL_DIAG_DFC_SS_DUMP_TABLE|DUMP TABLE 문|  
|SQL_DIAG_DFC_SS_DUMP_TRANSACTION|BACKUP 또는 DUMP TRANSACTION 문. **Trunc가 chkpt** 인 경우에는 CHECKPOINT 문에 대해서도 반환 됩니다. 데이터베이스 옵션이 설정되어 있으면 CHECKPOINT 문에 대해서도 반환됩니다.|  
|SQL_DIAG_DFC_SS_GOTO|GOTO 흐름 제어 문|  
|SQL_DIAG_DFC_SS_INSERT_BULK|INSERT BULK 문|  
|SQL_DIAG_DFC_SS_KILL|KILL 문|  
|SQL_DIAG_DFC_SS_LOAD_DATABASE|LOAD 또는 RESTORE DATABASE 문|  
|SQL_DIAG_DFC_SS_LOAD_HEADERONLY|LOAD 또는 RESTORE HEADERONLY 문|  
|SQL_DIAG_DFC_SS_LOAD_TABLE|LOAD TABLE 문|  
|SQL_DIAG_DFC_SS_LOAD_TRANSACTION|LOAD 또는 RESTORE TRANSACTION 문|  
|SQL_DIAG_DFC_SS_PRINT|PRINT 문|  
|SQL_DIAG_DFC_SS_RAISERROR|RAISERROR 문|  
|SQL_DIAG_DFC_SS_READTEXT|READTEXT 문|  
|SQL_DIAG_DFC_SS_RECONFIGURE|RECONFIGURE 문|  
|SQL_DIAG_DFC_SS_RETURN|RETURN 흐름 제어 문|  
|SQL_DIAG_DFC_SS_SELECT_INTO|SELECT INTO 문|  
|SQL_DIAG_DFC_SS_SET|SET 문(일반, 모든 옵션)|  
|SQL_DIAG_DFC_SS_SET_IDENTITY_INSERT|SET IDENTITY_INSERT 문|  
|SQL_DIAG_DFC_SS_SET_ROW_COUNT|SET ROWCOUNT 문|  
|SQL_DIAG_DFC_SS_SET_STATISTICS|SET STATISTICS IO 또는 SET STATISTICS TIME 문|  
|SQL_DIAG_DFC_SS_SET_TEXTSIZE|CREATE TEXTSIZE 문|  
|SQL_DIAG_DFC_SS_SETUSER|SETUSER 문|  
|SQL_DIAG_DFC_SS_SET_XCTLVL|SET TRANSACTION ISOLATION LEVEL 문|  
|SQL_DIAG_DFC_SS_SHUTDOWN|SHUTDOWN 문|  
|SQL_DIAG_DFC_SS_TRANS_BEGIN|BEGIN TRAN 문|  
|SQL_DIAG_DFC_SS_TRANS_COMMIT|COMMIT TRAN 문|  
|SQL_DIAG_DFC_SS_TRANS_PREPARE|분산 트랜잭션 커밋 준비|  
|SQL_DIAG_DFC_SS_TRANS_ROLLBACK|ROLLBACK TRAN 문|  
|SQL_DIAG_DFC_SS_TRANS_SAVE|SAVE TRAN 문|  
|SQL_DIAG_DFC_SS_TRUNCATE_TABLE|TRUNCATE TABLE 문|  
|SQL_DIAG_DFC_SS_UPDATE_STATISTICS|UPDATE STATISTICS 문|  
|SQL_DIAG_DFC_SS_UPDATETEXT|UPDATETEXT 문|  
|SQL_DIAG_DFC_SS_USE|USE 문|  
|SQL_DIAG_DFC_SS_WAITFOR|WAITFOR 흐름 제어 문|  
|SQL_DIAG_DFC_SS_WRITETEXT|WRITETEXT 문|  
  
## <a name="sqlgetdiagfield-and-table-valued-parameters"></a>SQLGetDiagField 및 테이블 반환 매개 변수  
 SQLGetDiagField를 사용 하 여 두 개의 진단 필드인 SQL_DIAG_SS_TABLE_COLUMN_NUMBER 및 SQL_DIAG_SS_TABLE_ROW_NUMBER를 검색할 수 있습니다. 두 필드는 진단 레코드와 관련된 오류 또는 경고를 발생시킨 값을 확인하는 데 유용합니다.  
  
 테이블 반환 매개 변수에 대 한 자세한 내용은 [ODBC&#41;&#40;테이블 반환 매개 변수 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQLGetDiagField 함수](../../odbc/reference/syntax/sqlgetdiagfield-function.md)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
