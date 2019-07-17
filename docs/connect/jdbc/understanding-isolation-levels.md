---
title: 격리 수준 이해 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2c41e23a-da6c-4650-b5fc-b5fe53ba65c3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 432da51055d0a9f250c342338770103fbe8fe4b0
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800172"
---
# <a name="understanding-isolation-levels"></a>격리 수준 이해

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

한 트랜잭션을 리소스 또는 다른 트랜잭션에서 수정한 데이터 내용으로부터 격리하는 정도를 정의하는 격리 수준을 트랜잭션에 지정할 수 있습니다. 격리 수준은 허용되는 동시성 부작용(예: 커밋되지 않은 읽기 또는 가상 읽기)의 관점에서 설명됩니다.  
  
트랜잭션 격리 수준으로 다음 사항을 제어할 수 있습니다.  
  
- 데이터를 읽을 때 잠금을 확보할지 여부 및 요청되는 잠금의 종류  
  
- 읽기 잠금의 보유 기간  
  
- 읽기 작업이 다른 트랜잭션에서 수정한 행을 참조할 경우 선택할 수 있는 다음과 같은 옵션  
  
  - 행에 대한 배타적 잠금이 해제될 때까지 차단  
  
  - 문 또는 트랜잭션 시작 당시의 커밋된 행 버전 검색  
  
  - 커밋되지 않은 데이터 수정 내용 읽기  

트랜잭션 격리 수준을 선택해도 데이터 수정 내용을 보호하기 위해 획득된 잠금에는 영향을 주지 않습니다. 설정된 격리 수준에 관계없이 트랜잭션은 항상 수정하는 데이터에 대해 배타적 잠금을 얻고 해당 트랜잭션이 완료될 때까지 이 잠금을 보유합니다. 읽기 작업의 경우 트랜잭션 격리 수준은 대개 다른 트랜잭션에서 수정한 내용의 영향을 받지 않도록 보호 수준을 정의합니다.  
  
격리 수준이 낮을수록 데이터에 동시에 액세스할 수 있는 사용자가 많아지지만 동시성 부작용(예: 커밋되지 않은 읽기 또는 업데이트 손실) 횟수도 늘어납니다. 반대로 격리 수준이 높을수록 동시성 부작용 종류가 줄어들지만 시스템 리소스가 더 많이 필요하게 되고 한 트랜잭션이 다른 트랜잭션을 차단하게 될 확률도 높아집니다. 적절한 격리 수준을 선택하려면 응용 프로그램의 데이터 무결성 요구 사항과 각 격리 수준에 의해 야기되는 오버헤드를 신중하게 평가해야 합니다. 최상위 격리 수준인 직렬화 가능의 경우 트랜잭션이 읽기 작업을 반복할 때마다 정확히 동일한 데이터를 검색하지만 다중 사용자 시스템에서 다른 사용자에게 영향을 줄 수 있는 수준의 잠금을 수행함으로써 이를 달성합니다. 최하위 격리 수준인 커밋되지 않은 읽기의 경우 다른 트랜잭션에서 수정했지만 커밋되지 않은 데이터를 검색할 수 있습니다. 커밋되지 않은 읽기에서는 모든 동시성 부작용이 발생할 수 있지만 읽기 잠금이나 버전 관리가 수행되지 않으므로 오버헤드가 최소화됩니다.  

## <a name="remarks"></a>Remarks

 다음 표에서는 각 격리 수준에서 허용되는 동시성 부작용을 보여 줍니다.  
  
| 격리 수준  | 커밋되지 않은 읽기 | 반복하지 않는 읽기 | 가상 |
| ---------------- | ---------- | ------------------- | ------- |
| 커밋되지 않은 읽기 | 예        | 예                 | 예     |
| 커밋된 읽기   | 아니오         | 예                 | 예     |
| 반복 읽기  | 아니오         | 아니오                  | 예     |
| 스냅샷         | 아니오         | 아니오                  | 아니오      |
| 직렬화 가능     | 아니오         | 아니오                  | 아니오      |
  
두 트랜잭션이 각기 동일한 행을 검색할 때 발생할 수 있는 업데이트 손실을 방지하려면 반복 읽기 이상의 격리 수준에서 트랜잭션을 실행해야 합니다. 그런 다음 원래 검색된 값에 따라 행을 업데이트하십시오. 두 트랜잭션이 한 개의 UPDATE 문을 사용하여 행을 업데이트하더라도 업데이트가 이전에 검색된 값에 따라 수행되지 않을 경우 기본 격리 수준인 커밋된 읽기에서는 업데이트 손실이 발생하지 않습니다.  

트랜잭션 격리 수준을 설정하는 데 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [setTransactionIsolation](../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md) 메서드를 사용할 수 있습니다. 이 메서드는 다음과 같은 연결 상수 중 하나를 기반으로 하는 **int** 값을 인수로 사용합니다.  

```java
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED);  
```

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새 스냅숏 격리 수준을 사용하려면 다음과 같은 `SQLServerConnection` 상수 중 하나를 사용할 수 있습니다.  

```java
con.setTransactionIsolation(SQLServerConnection.TRANSACTION_SNAPSHOT);  
```

또는 다음을 사용하십시오.  

```java
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED + 4094);  
```

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 격리 수준에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "[!INCLUDE[ssDE](../../includes/ssde_md.md)]의 격리 수준"을 참조하세요.  

## <a name="see-also"></a>참고 항목

[JDBC 드라이버로 트랜잭션 수행](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
