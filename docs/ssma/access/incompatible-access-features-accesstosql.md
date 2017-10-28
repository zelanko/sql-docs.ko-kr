---
title: "호환 되지 않는 액세스 기능 (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b60bab1d71142a74c8558ce05a6ca96451e7cfc9
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="incompatible-access-features-accesstosql"></a>호환 되지 않는 액세스 기능 (AccessToSQL)
모든 액세스 데이터베이스 기능을 호환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 액세스 예약 된 키워드 집합은 및입니다. 발급 하 여 성공적인 마이그레이션을 방해할 수 있습니다 이러한 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 가능한 마이그레이션 문제 및 //office.microsoft.com/ 수행할 수 있는 작업에 대 한 자세한 내용은 다음 표를 사용 합니다.  
  
## <a name="database-settings-or-features-that-might-affect-migration"></a>데이터베이스 설정 또는 마이그레이션에 영향을 줄 수 있는 기능  
  
|데이터베이스 설정 또는 기능에 액세스|마이그레이션 문제|  
|--------------------------------------|-------------------|  
|Access 테이블에 고유 인덱스를 사용할 필요가 없습니다.|고유 인덱스가 없는 테이블을 마이그레이션된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 마이그레이션 후 테이블을 수정할 수 없습니다. 응용 프로그램 호환성 문제가 발생할 수 있습니다.<br /><br />Access 데이터베이스 개체를 변환 하는 경우 출력 창에는 고유 인덱스를 갖지 않는 Access 테이블이 나열 됩니다.<br /><br />기본 키를 추가에 대 한 액세스를 구성할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 변환 하는 동안 테이블입니다. 자세한 내용은 참조 [프로젝트 설정 (변환)](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)합니다.|  
|Access 테이블에는 복제 열.|복제 시스템 열이 포함 된 Access 테이블을 마이그레이션된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 마이그레이션 후 Jet 복제 기능이 손상 됩니다.<br /><br />마이그레이션 후 사용해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 복제 데이터베이스의 동기화 된 복사본을 유지 관리 합니다.|  
|고유 인덱스는 모두 access 테이블 여러 null 값을 포함 합니다.|여러 null 값이 있는 고유 인덱스는 모두 access 테이블에 전송할 수 없으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]때문에에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 고유 인덱스에 여러 null 허용 되지 않습니다. 이러한 테이블에 대 한 마이그레이션이 실패 합니다.<br /><br />SSMA는 평가 보고서에서이 문제는 플래그입니다. 평가 보고서를 만들려면 참조 [변환에 대 한 Access 데이터베이스 개체가 평가](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441)합니다.<br /><br />이 문제가 있는 경우에 기본 키에 중복 된 null 값이 없는지 확인 해야 합니다. 또는 기본 키 또는 여러 개의 null 값을 포함 하는 고유 인덱스를 제거 해야 합니다.|  
|Access 테이블의 날짜 값을 포함 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 범위입니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime** 31 년 12 월 1753 1의 범위에서 날짜를 수락 하는 형식 9999만 합니다. 액세스 범위는 1 년 1 월 100 Dec 31에서으로 날짜를 입력할 9999입니다.<br /><br />SSMA는 평가 보고서에서이 문제는 플래그입니다. 평가 보고서를 만들려면 참조 [변환에 대 한 Access 데이터베이스 개체가 평가](http://msdn.microsoft.com/en-us/8b9e23d6-da62-437a-8c05-8ad2628b9441)합니다.<br /><br />SSMA 날짜를 확인 하는 방법을 구성할 수 있습니다 아웃 되 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 범위입니다. 자세한 내용은 참조 [프로젝트 설정 (마이그레이션)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d)합니다.|  
|Access에서 인덱스 길이 900 바이트를 초과 합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]인덱스는 인덱스 키 열의 총 크기에 대 한 900 바이트 제한 합니다. 더 큰 인덱스를 사용 하는 Access 테이블 SSMA 경고가 표시 됩니다.<br /><br />마이그레이션 데이터를 계속 진행 하면 마이그레이션이 실패할 수 있습니다.|  
|액세스 개체 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 키워드 또는 특수 문자를 포함 합니다.|액세스 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 여러 집합이 예약 된 키워드 및 특수 문자. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]사용 하 여 명명 된 개체를 수용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 키워드 또는 하는 경우 "select" 같은 대괄호로 묶인 또는 따옴표 붙은 식별자를 사용 하거나 [선택].p 특수 문자를 포함 합니다. 자세한 내용은 "구분 기호로 분리 된 식별자 (데이터베이스 엔진)"를 참조 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 온라인 설명서.<br /><br />**참고:** 식별자를 구분할 때는 따옴표를 사용 하려면 SET QUOTED_IDENTIFIER ON 이어야 합니다.<br /><br />예를 들어 `CREATE TABLE [schema](c1 [FOR])` 유효한, 문인 경우에 **스키마** 및 **에 대 한** 예약 키워드가 있습니다. 또한 `CREATE TABLE [xxx*yyy](c1 x&y)` 테이블 및 열 이름이 특수 문자를 포함 하는 경우에 유효한 문은  **\&#42;** 및  **&amp;** 합니다.<br /><br />해당 개체를 참조 하는 모든 쿼리 이름을 대괄호 또는 따옴표를 사용 해야 합니다. 예를 들어 쿼리 `SELECT * FROM schema` 실패 합니다. 올바른 쿼리는: `SELECT * FROM [schema]`합니다.<br /><br />Access 데이터베이스 개체를 변환 하는 경우 출력 창은 키워드 또는 특수 문자를 사용 하는 모든 액세스 테이블을 나열 합니다. Access에서 테이블을 수정 하 고 제거 하 고 수는 데이터베이스를 다시 추가 또는 쿼리 대괄호 또는 따옴표를 사용 하 여 식별자를 구분할 수 있도록 해당 개체를 참조 하는 쿼리를 수정할 수 있습니다. 쿼리를 수정 하면 액세스 응용 프로그램 오류를 반환할 수도 다른 문제가 있습니다.|  
|기본 키/외래 키 관계 필드 크기에 따라 다릅니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]열 데이터 형식이 나 다른 외래 키 제약 조건에 따라 크기 조정 된 연결의 Jet 기능을 지원 하지 않습니다.<br /><br />출력 창 모든 기본 키/외래 키 제약 조건을으로 변환 하지 나열 Access 데이터베이스 개체를 변환할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 일치 하 고 다음을 제거 하 고 있음을 Access 데이터베이스를 다시 추가 데이터 형식 및 열 액세스에서 크기를 변경할 수 있습니다. 이러한 제약 조건에 만들 수는 있지만 데이터를 마이그레이션할 수 있습니다 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.|  
|액세스 관계의 참조 된 테이블에 기본 키도 아니고 고유 인덱스를 가집니다.|액세스는 참조 되는 테이블 기본 키 또는 고유 인덱스가 있어야 하지 않는 테이블 간의 관계를 허용 합니다. 그러나이에서 지원 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.<br /><br />Access 데이터베이스 개체를 변환 하는 경우 관계 하지만 기본 키 또는 고유 인덱스가 없는 테이블 출력 창에 나열 됩니다. 기본 키 또는 고유 인덱스를 추가 하 고 다음 제거 하 고 다시 추가 Access 데이터베이스 테이블을 변경할 수 있습니다. 또는 테이블 사이의 관계 손상 됩니다. 하지만 데이터를 마이그레이션할 수 있습니다.|  
|Access 테이블에는 하이퍼링크 열.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]지원 하지 않습니다 **하이퍼링크** 열입니다. 대신 열 액세스 메모 열 처럼 취급 됩니다. 기본적으로 이러한 열으로 변환 됩니다 **nvarchar (max)** 열 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 매핑을 사용자 지정할 수 있습니다. 자세한 내용은 참조 [매핑 소스 및 대상 데이터 형식](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9)합니다.|  
|변환할 수 없는 액세스 함수를 포함 하는 기본 또는 유효성 검사 규칙 식 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다.|액세스 시스템 함수 또는 사용자 정의 함수에 매핑되지 않는 기본 액세스 식 또는 유효성 검사 규칙이 포함 될 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다. 에 매핑되지 않는 함수를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure은 기본 식 또는 유효성 검사 규칙을 로드 하지 못하도록 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다.|  
  
## <a name="see-also"></a>관련 항목:  
[Access 데이터베이스 마이그레이션을 준비](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

