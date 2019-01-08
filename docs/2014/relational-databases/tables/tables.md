---
title: 테이블 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server]
- table components [SQL Server]
ms.assetid: 82d7819c-b801-4309-a849-baa63083e83f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7a456d68283d81cf7eb4f879d76f086484c5e052
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52782885"
---
# <a name="tables"></a>테이블
  테이블은 데이터베이스의 모든 데이터를 포함하는 데이터베이스 개체입니다. 테이블에서 데이터는 스프레드시트와 비슷한 논리적인 행 및 열 형식으로 구성됩니다. 각 행은 고유한 레코드를 나타내며 각 열은 레코드 내의 필드를 나타냅니다. 예를 들어 회사 사원 데이터가 들어 있는 테이블은 각 사원에 대한 행과 사원 번호, 이름, 주소, 직책 및 집 전화번호와 같은 자세한 사원 정보를 나타내는 열로 구성할 수 있습니다.  
  
-   데이터베이스의 테이블 수는 데이터베이스에 허용되는 개체 수(2,147,483,647)로만 제한됩니다. 표준 사용자 정의 테이블에는 최대 1,024개의 열을 사용할 수 있습니다. 테이블의 행 수는 서버의 저장 용량으로만 제한됩니다.  
  
-   테이블과 테이블의 각 열에 속성을 할당하여 허용되는 데이터 및 기타 속성을 제어할 수 있습니다. 예를 들어, 열에 대한 제약 조건을 만들어 Null 값을 금지하거나 값이 지정되지 않은 경우 기본 값을 제공할 수 있으며, 고유성을 적용하거나 테이블 간의 관계를 정의하는 테이블에 대한 키 제약 조건을 할당할 수 있습니다.  
  
-   행별로 또는 페이지별로 테이블의 데이터를 압축할 수 있습니다. 데이터 압축을 사용하면 한 페이지에 더 많은 행을 저장할 수 있습니다. 자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하세요.  
  
