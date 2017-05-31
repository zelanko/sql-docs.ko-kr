---
title: "메모리 액세스에 최적화된 개체에 대한 내구성 정의 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0fe85fbf-8e8d-4983-96fd-d04b3c7d6d65
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d4f8bab5cfa0cc83737bb5736dfe4dcac84b8c13
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="defining-durability-for-memory-optimized-objects"></a>메모리 액세스에 최적화된 개체에 대한 내구성 정의
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  메모리 액세스에 최적화된 테이블에는 두 가지 내구성 옵션이 있습니다.  
  
 SCHEMA_AND_DATA(기본값)  
 이 옵션은 스키마와 데이터 모두에 대한 내구성을 제공합니다. 데이터 내구성 수준은 트랜잭션을 완전 내구성으로 커밋할지 아니면 지연된 내구성으로 커밋할지에 따라 달라집니다. 완전한 내구성이 있는 트랜잭션은 디스크 기반 테이블과 유사하게 스키마 및 데이터에 대한 동일한 내구성 보증을 제공합니다. 지연된 내구성은 성능을 향상시키지만 서버 충돌이나 장애 조치(Failover)의 경우 데이터 손실을 발생시킬 수도 있습니다. 지연된 내구성에 자세한 내용은 [트랜잭션 내구성 제어](../../relational-databases/logs/control-transaction-durability.md)를 참조하세요.  
  
 SCHEMA_ONLY  
 이 옵션은 테이블 스키마의 내구성을 보장합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작하거나 Azure SQL 데이터베이스에서 다시 구성하는 경우 테이블 스키마는 지속되지만 테이블의 데이터가 손실됩니다. (이것은 다시 시작하면 테이블과 데이터가 손실되는 tempdb의 테이블과는 다릅니다.) 내구성이 없는 테이블을 만드는 일반적인 시나리오는 ETL 프로세스를 위한 준비 테이블 같은 임시 테이블을 저장하는 것입니다. SCHEMA_ONLY 내구성은 트랜잭션 로깅과 검사점을 방지하여 I/O 작업을 크게 줄일 수 있습니다.  
  
 기본 SCHEMA_AND_DATA 테이블을 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 디스크 기반 테이블과 동일한 내구성 보증을 제공합니다.  
  
 트랜잭션 내구성  
 메모리 액세스에 최적화된 테이블에 DDL 또는 DML 변경을 적용한 완전한 내구성이 있는 트랜잭션을 커밋하면 메모리 액세스에 최적화된 내구성이 있는 테이블에 적용한 이 변경은 영구적이 됩니다.  
  
 지연된 내구성이 있는 트랜잭션을 메모리 액세스에 최적화된 테이블로 커밋하면 메모리 내 트랜잭션 로그가 디스크에 저장된 이후에만 트랜잭션이 트랜잭션이 내구성을 갖습니다. 지연된 내구성에 자세한 내용은 [트랜잭션 내구성 제어](../../relational-databases/logs/control-transaction-durability.md)를 참조하세요.  
  
 다시 시작 내구성  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 충돌이나 계획된 종료 후에 다시 시작되면 메모리 액세스에 최적화된 내구성이 있는 테이블이 다시 인스턴스화되어 종료나 충돌 전의 상태로 복원됩니다.  
  
 미디어 오류 내구성  
 실패했거나 손상된 디스크에 메모리 액세스에 최적화된 내구성이 있는 개체의 영구 복사본이 하나 이상 포함되어 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 및 복원 기능은 메모리 액세스에 최적화된 테이블을 새 미디어에 복원합니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화된 개체의 저장소 만들기 및 관리](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
