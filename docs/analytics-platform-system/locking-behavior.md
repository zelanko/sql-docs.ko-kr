---
title: 잠금 동작
description: 병렬 데이터 웨어하우스가 잠금을 사용 하 여 트랜잭션의 무결성을 확인 하 고 여러 사용자가 동시에 데이터에 액세스할 때 데이터베이스의 일관성을 유지 하는 방법을 알아봅니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f3ecf5cf783b707b75c90dfa70d502e3c81d28c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401007"
---
# <a name="locking-behavior-in-parallel-data-warehouse"></a>병렬 데이터 웨어하우스의 잠금 동작
병렬 데이터 웨어하우스가 잠금을 사용 하 여 트랜잭션의 무결성을 확인 하 고 여러 사용자가 동시에 데이터에 액세스할 때 데이터베이스의 일관성을 유지 하는 방법을 알아봅니다.  
  
## <a name="Basics"></a>잠금 기본 사항  
**모드**  
  
SQL Server PDW는 다음과 같은 네 가지 잠금 모드를 지원 합니다.  
  
단독  
배타적 잠금은 배타적 잠금을 보유 하 고 있는 트랜잭션이 완료 될 때까지 잠긴 개체를 읽거나 쓸 수 없습니다. 단독 잠금이 적용 되는 동안에는 모드의 다른 잠금을 사용할 수 없습니다. 예를 들어 DROP TABLE 및 CREATE DATABASE는 배타적 잠금을 사용 합니다.  
  
공유됨  
공유 잠금은 영향을 받는 개체에 대 한 배타적 잠금을 시작 하는 것을 금지 하지만 다른 모든 잠금 모드를 허용 합니다. 예를 들어 SELECT 문은 공유 잠금을 시작 하므로 여러 쿼리에서 선택 된 데이터에 동시에 액세스할 수 있지만 SELECT 문이 완료 될 때까지 읽을 레코드에 대 한 업데이트를 방지 합니다.  
  
ExclusiveUpdate  
ExclusiveUpdate 잠금은 잠겨 있는 개체에 대 한 쓰기를 금지 하지만 공유 잠금을 통해 읽을 수 있습니다. ExclusiveUpdate 잠금이 적용 되는 동안에는 다른 잠금이 허용 되지 않습니다. 예를 들어 데이터베이스 백업 및 복원 데이터베이스에는 배타적 업데이트 잠금이 사용 됩니다.  
  
대 한 sharedupdate  
SharedUpdate 잠금은 배타적 및 ExclusiveUpdate 잠금 모드를 금지 하 고 개체에 대 한 공유 및 SharedUpdate 잠금 모드를 허용 합니다. SharedUpdate는 개체를 수정 하지만 수정 하는 동안 읽기 액세스를 제한 하지 않습니다. 예를 들어 INSERT 및 UPDATE에는 SharedUpdate 잠금이 사용 됩니다.  
  
**리소스 클래스**  
  
잠금은 데이터베이스, 스키마, 개체 (테이블, 뷰 또는 프로시저), 응용 프로그램 (내부적으로 사용 됨), EXTERNALDATASOURCE, EXTERNALFILEFORMAT 및 SCHEMARESOLUTION (개체를 만들거나 변경 하는 동안 수행 되는 데이터베이스 수준 잠금)의 개체 클래스에서 유지 됩니다. 스키마 개체 또는 데이터베이스 사용자를 삭제 합니다. 이러한 개체 클래스는 [dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)의 object_type 열에 표시 될 수 있습니다.  
  
## <a name="Remarks"></a>일반적인 주의 사항  
데이터베이스, 테이블 또는 뷰에 잠금을 적용할 수 있습니다.  
  
SQL Server PDW는 구성 가능한 격리 수준을 구현 하지 않습니다. ANSI 표준에 정의 된 대로 READ_UNCOMMITTED 격리 수준을 지원 합니다. 그러나 읽기 작업은 READ_UNCOMMITTED에서 실행 되므로 실제로 차단 작업은 거의 발생 하지 않으며 시스템에서 경합이 발생할 수 있습니다.  
  
SQL Server PDW는 기본 SQL Server 엔진에 의존 하 여 잠금 및 동시성 제어를 구현 합니다. 작업이 동일한 노드 내에서 기본 SQL Server 교착 상태를 야기 하는 경우 SQL Server PDW는 SQL Server 교착 상태 검색 기능을 활용 하 고 차단 문 중 하나를 종료 합니다.  
  
