---
title: 데이터 원본 (ODBC) 추가 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 822ac0f5d2e228a982368849ed1c409ef63765ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181793"
---
# <a name="add-a-data-source-odbc"></a>데이터 원본 추가(ODBC)
  프로그래밍 방식으로 ODBC 관리자를 사용 하 여 데이터 소스를 추가할 수 있습니다 (사용 하 여 [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)), 또는 파일을 만듭니다.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>ODBC 관리자를 사용하여 데이터 원본을 추가하려면  
  
1.  **제어판**, 액세스 **관리 도구** 차례로 **데이터 원본 (ODBC)** 합니다. 또는 odbcad32.exe를 호출할 수도 있습니다.  
  
2.  클릭는 **사용자 DSN**, **시스템 DSN**, 또는 **파일 DSN** 탭을 클릭 한 다음 **추가**합니다.  
  
3.  클릭 **SQL Server**, 클릭 하 고 **마침**합니다.  
  
4.  SQL Server에 새로운 데이터 원본 만들기 마법사의 각 단계를 완료합니다.  
  
### <a name="to-add-a-data-source-programmatically"></a>프로그래밍 방식으로 데이터 원본을 추가하려면  
  
1.  호출 [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md) ODBC_ADD_DSN 또는 ODBC_ADD_SYS_DSN으로 설정 하는 두 번째 매개 변수를 사용 합니다.  
  
### <a name="to-add-a-file-data-source"></a>파일 데이터 원본을 추가하려면  
  
1.  호출 [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md) 는 SAVEFILE = file_name 매개 변수는 연결 문자열에 있습니다. 연결에 성공하면 ODBC 드라이버가 연결 매개 변수를 사용하여 SAVEFILE 매개 변수가 가리키는 위치에 파일 데이터 원본을 만듭니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server ODBC 드라이버 구성 방법 도움말 항목](../../database-engine/dev-guide/configuring-the-sql-server-odbc-driver-how-to-topics.md)  
  
  