---
title: 기타 데이터베이스 엔진 업그레이드 문제 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], upgrading
ms.assetid: 78a1d8e8-fa97-476f-8777-84617d145340
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2890a61850526f7506713b3f900d67b8d41d0bfb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012139"
---
# <a name="other-database-engine-upgrade-issues"></a>기타 데이터베이스 엔진 업그레이드 문제
  다음은 최신 업그레이드 관리자 버전에서 감지할 수 없는 업그레이드 문제입니다. 아래에 나와 있는 문제를 검토하여 이러한 문제가 시스템에 줄 수 있는 잠재적 영향을 평가하십시오.  
  
## <a name="multiple-database-engine-deprecated-features"></a>여러 데이터베이스 엔진 기능이 지원되지 않음  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 옵션은 더 이상 지원되지 않습니다.  
  
-   BACKUP LOG의 NO_LOG 및 TRUNCATE_ONLY 옵션  
  
-   BACKUP TRANSACTION  
  
-   RESTORE TRANSACTION  
  
-   DUMP  
  
-   LOAD  
  
-   DBCC CONCURRENCYVIOLATION  
  
-   sp_addalias  
  
-   sp_addgroup  
  
-   sp_changegroup  
  
-   sp_dropgroup  
  
-   sp_helpgroup  
  
-   syssegments  
  
 VIA 프로토콜을 사용한 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대한 연결은 더 이상 사용되지 않습니다.  
  
## <a name="new-data-types"></a>새 데이터 형식  
 다음과 같은 데이터가 시스템 형식으로 예약됩니다. 업그레이드하기 전이나 후에 충돌하는 기존 사용자 정의 형식의 이름을 바꾸십시오.  
  
-   Geography  
  
-   geometry  
  
-   Datetime2  
  
-   HierarchyID  
  
## <a name="target-table-of-the-output-into-clause-cannot-have-any-defined-triggers"></a>OUTPUT INTO 절의 대상 테이블에는 정의된 트리거를 사용할 수 없음  
 테이블에 활성화 된 트리거가 있는 경우 대상 테이블에 대 한 출력은 지원 되지 않습니다.  
  
## <a name="compile-time-error-for-udfs-when-the-target-of-an-output-into-clause-is-a-table"></a>OUTPUT INTO 절의 대상이 테이블일 경우 UDF를 컴파일할 때 오류가 발생함  
 UDF(사용자 정의 함수)를 사용하여 데이터베이스 상태 수정 동작을 수행할 수 없습니다. 예를 들어 UDF는 테이블 변수를 제외한 모든 개체에 대해 DDL(CREATE/ALTER/DROP) 또는 DML(INSERT/UPDATE/DELETE) 동작을 수행할 수 없습니다.  
  
## <a name="merge-is-a-reserved-keyword"></a>MERGE는 예약 키워드입니다.  
 MERGE는 이제 완전 예약 키워드입니다. 애플리케이션에 MERGE라는 개체(테이블, 열 등)가 더 이상 포함될 수 없습니다.  
  
## <a name="rename-cdc-schema"></a>CDC 스키마 이름 바꾸기  
 CDC라는 스키마 이름이 있습니다. 데이터베이스에 **변경 데이터 캡처가** 설정 된 경우에는이 스키마 이름을 사용할 수 없습니다.  
  
 데이터베이스에 대 한 **변경 데이터 캡처** 를 사용 하도록 설정 하기 전에 CDC 스키마를 삭제 해야 합니다. 이 작업은 업그레이드하기 전이나 후에 수행할 수 있습니다. 스키마를 삭제하려면 다음 단계를 수행하십시오.  
  
1.  ALTER SCHEMA를 사용하여 CDC 스키마의 개체를 새 스키마 이름으로 이동합니다.  
  
2.  새 스키마에 있는 개체에 대한 사용 권한을 확인합니다.  
  
3.  필요에 따라 애플리케이션을 수정합니다.  
  
4.  DROP SCHEMA를 사용하여 CDC 스키마를 삭제합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
  
