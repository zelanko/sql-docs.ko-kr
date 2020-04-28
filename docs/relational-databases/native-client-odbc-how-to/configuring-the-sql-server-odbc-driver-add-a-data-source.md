---
title: 데이터 원본 추가 (ODBC) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 55ae4f357aa850f6b3ff4ba9cca0b59a2ccbc570
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298336"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>SQL Server ODBC 드라이버 구성 - 데이터 원본 추가
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서 ODBC 애플리케이션을 사용하려면 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 카탈로그 저장 프로시저의 버전을 업그레이드하는 방법과 데이터 원본을 추가, 삭제 및 테스트하는 방법을 알아 두어야 합니다.  
  
  ODBC 관리자를 사용 하 여 프로그래밍 방식으로 ( [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)사용) 또는 파일을 만들어 데이터 원본을 추가할 수 있습니다.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>ODBC 관리자를 사용하여 데이터 원본을 추가하려면  
  
1.  **제어판**에서 **관리 도구** 를 선택한 다음 **odbc 데이터 원본 (64 비트)** 또는 **odbc 데이터 원본 (32 비트)** 중 하나를 선택 합니다. 또는 odbcad32.exe를 호출할 수도 있습니다.  
  
2.  **사용자 dsn**, **시스템 DSN**또는 **파일 dsn** 탭을 클릭 한 다음 **추가**를 클릭 합니다.  
  
3.  **SQL Server**를 클릭 한 다음 **마침**을 클릭 합니다.  
  
4.  **SQL Server 새 데이터 소스 만들기** 마법사의 단계를 완료 합니다.  
  
### <a name="to-add-a-data-source-programmatically"></a>프로그래밍 방식으로 데이터 원본을 추가하려면  
  
1.  ODBC_ADD_DSN 또는 ODBC_ADD_SYS_DSN로 설정 된 두 번째 매개 변수를 사용 하 여 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) 를 호출 합니다.  
  
### <a name="to-add-a-file-data-source"></a>파일 데이터 원본을 추가하려면  
  
1.  연결 문자열에서 SAVEFILE = file_name 매개 변수를 사용 하 여 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 를 호출 합니다. 연결에 성공하면 ODBC 드라이버가 연결 매개 변수를 사용하여 SAVEFILE 매개 변수가 가리키는 위치에 파일 데이터 원본을 만듭니다.  
  
## <a name="see-also"></a>참고 항목  
[ODBC&#41;&#40;데이터 원본 삭제](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
