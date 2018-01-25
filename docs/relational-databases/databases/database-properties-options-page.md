---
title: "데이터베이스 속성(옵션 페이지) | Microsoft 문서"
ms.custom: 
ms.date: 08/28/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.databaseproperties.options.f1
ms.assetid: a3447987-5507-4630-ac35-58821b72354d
caps.latest.revision: "67"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 342f7d2f57d8832ca0188ceea9112673746690b7
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="database-properties-options-page"></a>데이터베이스 속성(옵션 탭)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 페이지를 사용하여 선택한 데이터베이스의 옵션을 확인하거나 수정할 수 있습니다. 이 페이지에서 사용할 수 있는 옵션에 대한 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) 및 [ALTER DATABASE SCOPED CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 참조하세요.  
  
## <a name="page-header"></a>페이지 머리글  
 **데이터 정렬**  
 목록에서 선택하여 데이터베이스의 데이터 정렬을 지정합니다. 자세한 내용은 [Set or Change the Database Collation](../../relational-databases/collations/set-or-change-the-database-collation.md)을 참조하세요.  
  
 **복구 모델**  
 데이터베이스 복구 모델을 **전체**, **대량 로그**또는 **단순**중에서 하나 지정합니다. 복구 모델에 대한 자세한 내용은 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)을 참조하세요.  
  
 **호환성 수준**  
 데이터베이스에서 지원하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 최신 버전을 지정합니다. 가능한 값은 [ALTER DATABASE(Transact-SQL) 호환성 수준](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요. SQL Server 데이터베이스가 업그레이드되면 해당 데이터베이스에 대한 호환성 수준이 보존되거나(가능한 경우) 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대해 지원되는 최소 수준으로 변경됩니다. 
  
 **포함 유형**  
 없음 또는 부분을 지정하여 데이터베이스가 포함된 데이터베이스인지 여부를 나타냅니다. 포함된 데이터베이스에 대한 자세한 내용은 [Contained Databases](../../relational-databases/databases/contained-databases.md)를 참조하십시오. 데이터베이스를 포함된 데이터베이스로 구성하려면 **포함된 데이터베이스 사용** 서버 속성을 **TRUE** 로 설정해야 합니다.  
  
> [!IMPORTANT]  
>  부분적으로 포함된 데이터베이스를 사용하도록 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 액세스 제어 권한이 데이터베이스 소유자에게 위임됩니다. 자세한 내용은 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)를 참조하세요.  
  
## <a name="automatic"></a>자동  
 **자동 닫기**  
 마지막 사용자가 끝낸 후 데이터베이스가 완전히 종료되고 리소스가 해제되는지 여부를 지정합니다. 가능한 값은 **True** 및 **False**입니다. **True**로 설정하면 마지막 사용자가 로그오프한 후 데이터베이스가 완전히 종료되고 해당 리소스가 해제됩니다.  
  
 **증분 통계 자동 작성**  
 파티션당 통계를 만들 때 증분 옵션을 사용할지 여부를 지정합니다. 증분 통계에 대한 자세한 내용은 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요.  
  
 **통계 자동 작성**  
 데이터베이스에서 누락된 최적화 통계를 자동으로 작성하는지 여부를 지정합니다. 가능한 값은 **True** 및 **False**입니다. **True**로 설정하면 쿼리 최적화에 필요한 누락된 통계가 최적화 동안 모두 자동으로 작성됩니다. 자세한 내용은 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요.  
  
 **자동 축소**  
 데이터베이스 파일을 주기적으로 축소할 수 있는지 여부를 지정합니다. 가능한 값은 **True** 및 **False**입니다. 자세한 내용은 [Shrink a Database](../../relational-databases/databases/shrink-a-database.md)를 참조하세요.  
  
 **통계 자동 업데이트**  
 데이터베이스에서 오래된 최적화 통계를 자동으로 업데이트하는지 여부를 지정합니다. 가능한 값은 **True** 및 **False**입니다. **True**로 설정하면 쿼리 최적화에 필요한 오래된 통계가 최적화 동안 모두 자동으로 업데이트됩니다. 자세한 내용은 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요.  
  
 **통계를 비동기적으로 자동 업데이트**  
 **True**로 설정하면 오래된 통계에 대해 자동 업데이트를 시작하는 쿼리가 컴파일 수행 전에 통계가 업데이트되기를 기다리지 않습니다. 업데이트된 통계를 이용할 수 있으면 후속 쿼리는 업데이트된 통계를 사용합니다.  
  
 **False**로 설정하면 오래된 통계에 대해 자동 업데이트를 시작하는 쿼리가 업데이트된 통계를 쿼리 최적화 계획에 사용할 수 있을 때까지 기다립니다.  
  
 이때 **통계 자동 업데이트** 도 **True** 로 설정해야 이 옵션을 **True**로 설정했을 때 효과가 있습니다.  
  
