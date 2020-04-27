---
title: ODBC 데이터 원본 SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, about data sources
- ODBC data sources, names
- data sources [SQL Server Native Client]
- names [ODBC]
- ODBC applications, data sources
- SQL Server Native Client ODBC driver, data sources
- ODBC data sources
ms.assetid: a6a50fd0-d439-43fd-b76f-16ec02f478c5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de1226d675859312e1ccaf908141586f865c8946
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63028390"
---
# <a name="sql-server-native-client-odbc-data-sources"></a>SQL Server Native Client ODBC 데이터 원본
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DSN(데이터 원본 이름)은 ODBC 애플리케이션이 특정 서버의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 데 필요한 모든 정보가 포함된 ODBC 데이터 원본을 식별합니다. ODBC 데이터 원본 이름은 다음 두 가지 방법으로 정의할 수 있습니다.  
  
-   클라이언트 컴퓨터의 제어판에서 관리 도구를 열고 **데이터 원본 (ODBC)** 을 두 번 클릭 합니다. DSN을 만드는 데 사용하는 ODBC 데이터 원본 관리자가 열립니다.  
  
-   ODBC 응용 프로그램에서 [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)를 호출 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본에는 다음 항목이 포함됩니다.  
  
-   데이터 원본의 이름입니다.  
  
-   특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하는 데 필요한 정보  
  
-   특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 사용할 기본 데이터베이스(옵션)  
  
-   사용할 ANSI 옵션, 성능 통계 기록 여부 등의 설정(옵션)  
  
 ODBC 애플리케이션이 반드시 데이터 원본을 통해 연결해야 하는 것은 아니지만 이와 같은 연결 정보를 ODBC 연결 함수에 제공해야 합니다. 그렇지 않으면 드라이버가 DSN에서 연결 정보를 찾습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server &#40;ODBC&#41;와 통신](communicating-with-sql-server-odbc.md)  
  
  
