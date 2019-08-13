---
title: SQL Server용 Microsoft JDBC Driver 지원 매트릭스 | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c5769e67-99f7-4bc1-a4fa-8941dad33d35
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 04d7fe419c8639d9f14c3c3795a1007d947c3998
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893250"
---
# <a name="microsoft-jdbc-driver-for-sql-server-support-matrix"></a>SQL Server용 Microsoft JDBC Driver 지원 매트릭스
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  이 페이지에는 Microsoft JDBC Driver for SQL Server에 대한 지원 매트릭스 및 지원 드라이버에 대한 지원 주기 정책이 포함되어 있습니다.  
  
## <a name="microsoft-jdbc-driver-support-lifecycle-matrix-and-policy"></a>Microsoft JDBC Driver 지원 수명 주기 매트릭스 및 정책  
 MSL(Microsoft 지원 수명 주기) 정책은 Microsoft 제품 지원 수명 주기와 관련해서 투명하고 예측 가능한 정보를 제공합니다. JDBC 드라이버 버전 3.0, 4.x, 6.x 및 7.x는 드라이버 릴리스 날짜로부터 5년 동안 일반 지원을 제공합니다. 일반 지원은 Microsoft 지원 수명 주기 웹 사이트에 정의되어 있습니다.  
  
 확장 및 사용자 지정 지원 옵션은 Microsoft JDBC Driver에는 사용할 수 없습니다.  
    
 다음 Microsoft JDBC Driver는 지정된 지원 종료 날짜까지 지원됩니다.  
  
|드라이버 이름|드라이버 패키지 버전|적용 가능한 JAR|일반 지원 종료|
|-|-|-|-|  
|SQL Server용 Microsoft JDBC Driver 7.4|7.4|mssql-jdbc-7.4.1. jre12<br> mssql-jdbc-7.4.1. jre11<br> mssql-jdbc-7.4.1. jre8|2024 년 8 월 2 일|
|SQL Server용 Microsoft JDBC Driver 7.2|7.2|mssql-jdbc-7.2.2.jre11.jar<br> mssql-jdbc-7.2.2.jre8.jar|2024년 4월 16일|
|SQL Server용 Microsoft JDBC Driver 7.0|7.0|mssql-jdbc-7.0.0.jre10.jar<br> mssql-jdbc-7.0.0.jre8.jar|2023년 7월 31일|  
|SQL Server용 Microsoft JDBC Driver 6.4|6.4|mssql-jdbc-6.4.0.jre9.jar<br> mssql-jdbc-6.4.0.jre8.jar<br> mssql-jdbc-6.4.0.jre7.jar|2023년 2월 27일|    
|SQL Server용 Microsoft JDBC Driver 6.2|6.2|mssql-jdbc-6.2.2.jre8.jar<br> mssql-jdbc-6.2.2.jre7.jar|2022년 6월 30일|    
|Microsoft JDBC Driver 6.0 for SQL Server|6.0|sqljdbc42.jar<br>sqljdbc41.jar|2021년 7월 14일|    
|Microsoft JDBC Driver 4.2 for SQL Server|4.2|sqljdbc42.jar<br>sqljdbc41.jar|2020년 8월 24일|  
|Microsoft JDBC Driver 4.1 for SQL Server|4.1|sqljdbc41.jar|2019년 12월 12일|  
  
 다음 Microsoft JDBC Driver는 더 이상 지원되지 않습니다.  
 
|드라이버 이름|드라이버 패키지 버전|일반 지원 종료|  
|-|-|-|
|SQL Server용 Microsoft JDBC Driver 4.0|4.0|2017년 3월 6일|  
|Microsoft SQL Server JDBC Driver 3.0|3.0|2015년 4월 23일|  
|Microsoft SQL Server JDBC Driver 2.0|2.0|2012년 12월 31일|  
|Microsoft SQL Server 2005 JDBC 드라이버 1.2|1.2|2011년 6월 25일|  
|Microsoft SQL Server 2005 JDBC Driver 1.1|1.1|2011년 6월 25일|  
|Microsoft SQL Server 2005 JDBC Driver 1.0|1.0|2011년 6월 25일|  
|Microsoft SQL Server 2000 JDBC Driver|2000|2010년 7월 9일|  
  
## <a name="sql-version-compatibility"></a>SQL 버전 호환성  
  
