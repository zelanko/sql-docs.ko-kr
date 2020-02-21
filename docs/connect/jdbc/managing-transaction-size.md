---
title: 트랜잭션 크기 관리 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 82900342-bc80-445f-98a4-468a303aae1e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3b443e3541dbf86fd0cfa947f057faaf62e08226
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027905"
---
# <a name="managing-transaction-size"></a>트랜잭션 크기 관리
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  트랜잭션을 사용할 때 트랜잭션은 되도록 간단하게 유지하는 것이 중요합니다. 자동 커밋의 기본 모드는 [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md) 메서드를 사용하여 설정하거나 해제할 수 있는데 이 기본 모드에서는 모든 동작이 자동으로 커밋되므로, 개발자들이 작업하기에 가장 쉬운 모드입니다.  
  
 수동 트랜잭션을 사용할 경우 코드가 트랜잭션을 가능한 한 빨리 커밋하도록 하십시오. 트랜잭션이 열려 있으면 다른 사용자가 해당 데이터에 액세스할 수 없도록 차단됩니다. 예를 들어 catch 블록에 롤백 호출을 삽입하고 finally 블록에 커밋 호출을 삽입하는 것이 바람직한 프로그래밍 방식입니다. 그러나 바람직한 프로그래밍 방식은 애플리케이션의 디자인에 따라 다릅니다.  
  
 트랜잭션의 크기를 작게 유지하면 동시성이 향상됩니다. 예를 들어 수동 트랜잭션을 시작하여 20,000개 행 테이블에서 10,000개의 행을 수정한다면 단순히 데이터를 읽고 있는 경우에도 테이블의 절반이 완전히 차단되어 다른 모든 사용자가 사용할 수 없게 됩니다. 이 경우 수정을 2,000개 행으로 줄이면 테이블의 90%가 사용 가능해집니다.  
  
 또한 애플리케이션에서 차단 문제가 발생할 가능성이 있어 제한 시간을 설정해야 하는 경우 잠금 제한 시간 설정을 사용하십시오. [setLockTimeout](../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md) 메서드를 사용하면 됩니다. 잠금 제한 시간의 기본값은 -1이며 이는 잠금을 기다리는 동안 무제한으로 차단됨을 의미합니다. 잠금 제한 시간을 30초로 설정하면 다른 연결에 의해 연결이 차단된 경우 차단된 연결이 30초 내에 해제됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버로 성능 및 안정성 개선](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
