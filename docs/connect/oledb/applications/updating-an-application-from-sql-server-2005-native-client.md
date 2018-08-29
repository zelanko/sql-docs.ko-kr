---
title: SQL Server 2005 Native Client에서 응용 프로그램 업데이트 | Microsoft Docs
description: SQL Server 2005 Native Client에서 응용 프로그램 업데이트
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 15d4f01dbf35385e1fba296e5d78e57fa35f16ed
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43034895"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>SQL Server 2005 Native Client에서 응용 프로그램 업데이트
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 항목에서는 이후 SQL Server 용 OLE DB 드라이버의 주요 변경 내용 설명 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]입니다.  

 MDAC(Microsoft Data Access Components)에서 SQL Server용 OLE DB 드라이버로 업그레이드하는 경우에도 몇 가지 동작 차이점이 표시될 수 있습니다. 자세한 내용은 [MDAC에서 SQL Server 용 OLE DB 드라이버로 응용 프로그램 업데이트](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)합니다.  

 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]와 함께 제공되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0. [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]와 함께 제공되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 함께 제공되는 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 10.5. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]와 함께 제공되는 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client 11.0.  

|OLE DB 드라이버의 동작에 비해 SQL Server에 대 한 변경 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client|설명|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB가 정의된 배율로만 패딩됩니다.|변환 된 데이터가 서버로 전송 되는 변환, OLE DB Driver for SQL Server의 최대 길이 까지만 데이터의에서 후행 0을 채웁니다 **날짜/시간** 값입니다. 9자리까지 패딩된 SQL Server Native Client 9.0입니다.|  
|ICommandWithParameter::SetParameterInfo에 대 한 DBTYPE_DBTIMESTAMP의 유효성을 검사 합니다.|OLE DB Driver for SQL Server에 대 한 OLE DB 요구 사항을 구현 *bScale* 에서 ICommandWithParameter::SetParameterInfo DBTYPE_DBTIMESTAMP에 대해 소수 자릿수 초의 정밀도로 설정 되어야 합니다.|  
|합니다 **sp_columns** 저장 프로시저 반환 **"아니요"** 대신 **"아니요"** IS_NULLABLE 열에 대 한 합니다.|OLE DB 드라이버에서 SQL Server에 대 한 **sp_columns** 저장 프로시저 반환 **"아니요"** 대신 **"아니요"** 는 IS_NULLABLE 열에 대 한 합니다.|  
|데이터가 범위를 벗어날 때 서로 다른 오류가 반환되었습니다.|에 대 한 합니다 **날짜/시간** 형식에 다른 오류 번호가 반환 됩니다 OLE DB 드라이버에서 SQL Server에 대 한는 범위를 벗어난 날짜에 대 한 이전 버전에서 반환 된 것입니다.<br /><br /> 특히 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 벗어난 모든 연도 값 문자열 변환에 범위에 대해 22007을 반환 했지만 **datetime**, OLE DB Driver for SQL Server 날짜 지원하는범위내에있을때22008을반환하고**datetime2** 하지만 지 원하는 범위 밖에 **datetime** 하거나 **smalldatetime**합니다.|  
|반올림이 일을 변경하는 경우 **datetime** 값은 소수 자릿수 초를 자르고 반올림되지 않습니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전에는 서버로 전송된 **datetime** 값에 대한 클라이언트 동작에 의해 값이 1초의 1/300에 가깝게 반올림됩니다. OLE DB 드라이버에서 SQL Server에 대 한 두이 일이 변경 반올림 하는 경우 소수 자릿수 초의 잘림이 발생 합니다.|  
|시간 (초)에 대 한 가능한 trunction **날짜/시간** 값입니다.|SQL Server용 OLE DB 드라이버를 사용하여 빌드한 응용 프로그램에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 서버에 연결할 경우 유형 식별자인 DBTYPE_DBTIMESTAMP(OLE DB) 또는 SQL_TIMESTAMP(ODBC) 및 소수 자릿수 0을 사용하여 datetime 열에 바인딩하면 서버에 전송된 시간 데이터 부분에서 초 및 초의 소수 자리 부분이 잘립니다.<br /><br /> 예를 들어 다음과 같이 사용할 수 있습니다.<br /><br /> 입력 데이터: 1994-08-21 21:21:36.000<br /><br /> 삽입된 데이터: 1994-08-21 21:21:00.000|  
|DBTYPE_DBTIME에서 DBTYPE_DATE로 OLE DB 데이터 변환을 수행할 때 더 이상 일이 변경되지 않습니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전에는 DBTYPE_DATE의 시간 부분이 자정의 1/2초 내에 있는 경우 OLE DB 변환 코드로 인해 일이 변경되었습니다. OLE DB 드라이버에서 SQL Server, 일이 (소수 자릿수 초가 잘리고 반올림 되지 않음) 변경 되지 않습니다.|  
|IBCPSession::BCColFmt 변환이 변경 됩니다.|OLE DB 드라이버에서 SQL Server에 대 한 IBCPSession::BCOColFmt를 사용 하 여 SQLDATETIME 또는 SQLDATETIME을 문자열 형식으로 변환할 때 소수 자릿수 값이 내보내집니다. 예를 들어 SQLDATETIME 유형을 SQLNVARCHARMAX 유형으로 변환할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전 버전에서는 다음을 반환했습니다.<br /> 1989-02-01 00:00:00.<br />SQL Server용 OLE DB 드라이버는 다음을 반환합니다. <br />1989-02-01 00:00:00.0000000.|  
|이제 BCP API를 사용하는 사용자 지정 응용 프로그램에서 경고를 볼 수 있습니다.|데이터 길이가 모든 유형의 필드에 대해 지정된 길이보다 큰 경우 BCP API에서 경고 메시지를 생성합니다. 이전에는 이 경고가 문자 유형에 대해서만 제공되었으며 모든 유형에 대해 실행되지 않습니다.|  
|날짜/시간 유형으로 바인딩된 **sql_variant**에 빈 문자열을 삽입하면 오류가 생성됩니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0에서는 날짜/시간 유형으로 바인딩된 **sql_variant**에 빈 문자열을 삽입해도 오류가 생성되지 않았습니다. OLE DB Driver for SQL Server는이 상황에서 오류로 잘못 생성합니다.|  
|트리거가 실행될 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 다른 결과를 반환할 수 있습니다.|[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]에서 변경된 사항으로 인해 **NOCOUNT OFF**가 적용될 때 트리거를 실행하는 명령문에서 다른 결과가 반환될 수도 있습니다. 이 경우 응용 프로그램에서 오류가 발생할 수 있습니다. 이 오류를 해결 하려면 설정 **NOCOUNT ON** 트리거에서 합니다.|  

## <a name="see-also"></a>참고 항목   
 [SQL Server용 OLE DB 드라이버](../../oledb/oledb-driver-for-sql-server.md)
