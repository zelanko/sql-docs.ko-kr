---
title: 호환 되지 않는 액세스 기능 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, features incompatible with SQL Azure
- Access databases, features incompatible with SQL Server
- dates
- default expressions
- foreign keys
- hyperlink columns
- incompatible Access features
- indexes
- indexes, length of
- keywords
- primary keys
- reference, incompatible features
- replication columns
- special characters
- unique indexes
- validation rules
ms.assetid: 99d45b9c-e3b9-4d56-8c25-b594b887ace1
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2cc48fa530730beec07aaca4bfb933c9ff8fb2b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67986350"
---
# <a name="incompatible-access-features-accesstosql"></a>호환 되지 않는 액세스 기능 (AccessToSQL)
모든 Access 데이터베이스 기능이와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]호환 되지 않습니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 액세스에는 서로 다른 예약 키워드 집합이 있습니다. 이러한 문제로 인해로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 마이그레이션이 실패할 수 있습니다. 다음 표를 사용 하 여 가능한 마이그레이션 문제와 이러한 문제에 대해 수행할 수 있는 작업에 대해 알아보세요.  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>마이그레이션에 영향을 줄 수 있는 데이터베이스 설정 또는 기능  
  
|데이터베이스 설정 또는 기능에 액세스|마이그레이션 문제|  
|--------------------------------------|-------------------|  
|액세스 테이블은 고유 인덱스를 포함 하지 않습니다.|고유 인덱스가 없는 테이블이로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션되면 마이그레이션 후 테이블을 수정할 수 없습니다. 이로 인해 응용 프로그램 호환성 문제가 발생할 수 있습니다.<br /><br />Access 데이터베이스 개체를 변환할 때 출력 창에는 고유 인덱스가 없는 모든 액세스 테이블이 나열 됩니다.<br /><br />변환 하는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 기본 키를 추가 하는 액세스 권한을 구성할 수 있습니다. 자세한 내용은 [프로젝트 설정 (변환)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)을 참조 하세요.|  
|Access 테이블에는 복제 열이 있습니다.|복제 시스템 열을 포함 하는 액세스 테이블이로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션되면 마이그레이션 후 Jet 복제 기능이 손상 됩니다.<br /><br />마이그레이션 후에는 복제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 데이터베이스의 동기화 된 복사본을 유지 하는 것이 좋습니다.|  
|고유 인덱스가 있는 Access 테이블에는 null 값이 여러 개 포함 되어 있습니다.|에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]고유 인덱스가 여러 null을 허용 하지 않기 때문에 null 값이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]여러 개인 고유 인덱스가 있는 테이블에 대 한 액세스를로 전송할 수 없습니다. 이러한 테이블에 대 한 마이그레이션이 실패 합니다.<br /><br />SSMA는 평가 보고서에서이 문제에 플래그를 지정 합니다. 평가 보고서를 만들려면 [변환에 대 한 액세스 데이터베이스 개체 평가](assessing-access-database-objects-for-conversion-accesstosql.md)를 참조 하세요.<br /><br />이 문제가 발생 하는 경우 기본 키에 중복 된 null 값이 없는지 확인 해야 합니다. 또는 여러 null 값을 포함 하는 고유 인덱스 또는 기본 키를 제거 해야 합니다.|  
|Access 테이블에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 범위를 벗어난 날짜 값이 포함 되어 있습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Datetime** 형식은 1 년 1 월 1753 ~ 31 년 12 월 9999의 범위에서 날짜를 허용 합니다. 액세스는 1 년 1 월 100 ~ 31 년 12 월 9999 범위의 날짜를 허용 합니다.<br /><br />SSMA는 평가 보고서에서이 문제에 플래그를 지정 합니다. 평가 보고서를 만들려면 [변환에 대 한 액세스 데이터베이스 개체 평가](assessing-access-database-objects-for-conversion-accesstosql.md)를 참조 하세요.<br /><br />에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 범위를 벗어난 날짜를 확인 하는 방법을 구성할 수 있습니다. 자세한 내용은 [프로젝트 설정 (마이그레이션)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)을 참조 하세요.|  
|액세스의 인덱스 길이가 900 바이트를 초과 합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인덱스에는 인덱스 키 열의 전체 크기에 대 한 900 바이트 제한이 있습니다. Access 테이블에서 더 큰 인덱스를 사용 하는 경우 SSMA는 경고를 표시 합니다.<br /><br />데이터 마이그레이션을 계속 하면 마이그레이션이 실패할 수 있습니다.|  
|액세스 개체 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 키워드 이거나 특수 문자를 포함 합니다.|에 액세스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하 고 다른 예약 키워드 집합과 특수 문자 집합을 사용 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 키워드를 사용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하 여 이름이 지정 되거나 "select" 또는 [select]. p와 같이 대괄호로 묶은 식별자 또는 따옴표 붙은 식별자를 사용 하는 경우 특수 문자를 포함 하는 개체를 허용 합니다. 자세한 내용은 온라인 설명서의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "구분 식별자 (데이터베이스 엔진)"를 참조 하십시오.<br /><br />**참고:** 따옴표를 사용 하 여 식별자를 구분 하려면 QUOTED_IDENTIFIER 설정 해야 합니다.<br /><br />예를 들어 `CREATE TABLE [schema](c1 [FOR])` 은 **스키마** 및가 예약 키워드인 **경우에도** 유효한 문입니다. 또한 테이블 `CREATE TABLE [xxx*yyy](c1 x&y)` 및 열 이름에 ** \&#42;** 및 **&amp;** 의 특수 문자가 포함 되어 있더라도는 유효한 문입니다.<br /><br />이러한 개체를 참조 하는 모든 쿼리는 대괄호 또는 따옴표를 사용 하 여 이름도 사용 해야 합니다. 예를 들어 쿼리가 `SELECT * FROM schema` 실패 합니다. 올바른 쿼리는 `SELECT * FROM [schema]`입니다.<br /><br />Access 데이터베이스 개체를 변환할 때 출력 창에는 키워드나 특수 문자를 사용 하는 모든 액세스 테이블이 나열 됩니다. Access에서 테이블을 수정한 다음 데이터베이스를 제거 하 고 다시 추가할 수 있습니다. 또는 쿼리에서 대괄호 또는 따옴표를 사용 하 여 식별자를 구분할 수 있도록 해당 개체를 참조 하는 쿼리를 수정할 수 있습니다. 쿼리를 수정 하지 않으면 액세스 응용 프로그램에서 오류를 반환 하거나 다른 문제가 있을 수 있습니다.|  
|필드 크기는 기본 키/외래 키 관계에 따라 달라 집니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 foreign key 제약 조건이 다른 데이터 형식이 나 크기의 열을 연결 하는 Jet 기능을 지원 하지 않습니다.<br /><br />Access 데이터베이스 개체를 변환할 때 출력 창에로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]변환 되지 않을 기본 키/외래 키 제약 조건이 나열 됩니다. Access 열에서 데이터 형식 및 크기를 변경 하 여 데이터를 일치 시킬 수 있습니다. 그런 다음 Access 데이터베이스를 제거 하 고 다시 추가 합니다. 또는에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이러한 제약 조건이 생성 되지 않지만 데이터를 마이그레이션할 수 있습니다.|  
|액세스 관계에서 참조 되는 테이블에는 기본 키와 고유 인덱스가 모두 포함 되지 않습니다.|액세스는 참조 된 테이블에 기본 키 또는 고유 인덱스가 없는 테이블 간의 관계를 허용 합니다. 그러나이는에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]지원 되지 않습니다.<br /><br />Access 데이터베이스 개체를 변환할 때 출력 창에는 관계가 있지만 primary key 또는 unique 인덱스가 없는 테이블이 나열 됩니다. 테이블을 변경 하 여 기본 키 또는 고유 인덱스를 추가한 다음 Access 데이터베이스를 제거 하 고 다시 추가할 수 있습니다. 또는 테이블 간의 관계가 중단 되더라도 데이터를 마이그레이션할 수 있습니다.|  
|Access 테이블에는 하이퍼링크 열이 있습니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 **하이퍼링크** 열을 지원 하지 않습니다. 대신 열은 Access memo 열 처럼 처리 됩니다. 기본적으로 이러한 열은의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **nvarchar (max)** 열로 변환 됩니다. 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 [원본 및 대상 데이터 형식 매핑](mapping-source-and-target-data-types-accesstosql.md)을 참조 하세요.|  
|기본 또는 유효성 검사 규칙 식에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 변환 하거나 SQL Azure 수 없는 액세스 함수가 포함 되어 있습니다.|기본 식 또는 유효성 검사 규칙 액세스에는 액세스 시스템 함수 또는에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 매핑되지 않거나 SQL Azure 않는 사용자 정의 함수가 포함 될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 매핑되지 않는 함수를 사용 하면 기본 식 또는 유효성 검사 규칙을에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로드 하거나 SQL Azure 수 없습니다.|  
  
## <a name="see-also"></a>참고 항목  
[Access 데이터베이스에서 마이그레이션 준비](preparing-access-databases-for-migration-accesstosql.md)  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
