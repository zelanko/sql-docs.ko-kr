---
title: 드라이버 버전 가져오기 | Microsoft Docs
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
ms.topic: conceptual
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d3828c04f418a31e2dacddb97472ec3b2f776a5e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getting-the-driver-version"></a>드라이버 버전 가져오기
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  설치 된 버전 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 에서 다음과 같은 방법으로 확인할 수 있습니다.  
  
-   호출 된 [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 메서드 [getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md), [getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md), 또는 [getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md)합니다.  
  
-   버전은 제품 배포의 readme.txt 파일에 표시됩니다.  
  
 JDBC 드라이버 이름은에서 반환할 수는 또한는 [getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) SQLServerDatabaseMetaData 클래스에 메서드를 호출 합니다. 반환 합니다, 예를 들어, "Microsoft JDBC 드라이버 6.4에 대 한 SQL Server"입니다.  
  
 다음은 SQLServerDatabaseMetaData 클래스의 메서드를 호출에서 출력의 예입니다.  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 여기서 "xxx.x"는 최종 버전 번호입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 관련 문제 진단](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
