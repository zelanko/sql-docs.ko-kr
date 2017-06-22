---
title: "복제된 데이터의 유효성 검사 | Microsoft 문서"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- inline data validation [SQL Server replication]
- administering replication, validating data
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication]
- merge replication data validation [SQL Server replication], about data validation
- validating replicated data
ms.assetid: f7500a2b-61cb-41b5-816d-27609a6c58e7
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a57d074a1e24ec0d865c2a1be5c6a857ecb68354
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="validate-replicated-data"></a>복제된 데이터의 유효성 검사
  트랜잭션 및 병합 복제를 사용하면 구독자의 데이터가 게시자의 데이터와 일치하는지 확인할 수 있습니다. 게시에 대한 특정 구독 또는 모든 구독에 대해 유효성 검사를 수행할 수 있습니다. 다음 유효성 검사 유형 중 하나를 지정합니다. 배포 에이전트 또는 병합 에이전트가 다음에 실행될 때 해당 유형에 따라 데이터의 유효성을 검사합니다.  
  
-   행 개수만. 이 유형은 구독자에 있는 테이블의 행 개수가 게시자에 있는 테이블의 행 개수와 동일한지 여부의 유효성만 검사하고 행 내용 일치 여부의 유효성은 검사하지 않습니다. 행 개수 유효성 검사에서는 최소 수준의 데이터 문제 인식을 위한 검사만 수행됩니다.  
  
-   행 개수와 이진 체크섬. 게시자 및 구독자에서 행 개수의 유효성을 검사할 뿐만 아니라 체크섬 알고리즘을 사용하여 모든 데이터의 체크섬을 계산합니다. 행 개수 확인을 실패하면 체크섬 계산이 수행되지 않습니다.  
  
 구독자의 데이터와 게시자의 데이터가 일치하는지에 대한 유효성 검사 외에도 병합 복제는 각 구독자에 대해 데이터가 올바르게 분할되었는지에 대한 유효성을 검사하는 기능을 제공합니다. 자세한 내용은 [병합 구독자의 파티션 정보 유효성 검사](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md)를 참조하세요.  
  
 **데이터의 유효성을 검사하려면**  
  
 구독에 있는 모든 아티클의 유효성을 검사하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 저장 프로시저 또는 RMO(복제 관리 개체)를 사용합니다. 자세한 내용은 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)를 참조하세요. 스냅숏 게시와 트랜잭션 게시에 있는 개별 아티클의 유효성을 검사하려면 저장 프로시저를 사용해야 합니다.  
  
## <a name="data-validation-results"></a>데이터 유효성 검사 결과  
 유효성 검사가 완료되면 배포 에이전트 또는 병합 에이전트는 성공 여부에 대한 메시지를 기록합니다. 복제는 유효성이 확인되지 못한 행은 보고하지 않습니다. 이러한 메시지는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 복제 모니터 및 복제 시스템 테이블에서 볼 수 있습니다. 위에 나열된 방법 항목에서 유효성 검사를 실행하고 결과를 확인하는 방법을 설명합니다.  
  
 유효성 검사 실패를 처리하려면 다음 사항을 살펴보십시오.  
  
