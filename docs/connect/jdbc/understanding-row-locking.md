---
title: 행 잠금 이해 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 63c76a2f-f2b9-461f-8904-acbda0169ac3
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 888a877cfa0406c02667a968be0ad3e31ad8d403
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="understanding-row-locking"></a>행 잠금에 대한 개요
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 행 잠금을 사용합니다. 행 잠금은 데이터베이스에서 동시에 수정 작업을 수행하는 여러 사용자 사이의 동시성 제어를 구현합니다.  기본적으로 트랜잭션 및 잠금은 각 연결마다 관리됩니다. 예를 들어 응용 프로그램이 두 개의 JDBC 연결을 열 경우 한 연결에서 설정한 잠금은 다른 연결에서 공유할 수 없습니다. 연결은 다른 연결에서 보유한 잠금과 충돌하는 잠금을 설정할 수 없습니다.  
  
> [!NOTE]  
>  행 잠금이 사용되면 인출 버퍼의 모든 행에 잠금이 수행되므로 인출 크기에 매우 큰 값을 설정하면 동시성에 영향을 줄 수 있습니다.  
  
 잠금은 트랜잭션 무결성 및 데이터베이스 동시성을 보장하는 데 사용됩니다. 잠금은 다른 사용자가 변경하고 있는 데이터를 렌더링할 수 없도록 하고 여러 사용자가 동일한 데이터를 동시에 변경하지 못하도록 합니다. 잠금 기능을 사용하지 않으면 데이터베이스 내의 데이터가 논리적으로 올바르지 않게 되고, 해당 데이터에 대해 실행한 쿼리에서 예상치 못한 결과가 발생할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에서 행 잠금에 대한 자세한 내용은 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 온라인 설명서의 "[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에서의 잠금"을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버로 결과 집합 관리](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
