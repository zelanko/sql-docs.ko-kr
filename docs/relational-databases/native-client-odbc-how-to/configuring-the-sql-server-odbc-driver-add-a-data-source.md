---
title: 데이터 원본 (ODBC) 추가 | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-how-to
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3d0fd3ef5ecf15450f8ba231a6cff288c25e32e7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32945888"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>데이터 원본을 추가 SQL Server ODBC 드라이버 구성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서 ODBC 응용 프로그램을 사용하려면 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 카탈로그 저장 프로시저의 버전을 업그레이드하는 방법과 데이터 원본을 추가, 삭제 및 테스트하는 방법을 알아 두어야 합니다.  
  
  프로그래밍 방식으로 ODBC 관리자를 사용 하 여 데이터 소스를 추가할 수 있습니다 (사용 하 여 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)), 또는 파일을 만듭니다.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>ODBC 관리자를 사용하여 데이터 원본을 추가하려면  
  
1.  **제어판**, 액세스 **관리 도구** 마우스 **ODBC 데이터 원본 (64 비트)** 또는 **ODBC 데이터 원본 (32 비트)**. 또는 odbcad32.exe를 호출할 수도 있습니다.  
  
2.  클릭는 **사용자 DSN**, **시스템 DSN**, 또는 **파일 DSN** 탭을 클릭 한 다음 **추가**합니다.  
  
3.  클릭 **SQL Server**, 클릭 하 고 **마침**합니다.  
  
4.  단계를 완료 된 **SQL Server에 새 데이터 원본을 만들** 마법사.  
  
### <a name="to-add-a-data-source-programmatically"></a>프로그래밍 방식으로 데이터 원본을 추가하려면  
  
1.  호출 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) ODBC_ADD_DSN 또는 ODBC_ADD_SYS_DSN으로 설정 하는 두 번째 매개 변수를 사용 합니다.  
  
### <a name="to-add-a-file-data-source"></a>파일 데이터 원본을 추가하려면  
  
1.  호출 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) 는 SAVEFILE = file_name 매개 변수는 연결 문자열에 있습니다. 연결에 성공하면 ODBC 드라이버가 연결 매개 변수를 사용하여 SAVEFILE 매개 변수가 가리키는 위치에 파일 데이터 원본을 만듭니다.  
  
## <a name="see-also"></a>관련 항목:  
[삭제할 데이터 원본 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