> [!NOTE]  
> SQL Server는 잠금이 최신 잠금 요청에 의해 차단 될 때까지 기다리는 문을 허용 하지 않습니다. SQL Server PDW이 프로세스를 완전히 구현 하지 않았습니다. SQL Server PDW에서 새 공유 잠금에 대 한 연속 요청은 때때로 배타적 잠금에 대 한 이전 (대기 중) 요청을 차단할 수 있습니다. 예를 들어, **UPDATE** 문 (배타적 잠금 필요)은 일련의 **SELECT** 문에 부여 된 공유 잠금으로 차단할 수 있습니다. 차단 된 프로세스 ( [sys. dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) dvm을 검토 하 여 확인)를 해결 하려면 배타적 잠금이 충족 될 때까지 새 요청 제출을 중지 합니다.  
  
## <a name="lock-definition-table"></a>잠금 정의 테이블  
SQL Server는 다음과 같은 형식의 잠금을 지원 합니다. 모든 잠금 유형을 제어 노드에서 사용할 수 있는 것은 아니지만 계산 노드에서 발생할 수 있습니다.  
  
-   Sch-m-S (스키마 안정성). 특정 세션이 스키마 요소에 대해 스키마 안전성 잠금을 보유하고 있는 동안 테이블 또는 인덱스 등의 스키마 요소가 삭제되지 않도록 합니다.  
  
-   Sch-m-M (스키마 수정). 지정한 리소스의 스키마를 변경하려는 세션이 보유해야 하는 잠금 모드입니다. 다른 세션이 표시된 개체를 참조하지 않도록 합니다.  
  
-   S (공유). 보유 중인 세션이 리소스에 공유된 액세스를 할 수 있도록 권한을 부여합니다.  
  
-   U (업데이트). 업데이트될 리소스에 대해 업데이트 잠금을 획득하도록 합니다. 나중에 업데이트할 경우를 대비해 여러 세션에서 리소스를 잠근 경우 일반적인 교착 상태 발생을 방지하기 위해 사용됩니다.  
  
-   X (제외). 보유 중인 세션이 리소스에 배타적으로 액세스할 수 있도록 권한을 부여합니다.  
  
-   IS (내재 된 공유)입니다. 잠금 계층 구조의 일부 하위 리소스에 S 잠금을 설정하려는 의도를 표시합니다.  
  
-   IU (의도 업데이트). 잠금 계층 구조의 일부 하위 리소스에 U 잠금을 설정하려는 의도를 표시합니다.  
  
-   IX (의도 배타). 잠금 계층 구조의 일부 하위 리소스에 X 잠금을 설정하려는 의도를 표시합니다.  
  
-   SIU (공유 의도 업데이트). 잠금 계층 구조의 하위 리소스에 대한 업데이트 잠금을 획득하기 위해 리소스에 대한 공유된 액세스를 표시합니다.  
  
-   6 (공유 의도 배타). 잠금 계층 구조의 하위 리소스에 대한 배타적 잠금을 획득하기 위해 리소스에 대한 공유된 액세스를 표시합니다.  
  
-   UIX (업데이트 의도 배타). 잠금 계층 구조의 하위 리소스에 대한 배타적 잠금을 획득하기 위해 리소스에 업데이트 잠금을 보유함을 표시합니다.  
  
-   BU. 대량 작업에 사용합니다.  
  
-   RangeS_S (공유 키 범위 및 공유 리소스 잠금). 직렬화 가능 범위 검색을 표시합니다.  
  
-   RangeS_U (공유 키 범위 및 업데이트 리소스 잠금). 직렬화 가능 업데이트 검색을 표시합니다.  
  
-   RangeI_N (삽입 키 범위 및 Null 리소스 잠금). 새 키를 인덱스에 삽입하기 전에 범위를 테스트하는 데 사용됩니다.  
  
-   RangeI_S. RangeI_N 잠금과 S 잠금의 겹쳐진 부분에 의해 생성된 키 범위 변환 잠금입니다.  
  
-   RangeI_U. RangeI_N 잠금과 U 잠금의 겹쳐진 부분에 의해 생성된 키 범위 변환 잠금입니다.  
  
-   RangeI_X. RangeI_N 잠금과 X 잠금의 겹쳐진 부분에 의해 생성된 키 범위 변환 잠금입니다.  
  
-   RangeX_S. RangeI_N 잠금과 RangeS_S 잠금의 겹쳐진 부분에 의해 생성된 키 범위 변환 잠금입니다.  
  
-   RangeX_U. RangeI_N 잠금과 RangeS_U 잠금의 겹쳐진 부분에 의해 생성된 키 범위 변환 잠금입니다.  
  
-   RangeX_X (배타 키 범위 및 배타 리소스 잠금). 범위 내에서 키를 업데이트할 때 사용되는 변환 잠금입니다.  
  
## <a name="see-also"></a>참고 항목  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
