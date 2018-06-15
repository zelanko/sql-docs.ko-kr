---
title: 인덱스 작업에 필요한 트랜잭션 로그 디스크 공간 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- index disk space [SQL Server]
- space [SQL Server], indexes
- transaction logs [SQL Server], disk space
- disk space [SQL Server], transaction logs
- space [SQL Server], transaction logs
ms.assetid: 4f8a4922-4507-4072-be67-c690528d5c3b
caps.latest.revision: 17
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4e3c0e02d5c25c62775af001068ee3e92b63f224
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32937428"
---
# <a name="transaction-log-disk-space-for-index-operations"></a>인덱스 작업에 필요한 트랜잭션 로그 디스크 공간
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  대량 인덱스 작업은 트랜잭션 로그를 빠르게 채울 수 있는 대량의 데이터 로드를 생성할 수 있습니다. 트랜잭션 로그는 인덱스 작업의 롤백을 보장하기 위해 인덱스 작업이 완료된 이후에만 잘릴 수 있지만 트랜잭션 로그 백업은 인덱스 작업 중에도 수행할 수 있습니다. 따라서 인덱스 작업 중에는 인덱스 작업 트랜잭션 및 모든 동시 사용자 트랜잭션을 모두 저장할 수 있는 충분한 트랜잭션 로그 공간이 필요합니다. 이것은 오프라인 인덱스 작업과 온라인 인덱스 작업 모두에 해당합니다. 오프라인 인덱스 작업 중에는 기본 테이블에 액세스할 수 없기 때문에 사용자 트랜잭션이 거의 없고 로그가 빠르게 증가하지 않을 수 있습니다. 온라인 인덱스 작업에서는 동시 사용자 작업이 제한되지 않습니다. 따라서 대량의 온라인 인덱스 작업과 대량의 동시 사용자 트랜잭션이 결합하는 경우에는 자를 수 없을 만큼 지속적으로 트랜잭션 로그가 증가할 수 있습니다.  
  
## <a name="recommendations"></a>권장 사항  
 대량 인덱스 작업을 실행할 때는 다음 권장 사항을 고려하십시오.  
  
1.  온라인으로 대량 인덱스 작업을 실행하기 전에 트랜잭션 로그를 백업하고 잘랐는지 확인하고 예상되는 인덱스 및 사용자 트랜잭션을 저장할 트랜잭션 로그 공간이 충분한지 확인합니다.  
  
2.  인덱스 작업을 위해 SORT_IN_TEMPDB 옵션을 ON으로 설정할 것을 고려해 봅니다. 이렇게 하면 인덱스 트랜잭션이 동시 사용자 트랜잭션과 구분됩니다. 인덱스 트랜잭션은 **tempdb** 트랜잭션 로그에 저장되고 동시 사용자 트랜잭션은 사용자 데이터베이스의 트랜잭션 로그에 저장됩니다. 따라서 필요한 경우 인덱스 작업 중에 사용자 데이터베이스의 트랜잭션 로그를 자를 수 있습니다. 또한 **tempdb** 로그가 사용자 데이터베이스 로그와 동일한 디스크에 배치되지 않은 경우에는 두 로그가 동일한 디스크 공간을 차지하려고 경쟁하지 않습니다.  
  
    > [!NOTE]  
    >  **tempdb** 데이터베이스 및 트랜잭션 로그에 인덱스 작업을 처리할 충분한 디스크 공간이 있는지 확인합니다. **tempdb** 트랜잭션 로그는 인덱스 작업이 완료된 이후에만 자를 수 있습니다.  
  
3.  인덱스 작업의 최소 로깅을 허용하는 데이터베이스 복구 모델을 사용합니다. 이렇게 하면 로그 크기가 줄어들고 로그 공간이 로그로 채워지지 않을 수 있습니다.  
  
4.  온라인 인덱스 작업은 명시적 트랜잭션으로 실행하면 안 됩니다. 로그는 명시적 트랜잭션이 종료된 이후에만 잘립니다.  
  
## <a name="related-content"></a>관련 내용  
 [인덱스 DDL 작업의 디스크 공간 요구 사항](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [인덱스 디스크 공간 예](../../relational-databases/indexes/index-disk-space-example.md)  
  
  
