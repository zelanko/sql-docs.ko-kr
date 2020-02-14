---
title: 메모리 액세스에 최적화된 테이블 스토리지 구성 | Microsoft 문서
ms.custom: ''
ms.date: 1/15/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d1d0848a1399c533162799fd9a4404955bb542dd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76125009"
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블 스토리지 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  스토리지 용량 및 IOPS(초당 입력/출력 작업)를 구성해야 합니다.  
  
## <a name="storage-capacity"></a>스토리지 용량  

데이터베이스의 메모리 최적화 내구성 있는 테이블의 메모리 내 크기를 측정하려면 [메모리 최적화 테이블에 필요한 메모리 예측](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) 의 정보를 사용합니다. 인덱스가 메모리 최적화 테이블에 유지되지 않으므로 인덱스 크기를 포함하지 마세요. 
 
크기를 확인한 후에는 새로 변경된 데이터를 저장하는 데 사용되는 검사점 파일을 충분히 저장할 수 있는 디스크 공간을 제공해야 합니다. 저장된 데이터는 메모리 내 테이블에 추가되는 새 행의 콘텐츠뿐만 아니라 기존 행의 새 버전에도 포함합니다. 이 스토리지는 행이 삽입되거나 업데이트될 때 증가합니다. 로그 잘림이 발생하면 행 버전이 병합되고 스토리지가 회수됩니다. 어떤 이유로든 로그 잘림이 지연되면 메모리 내 OLTP 저장소가 늘어납니다.

이 영역에 대한 스토리지 크기를 조정하는 좋은 시작점은 내구성이 있는 메모리 내 테이블 크기의 4배를 예약하는 것입니다. 공간 사용량을 모니터링하고 필요한 경우 사용 가능한 스토리지를 확장할 수 있도록 준비합니다.
  
## <a name="storage-iops"></a>스토리지 IOPS  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 는 작업 처리량을 크게 증가시킬 수 있습니다. 따라서 IO가 병목 상태가 아니어야 합니다.  
  
-   디스크 기반 테이블을 메모리 최적화 테이블에 마이그레이션하는 경우 트랜잭션 로그가 증가된 트랜잭션 로그 작업을 지원할 수 있는 스토리지 미디어에 있어야 합니다. 예를 들어 스토리지 미디어가 100MB/초로 트랜잭션 로그 작업을 지원하고 메모리 최적화 테이블이 5배 뛰어난 성능을 발휘하는 경우 트랜잭션 로그의 스토리지 미디어는 트랜잭션 로그 작업에 성능 병목 상태가 발생하지 않도록 5배의 성능 향상을 지원할 수 있어야 합니다.  
  
-   메모리 최적화 테이블은 하나 이상의 컨테이너 간에 분산된 검사점 파일에서 유지됩니다. 각각의 컨테이너는 일반적으로 자체 스토리지 디바이스에 매핑되고 증가된 스토리지 용량 및 향상된 IOPS를 위해 모두 사용됩니다. 스토리지 미디어의 순차 IOPS는 최대 3배 유지 가능한 트랜잭션 로그 처리량을 지원할 수 있어야 합니다. 검사점 파일에 쓰기는 데이터 파일의 경우 256KB이고 델타 파일의 경우 4KB입니다.
  
     - 예를 들어 메모리 최적화 테이블이 트랜잭션 로그에서 유지 가능한 500MB/초의 작업을 생성하는 경우 메모리 최적화 테이블의 스토리지는 1.5GB/초 IOPS를 지원해야 합니다. 유지 가능한 트랜잭션 로그 처리량 3배 지원 요구는 데이터 및 델타 파일 쌍을 초기 데이터에 먼저 쓴 다음 병합 작업의 일부로 읽거나 다시 써야 하는 과정에서 발생합니다.  
  
- 스토리지에 대한 IOPS를 측정하는 다른 요소는 메모리 최적화 테이블의 복구 시간입니다. 애플리케이션에서 데이터베이스를 사용할 수 있으려면 먼저 내구성이 있는 테이블의 데이터를 메모리에서 읽어야 합니다. 일반적으로 메모리 최적화 테이블로 데이터 로드는 IOPS의 속도로 수행할 수 있습니다. 메모리 최적화 내구성 있는 테이블의 전체 스토리지가 60GB이고 이 데이터를 1분 내에 로드할 수 있으려면 스토리지의 IOPS를 1GB/초로 설정해야 합니다.  
  
-   일반적으로 검사점 파일은 공간이 허용된다면 모든 컨테이너 간에 균일하게 분산됩니다. SQL Server 2014를 사용하면 균일한 분산을 달성하기 위해 홀수의 컨테이너를 프로비전해야 합니다. 2016부터는 홀수 및 짝수 컨테이너 모두 균일하게 분산됩니다.
  
## <a name="encryption"></a>암호화  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 이상 버전에서는 메모리 최적화 테이블의 스토리지가 데이터베이스에서 TDE(투명한 데이터 암호화)를 사용하도록 설정하는 과정에서 미사용 시 암호화됩니다. 자세한 내용은 [투명한 데이터 암호화](../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하세요. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 검사점 파일은 데이터베이스에서 TDE가 사용하도록 설정된 경우에도 암호화되지 않습니다.

 [비지속형](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md)(SCHEMA_ONLY) 메모리 최적화 테이블의 데이터는 항상 디스크에 기록되지 않습니다. 따라서 해당 테이블에는 TDE가 적용되지 않습니다.
  
## <a name="see-also"></a>참고 항목  
 [메모리 최적화 개체에 대한 스토리지 만들기 및 관리](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
