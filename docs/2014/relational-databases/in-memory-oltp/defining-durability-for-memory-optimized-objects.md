---
title: 메모리 액세스에 최적화된 개체에 대한 내구성 정의 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0fe85fbf-8e8d-4983-96fd-d04b3c7d6d65
caps.latest.revision: 5
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6423f92f639c7408cd66c4bdcf91fae02afff1d0
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393497"
---
# <a name="defining-durability-for-memory-optimized-objects"></a>메모리 액세스에 최적화된 개체에 대한 내구성 정의
  메모리 내 OLTP는 완전한 ACID(원자성, 일관성, 격리 및 내구성) 속성을 보장합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 메모리 최적화 테이블의 컨텍스트에서 내구성은 다음과 같은 보증을 제공합니다.  
  
 트랜잭션 유지 기능  
 메모리 최적화 테이블에 DDL 또는 DML 변경을 적용한 완전한 내구성이 있는 트랜잭션을 커밋하면 메모리 최적화 내구성이 있는 테이블에 적용한 이 변경은 영구적이 됩니다.  
  
 지연된 내구성이 있는 트랜잭션을 메모리 최적화 테이블로 커밋하면 메모리 내 트랜잭션 로그가 디스크에 저장된 이후에만 트랜잭션이 내구성을 갖습니다.  
  
 다시 시작 내구성  
 
            [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 충돌이나 계획된 종료 후에 다시 시작되면 메모리 최적화 내구성이 있는 테이블이 다시 인스턴스화되어 종료나 충돌 전의 상태로 복원됩니다.  
  
 미디어 오류 내구성  
 실패했거나 손상된 디스크에 메모리 최적화 내구성이 있는 개체의 영구 복사본이 하나 이상 포함되어 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 및 복원 기능은 메모리 최적화 테이블을 새 미디어에 복원합니다.  
  
 메모리 최적화 테이블에는 두 가지 내구성 옵션이 있습니다.  
  
 SCHEMA_ONLY(내구성이 없는 테이블)  
 이 옵션은 인덱스를 포함한 테이블 스키마의 내구성을 보장합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 다시 시작하면 내구성이 없는 테이블이 다시 만들어지지만 데이터가 없이 시작됩니다. (이것은 다시 시작하면 테이블과 데이터가 손실되는 tempdb의 테이블과는 다릅니다.) 내구성이 없는 테이블을 만드는 일반적인 시나리오는 ETL 프로세스를 위한 준비 테이블 같은 임시 테이블을 저장하는 것입니다. SCHEMA_ONLY 내구성은 트랜잭션 로깅과 검사점을 방지하여 I/O 작업을 크게 줄일 수 있습니다.  
  
 SCHEMA_AND_DATA(내구성이 있는 테이블)  
 이 옵션은 스키마와 데이터 모두에 대한 내구성을 제공합니다. 데이터 내구성 수준은 트랜잭션을 완전 내구성으로 커밋할지 아니면 지연된 내구성으로 커밋할지에 따라 달라집니다. 완전한 내구성이 있는 트랜잭션은 디스크 기반 테이블과 유사하게 스키마 및 데이터에 대한 동일한 내구성 보증을 제공합니다. 지연된 내구성은 성능을 향상시키지만 서버 충돌이나 장애 조치(Failover)의 경우 데이터 손실을 발생시킬 수도 있습니다. 지연된 내구성에 자세한 내용은 [트랜잭션 내구성 제어](../logs/control-transaction-durability.md)를 참조하세요.  
  
 메모리 최적화 테이블의 스키마는 데이터베이스의 기본 파일 그룹에서 디스크 기반 테이블과 비슷하게 유지됩니다.  
  
 메모리 최적화 내구성이 있는 테이블의 데이터는 데이터 및 델타 파일 쌍에 저장됩니다.  
  
 메모리 최적화 테이블에 정의된 인덱스는 메타데이터에서만 유지되고 저장소에서는 유지되지 않습니다. 인덱스 구조는 메모리 최적화 테이블을 로드하는 과정에서 생성됩니다.  
  
 행은 DELETE 문에 의해 명시적으로 또는 UPDATE 문에 의해 간접적으로 삭제됩니다. UPDATE 작업은 삭제 후 삽입으로 실행됩니다. 행이 삭제되면 데이터 파일에는 아무런 변경이 없지만 삭제된 행을 식별하는 새로운 행이 해당 델타 파일에 추가됩니다.  
  
 복구 또는 복원 작업 중에 메모리 내 OLTP 엔진은 물리적 메모리에 로드하기 위해 데이터 및 델타 파일을 읽습니다. 로드 시간을 결정하는 요소는 다음과 같습니다.  
  
-   로드할 데이터의 양  
  
-   순차 I/O 대역폭  
  
-   파일 컨테이너 및 프로세서 코어의 수로 결정되는 병렬 처리 수준  
  
-   다시 실행해야 할 로그의 활성 부분에 있는 로그 레코드의 양입니다.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 액세스에 최적화된 개체의 저장소 만들기 및 관리](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