## <a name="containment"></a>Containment  
 포함된 데이터베이스의 경우 일반적으로 서버 수준에서 구성하는 일부 설정을 데이터베이스 수준에서 구성할 수 있습니다.  
  
 **기본 전체 텍스트 언어 LCID**  
 전체 텍스트 인덱싱된 열에 대한 기본 언어를 지정합니다. 전체 텍스트 인덱싱된 데이터의 언어 분석은 데이터의 언어에 따라 달라집니다. 이 옵션의 기본값은 서버의 언어입니다. 표시되는 설정에 해당하는 언어에 대한 자세한 내용은 [sys.fulltext_languages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)를 참조하세요.  
  
 **기본 언어**  
 따로 지정하지 않는 한 모든 새 포함된 데이터베이스 사용자의 기본 언어입니다.  
  
 **중첩 트리거 사용**  
 다른 트리거를 발생시키는 트리거를 허용합니다. 트리거는 최대 32 수준까지 중첩될 수 있습니다. 자세한 내용은 [CREATE TRIGGER&#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)의 "중첩 트리거" 섹션을 참조하세요.  
  
 **의미 없는 단어 변환**  
 의미 없는 단어(중지 단어)로 인해 전체 텍스트 쿼리에 대한 부울 연산에서 0개의 행을 반환할 경우 오류 메시지를 표시하지 않습니다. 자세한 내용은 [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)을 참조하세요.  
  
 **두 자리 연도 구분**  
 두 자릿수 연도로 입력될 수 있는 최고 연도 수를 나타냅니다. 나열된 연도와 99 이하인 연도는 두 자릿수 연도로 입력될 수 있습니다. 모든 다른 연도는 네 자릿수 연도로 입력되어야 합니다.  
  
 예를 들어, 기본 설정이 2049이면 '49/3/14'로 입력된 날짜는 2049년 3월 14일로 해석되고 '50/3/14'로 입력된 날짜는 1950년 3월 14일로 해석되는 것을 나타냅니다. 자세한 내용은 [Configure the two digit year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)을 참조하세요.  
  
## <a name="cursor"></a>커서  
 **커밋 시 커서 닫기 설정**  
 커서를 여는 트랜잭션이 커밋된 후 커서가 닫히는지 여부를 지정합니다. 가능한 값은 **True** 및 **False**입니다. **True**로 설정하면 트랜잭션이 커밋되거나 롤백될 때 열려 있는 커서가 모두 닫힙니다. **False**로 설정하면 트랜잭션이 커밋될 때 해당 커서가 열린 상태로 남게 됩니다. **False**로 설정한 경우 트랜잭션을 롤백하면 INSENSITIVE 또는 STATIC으로 정의된 것을 제외한 모든 커서가 닫힙니다. 자세한 내용은 [SET CURSOR_CLOSE_ON_COMMIT&#40;Transact-SQL&#41;](../../t-sql/statements/set-cursor-close-on-commit-transact-sql.md)을 참조하세요.  
  
 **기본 커서**  
 기본 커서 동작을 지정합니다. **True**로 설정하면 커서 선언은 기본적으로 LOCAL이 됩니다. **False**로 설정하면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서는 기본적으로 GLOBAL이 됩니다.  
  
## <a name="database-scoped-configurations"></a>데이터베이스 범위 구성  
 SQL Server 2016 및 Azure SQL 데이터베이스에는 데이터베이스 수준으로 범위를 지정할 수 있는 여러 구성 속성이 있습니다. 이러한 모든 설정에 대한 자세한 내용은 [ALTER DATABASE SCOPED CONFIGURATION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)을 참조하세요.  
  
 **기존 카디널리티 추정**  
 데이터베이스의 호환성 수준에 관계없이 주 항목에 대한 쿼리 최적화 프로그램 카디널리티 추정 모델을 지정합니다. 이 설정은 [추적 플래그 9481](https://support.microsoft.com/en-us/kb/2801413)과 동일합니다.  
  
 **보조 항목용 기존 카디널리티 추정**  
 데이터베이스의 호환성 수준에 관계없이 보조 항목(있는 경우)에 대한 쿼리 최적화 프로그램 카디널리티 추정 모델을 지정합니다. 이 설정은 [추적 플래그 9481](https://support.microsoft.com/en-us/kb/2801413)과 동일합니다.  
  
 **최대 DOP**  
 문에 사용해야 하는 주 항목에 대한 기본 [MAXDOP](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 설정을 지정합니다.  
  
 **보조 항목에 대한 최대 DOP**  
 문에 사용해야 하는 보조 항목(있는 경우)에 대한 기본 [MAXDOP](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 설정을 지정합니다.  
  
 **매개 변수 검색**  
 주 항목에 대해 매개 변수 검색을 사용하거나 사용하지 않도록 설정합니다. 이 설정은 [추적 플래그 4136](https://support.microsoft.com/en-us/kb/980653)과 동일합니다.  
  
 **보조 항목에 대한 매개 변수 검색**  
 보조 항목(있는 경우)에 대해 매개 변수 검색을 사용하거나 사용하지 않도록 설정합니다. 이 설정은 [추적 플래그 4136](https://support.microsoft.com/en-us/kb/980653)과 동일합니다.  
  
 **쿼리 최적화 프로그램 수정**  
 데이터베이스의 호환성 수준에 관계없이 주 항목에 대해 쿼리 최적화 핫픽스를 사용하거나 사용하지 않도록 설정합니다. 이 설정은 [추적 플래그 4199](https://support.microsoft.com/en-us/kb/974006)와 동일합니다.  
  
 **보조 항목에 대한 쿼리 최적화 프로그램 수정**  
 데이터베이스의 호환성 수준에 관계없이 보조 항목(있는 경우)에 대해 쿼리 최적화 핫픽스를 사용하거나 사용하지 않도록 설정합니다. 이 설정은 [추적 플래그 4199](https://support.microsoft.com/en-us/kb/974006)와 동일합니다.  
  
## <a name="filestream"></a>FILESTREAM  
 **FILESTREAM 디렉터리 이름**  
 선택한 데이터베이스에 연결된 FILESTREAM 데이터에 대한 디렉터리 이름을 지정합니다.  
  
 **FILESTREAM 비트랜잭션 액세스**  
 파일 시스템을 통해 FileTable에 저장된 FILESTREAM 데이터에 비트랜잭션 방식으로 액세스하기 위한 옵션을 **OFF**, **READ_ONLY**또는 **FULL**중 하나로 지정합니다. 서버에 FILESTREAM이 사용하도록 설정되어 있지 않은 경우에는 이 값이 OFF로 설정되고 사용할 수 없는 상태로 표시됩니다. 자세한 내용은 [FileTables&#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)를 참조하세요.  
  
## <a name="miscellaneous"></a>기타  
**스냅숏 격리 허용**  
이 기능을 사용할 수 있습니다.  

 **ANSI Null 기본값**  
 **CREATE TABLE** 또는 **ALTER TABLE** 문(기본 상태)을 실행하는 동안 **NOT NULL** 로 명시적으로 정의되지 않은 모든 사용자 정의 데이터 형식 또는 열에서 Null 값을 허용합니다. 자세한 내용은 [SET ANSI_NULL_DFLT_ON&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-null-dflt-on-transact-sql.md) 및 [SET ANSI_NULL_DFLT_OFF&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-null-dflt-off-transact-sql.md)를 참조하세요.  
  
 **ANSI Null 설정**  
 Null 값과 함께 사용할 때 같음(`=`)과 같지 않음(`<>`) 비교 연산자의 동작을 지정합니다. 가능한 값은 **True** (설정) 및 **False** (해제)입니다. **True**로 설정하면 NULL 값에 대한 모든 비교가 UNKNOWN으로 평가됩니다. **False**로 설정하면 NULL 값과 유니코드를 지원하지 않는 값의 비교는 두 값이 모두 NULL인 경우 **True**로 평가됩니다. 자세한 내용은 [SET ANSI_NULLS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)를 참조하세요.  
  
 **ANSI 패딩 설정**  
 ANSI 패딩을 설정할 것인지 여부를 지정합니다. 가능한 값은 **True**(설정) 및 **False**(해제)입니다. 자세한 내용은 [SET ANSI_PADDING&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)을 참조하세요.  
  
 **ANSI 경고 설정**  
 여러 오류 조건에 대한 ISO 표준 동작을 지정합니다. **True**로 설정한 경우 집계 함수(SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP, COUNT 등)에 NULL 값이 있으면 경고 메시지가 생성됩니다. **False**로 설정한 경우에는 경고가 발생하지 않습니다. 자세한 내용은 [SET ANSI_WARNINGS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)를 참조하세요.  
  
 **산술 연산 중단 설정**  
 산술 연산 중단에 대한 데이터베이스 옵션의 설정 여부를 지정합니다. 가능한 값은 **True** 및 **False**입니다. **True**로 설정하면 오버플로 또는 0으로 나누기 오류로 인해 쿼리 또는 일괄 처리가 종료됩니다. 트랜잭션에 오류가 발생하면 트랜잭션이 롤백됩니다. **False**로 설정하면 경고 메시지가 표시되지만 쿼리, 일괄 처리 또는 트랜잭션은 오류가 발생하지 않은 것처럼 계속 진행됩니다. 자세한 내용은 [SET ARITHABORT&#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)를 참조하세요.  
  
 **Null 연결 시 Null 생성**  
 Null 값이 연결될 때의 동작을 지정합니다. 속성 값이 **True**이면 **string** + NULL이 NULL을 반환합니다. **False**이면 결과는 **string**입니다. 자세한 내용은 [SET CONCAT_NULL_YIELDS_NULL&#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)을 참조하세요.  
  
 **데이터베이스 간 소유권 체인 설정**  
 이 읽기 전용 값은 데이터베이스 간 소유권 체인이 설정되어 있는지 여부를 나타냅니다. **True**이면 데이터베이스가 데이터베이스 간 소유권 체인의 원본이나 대상이 될 수 있습니다. ALTER DATABASE 문을 사용하여 이 속성을 설정할 수 있습니다.  
  
 **날짜 상관 관계 최적화 설정**  
 **True**로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 데이터베이스 내에서 FOREIGN KEY 제약 조건으로 연결되고 **datetime** 열이 있는 임의의 두 테이블 간에 상관 관계 통계를 유지합니다.  
  
 **False**로 설정하면 상관 관계 통계가 유지되지 않습니다.  
 
 **지원된 내구성**  
 이 기능을 사용할 수 있습니다.  
 
 **Read Committed 스냅숏 설정 여부**  
 이 기능을 사용할 수 있습니다.  
 
 **숫자 반올림 시 중단**  
 데이터베이스에서 반올림 오류를 처리하는 방법을 지정합니다. 가능한 값은 **True** 및 **False**입니다. **True**로 설정한 경우 식에서 전체 자릿수 손실이 발생하면 오류가 생성됩니다. **False**로 설정한 경우 전체 자릿수가 손실되면 오류 메시지가 생성되지 않고 해당 결과를 저장하는 변수나 열의 전체 자릿수로 결과가 반올림됩니다. 자세한 내용은 [SET NUMERIC_ROUNDABORT&#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)를 참조하세요.  
  
 **매개 변수화**  
 **SIMPLE**로 설정하면 쿼리가 데이터베이스의 기본 동작을 기반으로 매개 변수화됩니다. **FORCED**로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터베이스의 모든 쿼리를 매개 변수화합니다.  
  
 **따옴표 붙은 식별자 설정**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 키워드를 따옴표로 묶으면 식별자(개체 또는 변수 이름)로 사용할 수 있는지 여부를 지정합니다. 가능한 값은 **True** 및 **False**입니다. 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.  
  
 **재귀적 트리거 설정**  
 다른 트리거가 트리거를 발생시킬 수 있는지 여부를 지정합니다. 가능한 값은 **True** 및 **False**입니다. **True**로 설정하면 트리거가 재귀적으로 발생할 수 있습니다. **False**로 설정하면 직접 재귀만 방지됩니다. 간접 재귀를 해제하려면 sp_configure를 사용하여 nested triggers 서버 옵션을 0으로 설정합니다. 자세한 내용은 [중첩 트리거 만들기](../../relational-databases/triggers/create-nested-triggers.md)를 참조하세요.  
  
 **신뢰**  
 이 읽기 전용 옵션이 **True**를 표시하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터베이스 내에 설정된 가장 컨텍스트로 데이터베이스 외부의 리소스에 대한 액세스를 허용함을 나타냅니다. 가장 컨텍스트는 데이터베이스 모듈에 EXECUTE AS 사용자 문이나 EXECUTE AS 절을 사용하여 데이터베이스 내에 설정할 수 있습니다.  
  
 액세스하려면 데이터베이스의 소유자에게도 서버 수준의 AUTHENTICATE SERVER 권한이 있어야 합니다.  
  
 이 속성을 통해 데이터베이스 내에서 안전하지 않은 외부 액세스 어셈블리를 만들고 실행할 수 있습니다. 데이터베이스의 소유자는 이 속성을 **True**로 설정하는 것 외에 서버 수준의 EXTERNAL ACCESS ASSEMBLY 또는 UNSAFE ASSEMBLY 권한도 가지고 있어야 합니다.  
  
 기본적으로 **MSDB**를 제외한 모든 사용자 데이터베이스 및 시스템 데이터베이스에는 이 속성이 **False**로 설정되어 있습니다. **model** 및 **tempdb** 데이터베이스에 대해서는 이 값을 변경할 수 없습니다.  
  
 신뢰는 데이터베이스가 서버에 연결될 때마다 **False** 로 설정됩니다.  
  
 가장 컨텍스트로 데이터베이스 외부의 리소스에 액세스할 때는 **Trustworthy** 옵션과 함께 인증서와 서명을 사용하는 것이 좋습니다.  
  
 이 속성을 설정하려면 ALTER DATABASE 문을 사용합니다.  
  
 **VarDecimal 저장소 형식 사용**  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 이 옵션은 읽기 전용입니다. **True**인 경우 이 데이터베이스에 VarDecimal 저장소 형식을 사용할 수 있습니다. 데이터베이스의 테이블 중 VarDecimal 저장소 형식을 사용하는 테이블이 있으면 이 형식을 해제할 수 없습니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서는 모든 데이터베이스에 VarDecimal 저장소 형식을 사용할 수 있습니다. 이 옵션은 [sp_db_vardecimal_storage_format](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)을 사용합니다.  
  
## <a name="recovery"></a>복구  
 **페이지 확인**  
 디스크 I/O 오류로 인해 발생한 불완전한 I/O 트랜잭션을 검색하여 보고하는 데 사용되는 옵션을 지정합니다. 가능한 값은 **NONE**, **TORN_PAGE_DETECTION**및 **CHECKSUM**입니다. 자세한 내용은 [suspect_pages 테이블 관리&#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)에서 페이지를 복원하는 방법에 대해 설명합니다.  
  
 **대상 복구 시간(초)**  
 충돌 시 지정된 데이터베이스를 복구하는 데 걸리는 최대 시간(초)을 지정합니다. 자세한 내용은 [데이터베이스 검사점&#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)을 참조하세요.  

## <a name="service-broker"></a>Service Broker  
**Broker 활성화**  
Service Broker를 활성화 또는 비활성화합니다.  

**Broker 우선 순위 인식**  
읽기 전용 Service Broker 속성입니다.  

**Serice Broker 식별자**  
읽기 전용 식별자입니다.  

## <a name="state"></a>State  
 **데이터베이스 읽기 전용**  
 데이터베이스가 읽기 전용인지 여부를 지정합니다. 가능한 값은 **True** 및 **False**입니다. **True**로 설정하면 사용자가 데이터베이스의 데이터를 읽을 수만 있습니다. 사용자가 데이터나 데이터베이스 개체를 수정할 수는 없지만 `DROP DATABASE` 문을 사용하여 데이터베이스 자체를 삭제할 수는 있습니다. 데이터베이스를 사용하고 있을 때는 **데이터베이스 읽기 전용** 옵션의 새 값을 지정할 수 없습니다. master 데이터베이스는 예외인데, 이 옵션이 설정되어 있는 동안 시스템 관리자만 master를 사용할 수 있습니다.  
  
 **데이터베이스 상태**  
 데이터베이스의 현재 상태를 확인합니다. 편집할 수 없습니다. **데이터베이스 상태**에 대한 자세한 내용은 [Database States](../../relational-databases/databases/database-states.md)를 참조하십시오.  

 **암호화 사용**  
 **True**이면 이 데이터베이스에 데이터베이스 암호화를 사용할 수 있습니다. 데이터베이스 암호화 키는 암호화에 필요합니다. 자세한 내용은 [TDE&#40;투명한 데이터 암호화&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하세요.  
 
 **액세스 제한**  
 데이터베이스에 액세스할 수 있는 사용자를 지정합니다. 가능한 값은  
  
-   **여러 항목**  
  
     프로덕션 데이터베이스의 일반 상태로, 한 번에 여러 사용자가 데이터베이스에 액세스할 수 있습니다.  
  
-   **단일**  
  
     유지 관리 동작에 사용되며 한 번에 한 명의 사용자만 데이터베이스에 액세스할 수 있습니다.  
  
-   **제한됨**  
  
     db_owner, dbcreator 또는 sysadmin 역할의 멤버만 데이터베이스를 사용할 수 있습니다.  
  


## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
