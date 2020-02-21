---
title: 드라이버 버전 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e241d72-16da-4ada-ac67-e6308394108f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db44a391c16a63d28057c99755018179d6c2c0b5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028039"
---
# <a name="getting-the-driver-version"></a>드라이버 버전 가져오기
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  설치된 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 버전은 다음과 같은 방법으로 찾을 수 있습니다.  
  
-   [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 메서드 [getDriverMajorVersion](../../connect/jdbc/reference/getdrivermajorversion-method-sqlserverdatabasemetadata.md), [getDriverMinorVersion](../../connect/jdbc/reference/getdriverminorversion-method-sqlserverdatabasemetadata.md) 또는 [getDriverVersion](../../connect/jdbc/reference/getdriverversion-method-sqlserverdatabasemetadata.md)을 호출합니다.  
  
-   버전은 제품 배포의 readme.txt 파일에 표시됩니다.  
  
 또한 JDBC 드라이버 이름은 SQLServerDatabaseMetaData 클래스의 [getDriverName](../../connect/jdbc/reference/getdrivername-method-sqlserverdatabasemetadata.md) 메서드 호출에서 반환될 수 있습니다. 예를 들어 이 메서드는 “SQL Server용 Microsoft JDBC Driver 6.4”를 반환합니다.  
  
 다음은 SQLServerDatabaseMetaData 클래스의 메서드를 호출하는 경우의 출력 예입니다.  
  
 `getDriverName = Microsoft JDBC Driver 6.4 for SQL Server`  
  
 `getDriverMajorVersion = 6`  
  
 `getDriverMinorVersion = 4`  
  
 `getDriverVersion = 6.4.` *xxx.x*  
  
 여기서 "xxx.x"는 최종 버전 번호입니다.  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 관련 문제 진단](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
