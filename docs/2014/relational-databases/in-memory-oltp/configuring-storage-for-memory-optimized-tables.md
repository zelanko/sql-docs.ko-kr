---
title: 메모리 액세스에 최적화된 테이블 스토리지 구성 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 93698be4738ef2a28c79581d0957f695b036c911
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62990635"
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블 스토리지 구성
  스토리지 용량 및 IOPS(초당 입력/출력 작업)를 구성해야 합니다.  
  
## <a name="storage-capacity"></a>스토리지 용량  
 데이터베이스의 메모리 최적화 내구성 있는 테이블의 메모리 내 크기를 측정하려면 [메모리 최적화 테이블에 필요한 메모리 예측](memory-optimized-tables.md) 의 정보를 사용합니다. 인덱스가 메모리 최적화 테이블에 유지되지 않으므로 인덱스 크기를 포함하지 마세요. 크기를 결정했으면 내구성이 있는 메모리 내 테이블 크기의 4배에 해당하는 디스크 공간을 제공해야 합니다.  
  
## <a name="storage-performance"></a>스토리지 성능  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 는 작업 처리량을 크게 증가시킬 수 있습니다. 따라서 IO가 병목 상태가 아니어야 합니다.  
  
-   디스크 기반 테이블을 메모리 최적화 테이블에 마이그레이션하는 경우 트랜잭션 로그가 증가된 트랜잭션 로그 작업을 지원할 수 있는 스토리지 미디어에 있어야 합니다. 예를 들어 스토리지 미디어가 100MB/초로 트랜잭션 로그 작업을 지원하고 메모리 최적화 테이블이 5배 뛰어난 성능을 발휘하는 경우 트랜잭션 로그의 스토리지 미디어는 트랜잭션 로그 작업에 성능 병목 상태가 발생하지 않도록 5배의 성능 향상을 지원할 수 있어야 합니다.  
  
-   메모리 액세스에 최적화된 테이블은 하나 이상의 컨테이너 간에 분산된 파일에서 유지됩니다. 각각의 컨테이너는 일반적으로 자체 스핀들에 매핑되고 증가된 스토리지 용량 및 향상된 성능을 위해 모두 사용됩니다. 저장소 미디어의 순차 IOPS는 3을 지원할 수 있는지 확인 해야 합니다. 트랜잭션 로그 처리량에서 시간이 길어집니다.  
  
     예를 들어, 트랜잭션 로그에서 활동의 초당 500MB를 생성 하는 메모리 최적화 테이블, 메모리 최적화 테이블의 저장소 1.5 g B/초를 지원 해야 합니다. 3 배 지원 요구 트랜잭션 로그 처리량에서 증가 써야 과정은 데이터 및 델타 파일 쌍을 초기 데이터에 먼저 쓴 다음 하 읽기/다시에서 병합 작업의 일환으로 합니다.  
  
     스토리지 처리량을 측정하는 다른 요소는 메모리 최적화 테이블의 복구 시간입니다. 애플리케이션에서 데이터베이스를 사용할 수 있으려면 먼저 내구성이 있는 테이블의 데이터를 메모리에서 읽어야 합니다. 일반적으로 메모리 최적화 테이블로 데이터 로드는 IOPS의 속도로 수행할 수 있습니다. 메모리 최적화 내구성 있는 테이블의 전체 스토리지가 60GB이고 이 데이터를 1분 내에 로드할 수 있으려면 스토리지의 IOPS를 1GB/초로 설정해야 합니다.  
  
-   짝수 개의 스핀들이 있는 경우 컨테이너 개수의 두 배를 만들어야 하고 각 쌍은 같은 스핀들에 매핑되어야 합니다. 이는 IOPS 및 스토리지를 전파하는 데 필요합니다. 자세한 내용은 [메모리 최적화 파일 그룹이](the-memory-optimized-filegroup.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 액세스에 최적화된 개체의 저장소 만들기 및 관리](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
