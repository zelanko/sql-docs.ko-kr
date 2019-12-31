---
title: T-SQL 문
description: PDW (병렬 데이터 웨어하우스)를 SQL Server 하는 APS (분석 플랫폼 시스템)에 대 한 t-sql 문.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ce80d7a27384f628af02bfa58abcaa351b569d56
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399817"
---
# <a name="t-sql-statements-for-parallel-data-warehouse"></a>병렬 데이터 웨어하우스의 t-sql 문
PDW (병렬 데이터 웨어하우스)를 SQL Server 하는 APS (분석 플랫폼 시스템)에 대 한 transact-sql (T-sql) 문

## <a name="data-definition-language-ddl-statements"></a>데이터 정의 언어(DDL) 문
* [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)
* [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md)
* [ALTER 프로시저](../t-sql/statements/alter-procedure-transact-sql.md)
* [스키마 변경](../t-sql/statements/alter-schema-transact-sql.md)
* [ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md)
* [COLUMNSTORE 인덱스 만들기](../t-sql/statements/create-columnstore-index-transact-sql.md)
* [데이터베이스 만들기](../t-sql/statements/create-database-azure-sql-data-warehouse.md)
* [데이터베이스 범위 자격 증명 만들기](../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [외부 데이터 원본 만들기](../t-sql/statements/create-external-data-source-transact-sql.md)
* [외부 파일 형식 만들기](../t-sql/statements/create-external-file-format-transact-sql.md)
* [외부 테이블 만들기](../t-sql/statements/create-external-table-transact-sql.md)
* [CREATE 함수](../t-sql/statements/create-function-sql-data-warehouse.md)
* [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md)
* [프로시저 만들기](../t-sql/statements/create-procedure-transact-sql.md)
* [스키마 만들기](../t-sql/statements/create-schema-transact-sql.md)
* [통계 만들기](../t-sql/statements/create-statistics-transact-sql.md)
* [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)
* [CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)
* [뷰 만들기](../t-sql/statements/create-view-transact-sql.md)
* [외부 데이터 원본 삭제](../t-sql/statements/drop-external-data-source-transact-sql.md)
* [외부 파일 형식 삭제](../t-sql/statements/drop-external-file-format-transact-sql.md)
* [외부 테이블 삭제](../t-sql/statements/drop-external-table-transact-sql.md)
* [DROP INDEX](../t-sql/statements/drop-index-transact-sql.md)
* [DROP 프로시저](../t-sql/statements/drop-procedure-transact-sql.md)
* [DROP STATISTICS](../t-sql/statements/drop-statistics-transact-sql.md)
* [테이블 삭제](../t-sql/statements/drop-table-transact-sql.md)
* [스키마 삭제](../t-sql/statements/drop-schema-transact-sql.md)
* [뷰 삭제](../t-sql/statements/drop-view-transact-sql.md)
* [바꾸면](../t-sql/statements/rename-transact-sql.md)
* [TRUNCATE TABLE](../t-sql/statements/truncate-table-transact-sql.md)
* [통계 업데이트](../t-sql/statements/update-statistics-transact-sql.md)

## <a name="data-manipulation-language-dml-statements"></a>데이터 조작 언어(DML) 문
* [제거](../t-sql/statements/delete-transact-sql.md)
* [넣거나](../t-sql/statements/insert-transact-sql.md)
* [고침](../t-sql/queries/update-transact-sql.md)

## <a name="database-console-commands"></a>데이터베이스 콘솔 명령
* [DBCC DROPCLEANBUFFERS](../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)
* [DBCC FREEPROCCACHE](https://msdn.microsoft.com/library/mt204018.aspx)
* [DBCC SHRINKLOG](https://msdn.microsoft.com/library/mt204020.aspx)
* [DBCC PDW_SHOWEXECUTIONPLAN](https://msdn.microsoft.com/library/mt204017.aspx)
* [DBCC PDW_SHOWPARTITIONSTATS](https://msdn.microsoft.com/library/mt204013.aspx)
* [DBCC PDW_SHOWSPACEUSED](../t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql.md)
* [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/mt204043.aspx)

## <a name="query-statements"></a>쿼리 문
* [[](../t-sql/queries/select-transact-sql.md)
* [Common_table_expression 사용](../t-sql/queries/with-common-table-expression-transact-sql.md)
* [EXCEPT 및 INTERSECT](../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)
* [하겠습니다](../t-sql/queries/explain-transact-sql.md)
* [보낸 사람](../t-sql/queries/from-transact-sql.md)
* [PIVOT 및 UNPIVOT 사용](../t-sql/queries/from-using-pivot-and-unpivot.md)
* [GROUP BY](../t-sql/queries/select-group-by-transact-sql.md)
* [HAVING](../t-sql/queries/select-having-transact-sql.md)
* [ORDER BY](../t-sql/queries/select-order-by-clause-transact-sql.md)
* [OPTION](../t-sql/queries/option-clause-transact-sql.md)
* [UNION](../t-sql/language-elements/set-operators-union-transact-sql.md)
* [위치](../t-sql/queries/where-transact-sql.md)
* [맨 위로](../t-sql/queries/top-transact-sql.md)
* [별칭 지정](../t-sql/queries/aliasing-azure-sql-data-warehouse-parallel-data-warehouse.md)
* [검색 조건](../t-sql/queries/search-condition-transact-sql.md)
* [In](../t-sql/queries/subqueries-azure-sql-data-warehouse-parallel-data-warehouse.md)

## <a name="security-statements"></a>보안 문
* 사용 권한: [GRANT](../t-sql/statements/grant-transact-sql.md), [DENY](../t-sql/statements/deny-transact-sql.md), [REVOKE](../t-sql/statements/revoke-transact-sql.md)
* [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)
* [인증서 변경](../t-sql/statements/alter-certificate-transact-sql.md)
* [ALTER DATABASE ENCRYPTION 키](../t-sql/statements/alter-database-encryption-key-transact-sql.md)
* [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)
* [마스터 키 변경](../t-sql/statements/alter-master-key-transact-sql.md)
* [역할 변경](../t-sql/statements/alter-role-transact-sql.md)
* [사용자 변경](../t-sql/statements/alter-user-transact-sql.md)
* [인증서 백업](../t-sql/statements/backup-certificate-transact-sql.md)
* [마스터 키 닫기](../t-sql/statements/close-master-key-transact-sql.md)
* [인증서 만들기](../t-sql/statements/create-certificate-transact-sql.md)
* [데이터베이스 암호화 키 만들기](../t-sql/statements/create-database-encryption-key-transact-sql.md)
* [로그인 만들기](../t-sql/statements/create-login-transact-sql.md)
* [마스터 키 만들기](../t-sql/statements/create-master-key-transact-sql.md)
* [역할 만들기](../t-sql/statements/create-role-transact-sql.md)
* [사용자 만들기](../t-sql/statements/create-user-transact-sql.md)
* [인증서 삭제](../t-sql/statements/drop-certificate-transact-sql.md)
* [데이터베이스 암호화 키 삭제](../t-sql/statements/drop-database-encryption-key-transact-sql.md)
* [로그인 삭제](../t-sql/statements/drop-login-transact-sql.md)
* [마스터 키 삭제](../t-sql/statements/drop-master-key-transact-sql.md)
* [역할 삭제](../t-sql/statements/drop-role-transact-sql.md)
* [사용자 삭제](../t-sql/statements/drop-user-transact-sql.md)
* [마스터 키 열기](../t-sql/statements/open-master-key-transact-sql.md)

## <a name="next-steps"></a>다음 단계
자세한 참조 정보는 [t-sql 언어 요소](tsql-language-elements.md) 및 [t-sql 시스템 뷰](tsql-system-views.md)를 참조 하세요.

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
