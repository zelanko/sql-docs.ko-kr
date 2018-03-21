---
title: "메모리 액세스에 최적화된 테이블 저장소 구성 | Microsoft 문서"
ms.custom: 
ms.date: 10/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e787ac4b1106857a2571dd56c0d352495e8056b
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블 저장소 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  저장소 용량 및 IOPS(초당 입력/출력 작업)를 구성해야 합니다.  
  
## <a name="storage-capacity"></a>저장소 용량  
 데이터베이스의 메모리 최적화 내구성 있는 테이블의 메모리 내 크기를 측정하려면 [메모리 최적화 테이블에 필요한 메모리 예측](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) 의 정보를 사용합니다. 인덱스가 메모리 최적화 테이블에 유지되지 않으므로 인덱스 크기를 포함하지 마세요. 크기를 결정했으면 내구성이 있는 메모리 내 테이블 크기의 4배에 해당하는 디스크 공간을 제공해야 합니다.  
  
## <a name="storage-iops"></a>저장소 IOPS  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 는 작업 처리량을 크게 증가시킬 수 있습니다. 따라서 IO가 병목 상태가 아니어야 합니다.  
  
-   디스크 기반 테이블을 메모리 최적화 테이블에 마이그레이션하는 경우 트랜잭션 로그가 증가된 트랜잭션 로그 작업을 지원할 수 있는 저장소 미디어에 있어야 합니다. 예를 들어 저장소 미디어가 100MB/초로 트랜잭션 로그 작업을 지원하고 메모리 최적화 테이블이 5배 뛰어난 성능을 발휘하는 경우 트랜잭션 로그의 저장소 미디어는 트랜잭션 로그 작업에 성능 병목 상태가 발생하지 않도록 5배의 성능 향상을 지원할 수 있어야 합니다.  
  
-   메모리 최적화 테이블은 하나 이상의 컨테이너 간에 분산된 검사점 파일에서 유지됩니다. 각각의 컨테이너는 일반적으로 자체 저장소 장치에 매핑되고 증가된 저장소 용량 및 향상된 IOPS를 위해 모두 사용됩니다. 저장소 미디어의 순차 IOPS는 최대 3배 유지 가능한 트랜잭션 로그 처리량을 지원할 수 있어야 합니다. 검사점 파일에 쓰기는 데이터 파일의 경우 256KB이고 델타 파일의 경우 4KB입니다.
  
     - 예를 들어 메모리 최적화 테이블이 트랜잭션 로그에서 유지 가능한 500MB/초의 작업을 생성하는 경우 메모리 최적화 테이블의 저장소는 1.5GB/초 IOPS를 지원해야 합니다. 유지 가능한 트랜잭션 로그 처리량 3배 지원 요구는 데이터 및 델타 파일 쌍을 초기 데이터에 먼저 쓴 다음 병합 작업의 일부로 읽거나 다시 써야 하는 과정에서 발생합니다.  
  
- 저장소에 대한 IOPS를 측정하는 다른 요소는 메모리 최적화 테이블의 복구 시간입니다. 응용 프로그램에서 데이터베이스를 사용할 수 있으려면 먼저 내구성이 있는 테이블의 데이터를 메모리에서 읽어야 합니다. 일반적으로 메모리 최적화 테이블로 데이터 로드는 IOPS의 속도로 수행할 수 있습니다. 메모리 최적화 내구성 있는 테이블의 전체 저장소가 60GB이고 이 데이터를 1분 내에 로드할 수 있으려면 저장소의 IOPS를 1GB/초로 설정해야 합니다.  
  
-   일반적으로 검사점 파일은 공간이 허용된다면 모든 컨테이너 간에 균일하게 분산됩니다. SQL Server 2014를 사용하면 균일한 분산을 달성하기 위해 홀수의 컨테이너를 프로비전해야 합니다. 2016부터는 홀수 및 짝수 컨테이너 모두 균일하게 분산됩니다.
  
## <a name="encryption"></a>암호화  
 
            [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 데이터베이스에 TDE를 사용하는 일부로 메모리 최적화 테이블에 대한 저장소를 암호화합니다. 자세한 내용은 [TDE&#40;투명한 데이터 암호화&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하세요. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 검사점 파일은 데이터베이스에서 TDE가 사용하도록 설정된 경우에도 암호화되지 않습니다.
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화된 개체의 저장소 만들기 및 관리](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
