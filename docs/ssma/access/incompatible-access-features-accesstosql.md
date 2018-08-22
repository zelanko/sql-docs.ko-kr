---
title: 호환 되지 않는 Access 기능 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2c5819ffe66cfb6d80e19973cc9b3f2cba0251df
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392880"
---
# <a name="incompatible-access-features-accesstosql"></a>호환 되지 않는 Access 기능 (AccessToSQL)
모든 액세스 데이터베이스 기능을 사용 하 여 호환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 액세스 예약 된 키워드 집합은 및입니다. 문제에 성공적인 마이그레이션을 방해할 수 있습니다 이러한 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 가능한 마이그레이션 문제 및 수행할 수 있는 정보에 대해 자세히 알아보려면 다음 표를 사용 합니다.  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>데이터베이스 설정 또는 마이그레이션에 영향을 줄 수 있는 기능  
  
|데이터베이스 설정 또는 기능에 액세스|마이그레이션 문제|  
|--------------------------------------|-------------------|  
|테이블 액세스에 고유 인덱스를 사용할 필요가 없습니다.|고유 인덱스가 없는 테이블을 마이그레이션된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 마이그레이션 후 테이블을 수정할 수 없습니다. 이 응용 프로그램 호환성 문제가 발생할 수 있습니다.<br /><br />Access 데이터베이스 개체를 변환 하는 경우 출력 창에는 고유 인덱스에 있지 않은 Access 테이블이 나열 됩니다.<br /><br />기본 키에 추가에 대 한 액세스를 구성할 수 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 변환 하는 동안 테이블입니다. 자세한 내용은 [프로젝트 설정 (변환)](http://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)합니다.|  
|테이블 액세스 복제 열 경우|복제 시스템 열을 포함 하는 Access 테이블을 마이그레이션된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 마이그레이션 후 Jet 복제 기능이 중단 됩니다.<br /><br />마이그레이션 후 사용 하 여 것이 좋습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 데이터베이스의 동기화 된 복사본을 유지 관리 합니다.|  
|여러 null 값을 포함 하는 고유 인덱스가 있는 테이블을 액세스 합니다.|여러 null 값을 가진 고유 인덱스가 있는 테이블 액세스를 전송할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]때문에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 고유 인덱스에 여러 null 허용 하지 않습니다. 이러한 테이블에 대 한 마이그레이션이 실패 합니다.<br /><br />SSMA는 평가 보고서에서이 문제는 플래그입니다. 평가 보고서를 참조 하세요 [변환을 위해 Access 데이터베이스 개체 평가](assessing-access-database-objects-for-conversion-accesstosql.md)합니다.<br /><br />이 문제가 발생할 경우에 기본 키에 중복 된 null 값이 없는지 확인 해야 합니다. 또는 기본 키 또는 여러 개의 null 값을 포함 하는 고유 인덱스를 제거 해야 합니다.|  
|테이블 액세스의 날짜 값을 포함 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 범위입니다.|합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** 1 1753 년 1 월 12 월 31 범위의 날짜를 수락 하는 형식 9999만 합니다. 액세스 허용 31 Dec 1 년 1 월 100 범위의 날짜가 9999입니다.<br /><br />SSMA는 평가 보고서에서이 문제는 플래그입니다. 평가 보고서를 참조 하세요 [변환을 위해 Access 데이터베이스 개체 평가](assessing-access-database-objects-for-conversion-accesstosql.md)합니다.<br /><br />SSMA에서 날짜를 확인 하는 방법을 구성할 수 있습니다 개는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 범위입니다. 자세한 내용은 [프로젝트 설정 (마이그레이션)](http://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d)합니다.|  
|액세스에 대 한 인덱스 길이 900 바이트를 초과 합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인덱스는 인덱스 키 열의 총 크기는 900 바이트 한도 갖습니다. 큰 인덱스를 사용 하는 테이블에 액세스 하는 경우 SSMA 경고가 표시 됩니다.<br /><br />데이터 마이그레이션을 사용 하 여 계속 하면 마이그레이션이 실패할 수 있습니다.|  
|액세스 개체 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 키워드 또는 특수 문자를 포함 합니다.|액세스 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다른 예약 된 키워드 및 특수 문자 집합입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하 여 이름이 지정 된 개체를 수락할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 키워드 또는 "select" 같은 대괄호로 묶은 또는 따옴표 붙은 식별자를 사용 하거나 [선택].p 경우 특수 문자를 포함 합니다. 자세한 내용은 나오는 "구분 기호로 분리 됨 식별자 (데이터베이스 엔진)" [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onl 온라인 설명서.<br /><br />**참고:** 구분 식별자에 따옴표를 사용 하려면 SET quoted_identifier가 ON 이어야 합니다.<br /><br />예를 들어 `CREATE TABLE [schema](c1 [FOR])` 는 유효한 문이 **스키마** 하 고 **에 대 한** 은 예약 된 키워드. 또한 `CREATE TABLE [xxx*yyy](c1 x&y)` 는 테이블 및 열 이름에 특수 문자를 포함 하는 경우에 유효한 문이  **\&#42;** 하 고 **&amp;** 합니다.<br /><br />또한 이러한 개체를 참조 하는 모든 쿼리 대괄호 또는 따옴표를 사용 하 여 이름을 사용 해야 합니다. 예를 들어, 쿼리 `SELECT * FROM schema` 실패 합니다. 올바른 쿼리는: `SELECT * FROM [schema]`합니다.<br /><br />Access 데이터베이스 개체를 변환할 때는 키워드 또는 특수 문자를 사용 하는 모든 액세스 테이블 출력 창에 나열 됩니다. Access에서 테이블을 수정 하 고 제거 하 고 수는 데이터베이스를 다시 추가 또는 쿼리를 사용 하 여 대괄호 또는 따옴표로 구분 식별자에는 해당 개체를 참조 하는 쿼리를 수정할 수 있습니다. 쿼리를 수정 하면 액세스 응용 프로그램 오류를 반환할 수도 다른 문제가 있습니다.|  
|필드 크기는 기본 키/외래 키 관계에서 다릅니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다른 데이터 형식 또는 foreign key 제약 조건 크기는 열을 연결 하는 Jet 기능을 지원 하지 않습니다.<br /><br />출력 창의 모든 기본 키/외래 키 제약 조건을에 변환 되지 것입니다 표시 Access 데이터베이스 개체를 변환 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 일치 하 고 다음 제거 하 고 있도록 Access 데이터베이스를 다시 추가 데이터 형식 및 열 액세스에서 크기를 변경할 수 있습니다. 이러한 제약 조건에서 생성 되지 것입니다 하지만 데이터를 마이그레이션할 수 있습니다 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
|액세스 관계의 참조 테이블 기본 키도 아니고 고유 인덱스를 가집니다.|액세스 위치는 참조 테이블에 없는 기본 키 또는 고유 인덱스는 테이블 간의 관계를 허용 합니다. 그러나에서 지원 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.<br /><br />Access 데이터베이스 개체를 변환 하면 출력 창 관계 하지만 기본 키 또는 고유 인덱스가 있는 테이블이 나열 됩니다. 기본 키 또는 고유 인덱스를 추가 하 고 다음 제거 하 고 다시 추가 Access 데이터베이스 테이블을 변경할 수 있습니다. 또는 테이블 간의 관계 끊어집니다. 하지만 데이터를 마이그레이션할 수 있습니다.|  
|테이블 액세스 하이퍼링크 열 경우|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지원 하지 않습니다 **하이퍼링크** 열입니다. 대신 열 액세스 메모 열 처럼 취급 됩니다. 기본적으로 이러한 열은 변환할 **nvarchar (max)** 열에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 [매핑 원본 및 대상 데이터 형식](mapping-source-and-target-data-types-accesstosql.md)합니다.|  
|변환할 수 없는 액세스 함수를 포함 하는 기본 또는 유효성 검사 규칙 식 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다.|액세스 시스템 함수 또는 사용자 정의 함수에 매핑되지 않는 기본 액세스 식 또는 유효성 검사 규칙이 포함 될 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. 에 매핑되지 않는 함수를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 기본 식 또는 유효성 검사 규칙을 로드 하지 못하도록 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다.|  
  
## <a name="see-also"></a>관련 항목  
[Access 데이터베이스 마이그레이션 준비](preparing-access-databases-for-migration-accesstosql.md)  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