## <a name="types-of-tables"></a>테이블 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 기본 사용자 정의 테이블의 표준 역할 외에도 데이터베이스에서 특수한 용도로 사용되는 다음과 같은 테이블 유형을 제공합니다.  
  
 분할된 테이블  
 분할된 테이블은 데이터가 수평 분할된 단위로 되어 데이터베이스의 여러 파일 그룹에 분산될 수 있는 테이블입니다. 분할을 사용하면 데이터 하위 집합을 빠르고 효율적으로 액세스하거나 관리하면서 동시에 전체 컬렉션의 무결성을 유지할 수 있으므로 큰 테이블 또는 인덱스를 더욱 편리하게 관리할 수 있습니다. 기본적으로 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 은 최대 15,000개의 파티션을 지원합니다. 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)을 참조하세요.  
  
 임시 테이블  
 임시 테이블은 `tempdb`에 저장됩니다. 임시 테이블에는 로컬 및 전역의 두 가지 유형이 있습니다. 이 두 유형은 이름, 표시 여부 및 가용성 면에서 서로 다릅니다. 로컬 임시 테이블은 이름이 한 개의 숫자 기호(#)로 시작하며 사용자의 현재 연결에만 표시되고 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스와의 연결을 끊으면 삭제됩니다. 전역 임시 테이블은 이름이 두 개의 숫자 기호(##)로 시작하며 테이블 작성 후 모든 사용자에게 표시되고 테이블을 참조하는 모든 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스와의 연결을 끊으면 삭제됩니다.  
  
 시스템 테이블  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 서버와 서버의 모든 테이블에 대한 구성을 정의하는 데이터를 시스템 테이블이라고 알려진 특수한 테이블 집합에 저장합니다. 사용자는 시스템 테이블을 직접 쿼리하거나 업데이트할 수 없습니다. 시스템 테이블의 정보는 시스템 뷰를 통해 사용할 수 있습니다. 자세한 내용은 [시스템 뷰&#40;Transact-SQL&#41;](/sql/t-sql/language-reference)를 참조하세요.  
  
 넓은 테이블  
 넓은 테이블에서는 [스파스 열](use-sparse-columns.md) 을 사용하여 테이블이 포함할 수 있는 전체 열을 최대 30,000개까지 늘립니다. 스파스 열은 Null 값에 대해 최적화된 저장소가 있는 일반 열입니다. 스파스 열을 사용하면 Null 값에 대한 공간 요구 사항이 줄어드는 반면 Null이 아닌 값을 검색하는 데 더 많은 오버헤드가 발생합니다. 넓은 테이블은 테이블의 모든 스파스 열을 구조화된 출력으로 결합하는 형식화되지 않은 XML 표현인 [열 집합](use-column-sets.md)을 정의했습니다. 인덱스 및 통계 수도 각각 1,000개와 30,000개로 늘어납니다. 넓은 테이블 행의 최대 크기는 8,019바이트입니다. 따라서 특정 행에 포함된 대부분의 데이터는 NULL이어야 합니다. 넓은 테이블에 있는 비스파스 열과 계산 열을 더한 최대 개수는 1,024개입니다.  
  
 넓은 테이블은 성능에 다음과 같은 영향을 미칠 수 있습니다.  
  
-   넓은 테이블을 사용하면 테이블에서 인덱스를 유지 관리하는 비용이 증가할 수 있습니다. 넓은 테이블의 인덱스 수는 비즈니스 논리에 필요한 인덱스 수로 제한하는 것이 좋습니다. 인덱스 수가 늘어나면 DML 컴파일 시간과 메모리 요구 사항도 함께 늘어납니다. 비클러스터형 인덱스는 데이터 하위 집합에 적용되는 필터링된 인덱스여야 합니다. 자세한 내용은 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)을(를) 참조하세요.  
  
-   애플리케이션은 넓은 테이블에서 열을 동적으로 추가하고 제거할 수 있습니다. 열을 추가하거나 제거하면 컴파일된 쿼리 계획도 함께 무효화됩니다. 스키마의 변동 정도가 최소화되도록 예상 작업에 맞게 애플리케이션을 디자인하는 것이 좋습니다.  
  
-   넓은 테이블에서 데이터를 추가 및 제거하면 성능에 영향을 줄 수 있습니다. 데이터 테이블이 최소한으로 변경되도록 예상 작업에 맞게 애플리케이션을 디자인해야 합니다.  
  
-   넓은 테이블에서 클러스터링 키의 여러 행을 업데이트하는 DML 문의 실행은 가급적 제한해야 합니다. 이러한 문은 컴파일 및 실행에 많은 메모리 리소스가 필요할 수 있습니다.  
  
-   넓은 테이블에서는 파티션 전환 작업의 속도가 느리고 처리하는 데 많은 양의 메모리가 필요할 수 있습니다. 성능 및 메모리 요구 사항은 원본 및 대상 파티션에 있는 전체 열 개수와 비례합니다.  
  
-   넓은 테이블에서 특정 열을 업데이트하는 업데이트 커서는 FOR UPDATE 절에서 열을 명시적으로 나열해야 합니다. 이렇게 하면 커서를 사용할 때 성능을 최적화하는 데 도움이 됩니다.  
  
## <a name="common-table-tasks"></a>공통 테이블 태스크  
 다음 표에서는 테이블 만들기 또는 수정과 관련된 공통 태스크의 링크를 제공합니다.  
  
|테이블 태스크|항목|  
|-----------------|-----------|  
|테이블을 만드는 방법을 설명합니다.|[테이블 만들기&#40;데이터베이스 엔진&#41;](create-tables-database-engine.md)|  
|테이블을 삭제하는 방법을 설명합니다.|[테이블 삭제&#40;데이터베이스 엔진&#41;](delete-tables-database-engine.md)|  
|기존 테이블의 열이 일부 또는 모두 포함된 새 테이블을 만드는 방법을 설명합니다.|[테이블 복제](duplicate-tables.md)|  
|테이블의 이름을 바꾸는 방법을 설명합니다.|[테이블 이름 바꾸기&#40;데이터베이스 엔진&#41;](rename-tables-database-engine.md)|  
|테이블의 속성을 보는 방법을 설명합니다.|[테이블 정의 보기](view-the-table-definition.md)|  
|뷰 또는 저장 프로시저와 같은 다른 개체가 테이블에 종속되는지 여부를 결정하는 방법을 설명합니다.|[테이블의 종속성 보기](view-the-dependencies-of-a-table.md)|  
  
 다음 표에서는 테이블에서 열 만들기 또는 수정과 관련된 공통 태스크에 대한 링크를 제공합니다.  
  
|열 태스크|항목|  
|------------------|-----------|  
|기존 테이블에 열을 추가하는 방법을 설명합니다.|[테이블에 열 추가&#40;데이터베이스 엔진&#41;](add-columns-to-a-table-database-engine.md)|  
|테이블에서 열을 삭제하는 방법을 설명합니다.|[테이블에서 열 삭제](delete-columns-from-a-table.md)|  
|열의 이름을 변경하는 방법을 설명합니다.|[열 이름 바꾸기&#40;데이터베이스 엔진&#41;](rename-columns-database-engine.md)|  
|열 정의만 복사하거나 열 정의와 데이터를 모두 복사하여 한 테이블에서 다른 테이블로 열을 복사하는 방법을 설명합니다.|[한 테이블에서 다른 테이블로 열 복사&#40;데이터베이스 엔진&#41;](copy-columns-from-one-table-to-another-database-engine.md)|  
|데이터 형식 또는 다른 속성을 변경하여 열 정의를 수정하는 방법을 설명합니다.|[열 수정&#40;데이터베이스 엔진&#41;](modify-columns-database-engine.md)|  
|열이 표시되는 순서를 변경하는 방법을 설명합니다.|[테이블에서 열 순서 변경](change-column-order-in-a-table.md)|  
|테이블에서 계산 열을 만드는 방법을 설명합니다.|[테이블에서 계산 열 지정](specify-computed-columns-in-a-table.md)|  
|열의 기본값을 지정하는 방법을 설명합니다. 다른 값을 제공하지 않으면 이 값이 사용됩니다.|[열의 기본값 지정](specify-default-values-for-columns.md)|  
  
## <a name="see-also"></a>관련 항목  
 [PRIMARY KEY 및 FOREIGN KEY 제약 조건](primary-and-foreign-key-constraints.md)   
 [UNIQUE 제약 조건 및 CHECK 제약 조건](unique-constraints-and-check-constraints.md)  
  
  