|드라이버 버전|SQL Server 2008|SQL Server 2008R2|SQL Server 2012|Azure SQL 데이터베이스|PDW 2008R2 AU3<sup>4</sup>|SQL Server 2014|SQL Server 2016|SQL Server 2017|SQL Server 2019|  
|-|-|-|-|-|-|-|-|-|-|-|
|7.4|N|N|Y|Y|Y|Y|Y|Y|Y|
|7.2|N|Y|Y|Y|Y|Y|Y|Y|N| 
|7.0|N|Y|Y|Y|Y|Y|Y|Y|N| 
|6.4|N|Y|Y|Y|Y|Y|Y|Y|N| 
|6.2|Y|Y|Y|Y|Y|Y|Y|Y|N|
|6.1|Y|Y|Y|Y|Y|Y|Y|N|N|
|6.0|Y|Y|Y|Y|Y|Y|Y|N|N|
|4.2|Y|Y|Y|Y|Y|Y|Y|N|N|
|4.1|Y|Y|Y|Y|Y|Y|Y|N|N|
|4.0|Y|Y|Y|Y|Y|Y|Y|N|N|
|3.0|Y|Y|Y<sup>1</sup>|Y<sup>2</sup>|N|Y<sup>5</sup>|N|N|N|
|2.0|Y<sup>3</sup>|Y<sup>3</sup>|N|N|N|N|N|N|N|
|1.2|Y<sup>3</sup>|N|N|N|N|N|N|N|N|
|1.1|N|N|N|N|N|N|N|N|N|  
|1.0|N|N|N|N|N|N|N|N|N|  
|2000|N|N|N|N|N|N|N|N|N|  
  
 <sup>1</sup>Microsoft SQL Server JDBC Driver 버전 3.0은 하위 수준 클라이언트로 SQL Server 2012에 연결될 수 있습니다.  
  
 <sup>2</sup>Azure SQL Database에 대한 지원은 3.0 드라이버에서 핫픽스로 도입되었습니다. Azure SQL 데이터베이스 고객은 사용 가능한 최신 드라이버 버전을 사용하는 것이 좋습니다.  
  
 <sup>3</sup>Microsoft SQL Server JDBC Driver 버전 2.0 및 Microsoft SQL Server 2005 JDBC Driver 버전 1.2는 하위 수준 클라이언트로 SQL Server 2008에 연결될 수 있습니다. 하위 수준 변환이 허용되는 경우 애플리케이션은 쿼리를 실행하고 시간, 날짜, datetime2, datetimeoffset 및 FILESTREAM 등 새로운 SQL Server 2008 데이터 형식을 업데이트할 수 있습니다. JDBC Driver와 함께 이러한 새로운 데이터 형식을 사용하는 방법에 대한 자세한 내용은  [JDBC Driver를 사용하여 SQL Server 2008 날짜/시간 데이터 형식 작업](https://go.microsoft.com/fwlink/?LinkId=145198) 및  [JDBC Driver를 사용하 여 SQL Server 2008 FileStream 작업](https://go.microsoft.com/fwlink/?LinkId=145199)을 참조하세요. 이러한 새 데이터 형식의 하위 수준 호환성에 대한 자세한 내용은 SQL Server 온라인 설명서의  [날짜 및 시간 데이터 사용](https://go.microsoft.com/fwlink/?LinkId=145211)및  [FILESTREAM 지원](https://go.microsoft.com/fwlink/?LinkId=145212) 항목을 참조하세요.  
  
 <sup>4</sup>Microsoft JDBC Driver와 병렬 데이터 웨어하우스 간의 연결 지원은 SQL Server용 Microsoft JDBC Driver 4.0 및 Microsoft SQL Server 2008 R2 병렬 데이터 웨어하우스 어플라이언스 업데이트 3에 최초로 도입되었습니다.  
  
 <sup>5</sup>Microsoft SQL Server JDBC Driver 버전 3.0은 하위 수준 클라이언트로 SQL Server 2014에 연결될 수 있습니다.  
  
## <a name="java-and-jdbc-specification-support"></a>Java 및 JDBC 사양 지원  
  
|JDBC 드라이버 버전|JRE 버전|JDBC API 버전| 
|-|-|-|  
|7.4|1.8, 11, 12|4.2, 4.3(부분)|
|7.2|1.8, 11|4.2, 4.3(부분)|
|7.0|1.8, 10|4.2, 4.3(부분)|
|6.4|1.7, 1.8, 9|4.1, 4.2, 4.3(부분)|  
|6.2|1.7, 1.8|4.1, 4.2|  
|6.1|1.7, 1.8|4.1, 4.2|  
|6.0|1.7, 1.8|4.1, 4.2|  
|4.2|1.7, 1.8|4.1, 4.2|  
|4.1|1.7|4.0|  
|4.0|1.5, 1.6, 1.7|3.0, 4.0|  
|3.0|1.5, 1.6,|3.0, 4.0|  
|2.0|1.5, 1.6|3.0, 4.0|  
|1.2|1.4, 1.5, 1.6|3.0|  
|1.1|1.4|3.0|  
|1.0|1.4|3.0|  
|2000|1.4|3.0|  
  
## <a name="supported-operating-systems"></a>지원되는 운영 체제  
 Microsoft JDBC Driver는 JVM(Java Virtual Machine)의 사용을 지원하는 모든 운영 체제에서 작동하도록 설계되어 있지만 일부 자주 사용되는 플랫폼에는 Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2008 R2, Windows Vista, Linux, Unix, AIX, MacOS 등이 포함됩니다.  
  
 JDBC 제품 팀은 Windows, Sun Solaris, SUSE Linux 및 RedHat Linux에서 Microsoft 드라이버를 테스트합니다.  고객 지원 센터는 모든 플랫폼의 고객이 사용할 수 있지만 Windows와 같은 플랫폼에서 문제를 재현하도록 요청될 수 있습니다.  
  
## <a name="application-server-support"></a>응용 프로그램 서버 지원  
 Microsoft JDBC Driver for SQL Server는 다양한 애플리케이션 서버에서 테스트됩니다.  사용 중인 제품과 호환되는 드라이버 버전에 대한 추가 세부 정보를 얻으려면 애플리케이션 서버 공급업체에 문의하세요.
 
 