---
title: 데이터 원본 추가 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c050efd2f309ccec76b80fd24b519e7d2389e4ea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63126077"
---
# <a name="add-a-data-source-odbc"></a>데이터 원본 추가(ODBC)
  ODBC 관리자를 사용 하 여 프로그래밍 방식으로 ( [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)사용) 또는 파일을 만들어 데이터 원본을 추가할 수 있습니다.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>ODBC 관리자를 사용하여 데이터 원본을 추가하려면  
  
1.  **제어판**에서 **관리 도구** , **데이터 원본 (ODBC)** 에 액세스 합니다. 또는 odbcad32.exe를 호출할 수도 있습니다.  
  
2.  **사용자 dsn**, **시스템 DSN**또는 **파일 dsn** 탭을 클릭 한 다음 **추가**를 클릭 합니다.  
  
3.  **SQL Server**를 클릭 한 다음 **마침**을 클릭 합니다.  
  
4.  SQL Server에 새로운 데이터 원본 만들기 마법사의 각 단계를 완료합니다.  
  
### <a name="to-add-a-data-source-programmatically"></a>프로그래밍 방식으로 데이터 원본을 추가하려면  
  
1.  ODBC_ADD_DSN 또는 ODBC_ADD_SYS_DSN로 설정 된 두 번째 매개 변수를 사용 하 여 [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md) 를 호출 합니다.  
  
### <a name="to-add-a-file-data-source"></a>파일 데이터 원본을 추가하려면  
  
1.  연결 문자열에서 SAVEFILE = file_name 매개 변수를 사용 하 여 [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md) 를 호출 합니다. 연결에 성공하면 ODBC 드라이버가 연결 매개 변수를 사용하여 SAVEFILE 매개 변수가 가리키는 위치에 파일 데이터 원본을 만듭니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server ODBC 드라이버 구성 방법 도움말 항목](../../database-engine/dev-guide/configuring-the-sql-server-odbc-driver-how-to-topics.md)  
  
  