-   **복제: 구독자가 데이터 유효성 검사에 실패했습니다** 라는 복제 경고를 구성하여 검사 실패에 대한 알림을 받도록 합니다. 자세한 내용은 [미리 정의된 복제 경고 구성&#40;SQL Server Management Studio&#41;](../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)을 참조하세요.  
  
-   유효성 검사 실패가 응용 프로그램에 문제가 됩니까? 유효성 검사 실패가 문제가 되는 경우 수동으로 데이터를 업데이트하여 동기화하거나 구독을 다시 초기화합니다.  
  
    -   [tablediff 유틸리티](../../tools/tablediff-utility.md)를 사용하여 데이터를 업데이트할 수 있습니다. 이 유틸리티를 사용하는 방법은 [복제된 테이블의 차이점 비교&#40;복제 프로그래밍&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)를 참조하세요.  
  
    -   다시 초기화에 대한 자세한 내용은 [구독 다시 초기화](../../relational-databases/replication/reinitialize-subscriptions.md)를 참조하세요.  
  
## <a name="considerations-for-data-validation"></a>데이터 유효성 검사에 대한 고려 사항  
 데이터 유효성을 검사할 때 다음 사항을 고려하십시오.  
  
-   데이터 유효성을 검사하기 전에 구독자에서 모든 업데이트 작업을 중지해야 합니다. 유효성 검사가 수행 중일 때는 게시자에서 작업을 중지할 필요가 없습니다.  
  
-   큰 데이터 집합의 유효성을 검사할 때는 체크섬 및 이진 체크섬이 프로세서 리소스를 많이 요구할 수 있으므로 복제에 사용되는 서버에서 진행 중인 작업 수가 가장 적은 경우 유효성 검사가 수행되도록 예약해야 합니다.  
  
-   복제는 테이블의 유효성만 검사하고 게시자의 스키마 전용 아티클(예: 저장 프로시저)이 구독자의 스키마 전용 아티클과 동일한지 여부의 유효성은 검사하지 않습니다.  
  
-   게시된 테이블에는 이진 체크섬을 사용할 수 있습니다. 체크섬은 열 필터가 있는 테이블 또는 열을 삭제 또는 추가하는 ALTER TABLE 문으로 인해 열 오프셋이 다른 논리적 테이블 구조의 유효성을 검사할 수 없습니다.  
  
-   복제 유효성 검사에서는 **checksum** 및 **binary_checksum** 함수를 사용합니다. 해당 동작에 대한 자세한 내용은 [CHECKSUM&#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md) 및 [BINARY_CHECKSUM&#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md)을 참조하세요.  
  
-   구독자에서의 데이터 형식과 게시자에서의 데이터 형식이 다른 경우 이진 체크섬 또는 체크섬 유효성 검사가 올바르지 않을 수 있습니다. 이 문제는 다음 중 하나를 수행할 경우 발생할 수 있습니다.  
  
    -   이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 데이터 형식을 매핑하도록 스키마 옵션을 명시적으로 설정한 경우.  
  
    -   병합 게시의 게시 호환성 수준을 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 설정했으며 게시된 테이블에 이 버전에 대해 매핑해야 하는 데이터 형식이 하나 이상 들어 있는 경우.  
  
    -   구독을 수동으로 초기화하고 구독자에서 다른 데이터 형식을 사용하는 경우  
  
-   트랜잭션 복제의 변환 가능한 구독에서는 이진 체크섬 및 체크섬 유효성 검사가 지원되지 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자로 복제된 데이터에 대해서는 유효성 검사가 지원되지 않습니다.  
  
## <a name="how-data-validation-works"></a>데이터 유효성 검사 작업 방식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 게시자에서 행 개수 또는 체크섬을 계산한 다음 그 값을 구독자에서 계산된 행 개수 또는 체크섬과 비교하여 데이터의 유효성을 검사합니다. 전체 게시 테이블과 전체 구독 테이블에 대해 각각 하나의 값이 계산되지만 **text**, **ntext**또는 **image** 열의 데이터는 계산에 포함되지 않습니다.  
  
 계산이 수행되는 동안 행 개수 또는 체크섬이 실행될 테이블에 공유 잠금이 임시로 지정되지만 대부분 몇 초 내에 계산이 신속히 완료되고 공유 잠금이 제거됩니다.  
  
 이진 체크섬을 사용할 때는 데이터 페이지의 실제 행에 대한 CRC 대신 열 단위의 32비트 중복 검사(CRC)가 수행됩니다. 따라서 테이블의 열이 데이터 페이지에서 실제로 임의의 순서로 배열될 수 있지만, 해당 행에 대해 동일한 CRC로 계산됩니다. 이진 체크섬 유효성 검사는 게시에 행 또는 열 필터가 있을 때 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Best Practices for Replication Administration](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
