---
title: JDBC 드라이버로 트랜잭션 수행 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: afbb776f-05dc-4e79-bb25-2c340483e401
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 58c6282a11e3fcc0ca896a2e3e4075a4b51d928e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027848"
---
# <a name="performing-transactions-with-the-jdbc-driver"></a>JDBC 드라이버로 트랜잭션 수행
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  트랜잭션 처리는 영구 데이터의 일관성을 보장해야 하는 모든 애플리케이션의 필수 요구 사항입니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서는 트랜잭션 처리를 로컬로 수행하거나 분산 수행합니다. 트랜잭션은 ACID(원자성, 일관성, 격리성 및 내구성)를 갖춘 실행 모듈입니다.  
  
 이 섹션의 항목에서는 격리 수준, 트랜잭션 저장점 및 결과 집합 유지 기능을 비롯하여 JDBC 드라이버가 트랜잭션을 지원하는 방법에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[트랜잭션 이해](../../connect/jdbc/understanding-transactions.md)|JDBC 드라이버에서 트랜잭션을 사용하는 방법의 개요를 제공합니다.|  
|[XA 트랜잭션 이해](../../connect/jdbc/understanding-xa-transactions.md)|JDBC 드라이버에서 XA 트랜잭션을 사용하는 방법의 개요를 제공합니다.|  
|[격리 수준 이해](../../connect/jdbc/understanding-isolation-levels.md)|JDBC 드라이버가 지원하는 다양한 격리 수준을 설명합니다.|  
|[저장점 사용](../../connect/jdbc/using-savepoints.md)|JDBC 드라이버를 트랜잭션 저장점과 함께 사용하는 방법을 설명합니다.|  
|[유지 기능 사용](../../connect/jdbc/using-holdability.md)|JDBC 드라이버를 결과 집합 유지 기능과 함께 사용하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
