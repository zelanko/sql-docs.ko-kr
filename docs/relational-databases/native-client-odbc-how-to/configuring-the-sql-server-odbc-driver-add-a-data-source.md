---
title: 데이터 원본 (ODBC) 추가 | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 21ba3a1507588e0110bbcf281f2cbbe9f41742a3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787941"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>SQL Server ODBC 드라이버 구성 - 데이터 원본 추가
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서 ODBC 응용 프로그램을 사용하려면 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 카탈로그 저장 프로시저의 버전을 업그레이드하는 방법과 데이터 원본을 추가, 삭제 및 테스트하는 방법을 알아 두어야 합니다.  
  
  ODBC 관리자를 프로그래밍 방식으로 사용 하 여 데이터 소스를 추가할 수 있습니다 (사용 하 여 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)), 또는 파일을 만듭니다.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>ODBC 관리자를 사용하여 데이터 원본을 추가하려면  
  
1.  **Control Panel**에 액세스 **관리 도구** 오른쪽 단추로 **ODBC 데이터 원본 (64 비트)** 또는 **ODBC 데이터 원본 (32 비트)**. 또는 odbcad32.exe를 호출할 수도 있습니다.  
  
2.  클릭 합니다 **사용자 DSN**를 **시스템 DSN**, 또는 **파일 DSN** 탭을 클릭 한 다음 **추가**합니다.  
  
3.  클릭 **SQL Server**를 클릭 하 고 **마침**합니다.  
  
4.  단계를 완료 합니다 **SQL Server에 새 데이터 원본 만들기** 마법사.  
  
### <a name="to-add-a-data-source-programmatically"></a>프로그래밍 방식으로 데이터 원본을 추가하려면  
  
1.  호출 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) 두 번째 매개 변수를 ODBC_ADD_DSN 또는 ODBC_ADD_SYS_DSN를 설정 합니다.  
  
### <a name="to-add-a-file-data-source"></a>파일 데이터 원본을 추가하려면  
  
1.  호출 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 를 SAVEFILE = file_name 매개 변수에서 연결 문자열입니다. 연결에 성공하면 ODBC 드라이버가 연결 매개 변수를 사용하여 SAVEFILE 매개 변수가 가리키는 위치에 파일 데이터 원본을 만듭니다.  
  
## <a name="see-also"></a>관련 항목  
[데이터 원본 삭제 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
