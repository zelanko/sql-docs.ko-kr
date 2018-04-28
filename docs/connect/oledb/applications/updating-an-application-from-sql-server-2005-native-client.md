---
title: SQL Server 2005 Native Client에서 응용 프로그램 업데이트 | Microsoft Docs
description: SQL Server 2005 Native Client에서 응용 프로그램 업데이트
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8c5548467122f2669fe049b39e6bc9800e2160b7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>SQL Server 2005 Native Client에서 응용 프로그램 업데이트
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 항목에서는 이후 SQL Server 용 OLE DB Driver의 주요 변경 내용 설명 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]합니다.  

 Microsoft 데이터 액세스 Components (MDAC)에서 OLE DB driver for SQL Server를 업그레이드 하면 몇 가지 동작 차이점이 참고할 수 있습니다. 자세한 내용은 참조 [MDAC에서 SQL Server 용 OLE DB Driver로 응용 프로그램 업데이트](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)합니다.  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 함께 제공 된 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 함께 제공 된 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]합니다.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 함께 제공되는 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 10.5. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]와 함께 제공되는 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client 11.0.  

|SQL Server에 비해에 대 한 OLE DB 드라이버에서 동작을 변경 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client|Description|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB가 정의된 배율로만 패딩됩니다.|서버에 변환 된 데이터를 보내는 위치 변환에 대 한 OLE DB Driver for SQL Server의 최대 길이 까지만 데이터의 후행 0에서 채우는 **datetime** 값입니다. 9자리까지 패딩된 SQL Server Native Client 9.0입니다.|  
|ICommandWithParameter::SetParameterInfo에 대 한 DBTYPE_DBTIMESTAMP의 유효성을 검사 합니다.|OLE DB Driver for SQL Server에 대 한 OLE DB 요구 사항을 구현 *bScale* 에 ICommandWithParameter::SetParameterInfo DBTYPE_DBTIMESTAMP에 대해 소수 자릿수 초의 정밀도로 설정 해야 합니다.|  
|**sp_columns** 저장 프로시저 반환 **"NO"** 대신 **"NO"** IS_NULLABLE 열에 대 한 합니다.|OLE DB 드라이버에서 SQL Server, **sp_columns** 저장 프로시저 반환 **"NO"** 대신 **"NO"** 는 IS_NULLABLE 열에 대 한 합니다.|  
|데이터가 범위를 벗어날 때 서로 다른 오류가 반환되었습니다.|에 대 한는 **datetime** 형식에는 다른 오류 번호가 반환 됩니다 OLE DB 드라이버에서 SQL Server에 대 한 범위를 벗어난 날짜에 대 한 이전 버전에서 반환 된 것입니다.<br /><br /> 특히, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 벗어난 모든 연도 값 문자열 변환에 범위에 대해 22007을 반환 했지만 **datetime**, OLE DB Driver for SQL Server 날짜 에서지원하는범위내에있을때22008을반환하고**datetime2** 에서 지 원하는 범위 외부에 있으면 서 **datetime** 또는 **smalldatetime**합니다.|  
|**날짜/시간** if 라운드 하지 반올림이 일을 변경 및 소수 자릿수 초 값이 잘립니다.|이전에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0에 대 한 클라이언트 동작 **datetime** 서버로 전송 하는 값 1에 가깝게 반올림 됩니다/300 초입니다. OLE DB 드라이버에서 SQL Server에 대 한 두이 일이 변경 되 반올림 하는 경우 소수 자릿수 초의 잘림이 발생 합니다.|  
|에 대 한 초가 잘릴 수 있습니다 **datetime** 값입니다.|에 연결 하는 SQL Server 용 OLE DB 드라이버를 사용 하 여 빌드한 응용 프로그램을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 서버 초와 유형 식별자 인 DBTYPE_DBTIMESTAMP (지정 된 datetime 열에 바인딩하면 서버에 전송 되는 데이터의 시간 부분에 대 한 소수 자릿수 초가 잘립니다 OLE DB) 또는 SQL_TIMESTAMP (ODBC) 및 소수 자릿수가 0입니다.<br /><br /> 예를 들어:<br /><br /> 입력 데이터: 1994-08-21 21:21:36.000<br /><br /> 데이터 삽입: 1994-08-21 21:21:00.000|  
|DBTYPE_DBTIME에서 DBTYPE_DATE로 OLE DB 데이터 변환을 수행할 때 더 이상 일이 변경되지 않습니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전에는 DBTYPE_DATE의 시간 부분이 자정의 1/2초 내에 있는 경우 OLE DB 변환 코드로 인해 일이 변경되었습니다. OLE DB 드라이버에서 SQL Server, 일이 변경 (소수 자릿수 초가 잘리고 반올림 되지 않음).|  
|IBCPSession::BCColFmt 변환이 변경 됩니다.|OLE DB 드라이버에서 SQL Server에 대 한 IBCPSession::BCOColFmt를 사용 하 여 SQLDATETIME 또는 SQLDATETIME을 문자열 형식으로 변환 하는 소수 자릿수 값이 내보내집니다. 예를 들어 변환 형식 때 SQLNVARCHARMAX, 이전 버전을 입력 하 여 SQLDATETIME [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 반환<br /> 1989-02-01 00:00:00.<br />OLE DB Driver for SQL Server 반환 <br />1989-02-01 00:00:00.0000000.|  
|이제 BCP API를 사용하는 사용자 지정 응용 프로그램에서 경고를 볼 수 있습니다.|데이터 길이가 모든 유형의 필드에 대해 지정된 길이보다 큰 경우 BCP API에서 경고 메시지를 생성합니다. 이전에는 이 경고가 문자 유형에 대해서만 제공되었으며 모든 유형에 대해 실행되지 않습니다.|  
|에 빈 문자열을 삽입 한 **sql_variant** 오류를 생성 하는 날짜/시간 유형으로 바인딩된 합니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0에서는에 빈 문자열을 삽입 한 **sql_variant** 바운드 날짜/시간 유형 오류를 생성 하지 않았습니다. OLE DB Driver for SQL Server는 잘못이 상황에서 오류를 생성합니다.|  
|트리거가 실행될 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 다른 결과를 반환할 수 있습니다.|에 도입 된 변경 내용은 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 응용 프로그램 트리거를 실행할 때 발생 하는 문에서 반환 하는 다른 결과가 발생할 수 있습니다 **NOCOUNT OFF** 가 적용 됩니다. 이 경우 응용 프로그램에서 오류가 발생할 수 있습니다. 이 오류를 해결 하려면 설정 **NOCOUNT ON** 트리거의 합니다.|  

## <a name="see-also"></a>관련 항목:   
 [SQL Server용 OLE DB 드라이버](../../oledb/oledb-driver-for-sql-server.md)
