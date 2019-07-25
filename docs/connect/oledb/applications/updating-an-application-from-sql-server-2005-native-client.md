---
title: SQL Server 2005 Native Client에서 애플리케이션 업데이트 | Microsoft Docs
description: SQL Server 2005 Native Client에서 애플리케이션 업데이트
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, updating applications
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 7915b9fb74f05057e05eef022d7f9b0e4ccdd21f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989252"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>SQL Server 2005 Native Client에서 애플리케이션 업데이트
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 항목에서는의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]Native Client 이후 SQL Server OLE DB 드라이버의 주요 변경 내용에 대해 설명 합니다.  

 MDAC(Microsoft Data Access Components)에서 SQL Server용 OLE DB 드라이버로 업그레이드하는 경우에도 몇 가지 동작 차이점이 표시될 수 있습니다. 자세한 내용은 [MDAC의 SQL Server에 대 한 OLE DB 드라이버로 응용 프로그램 업데이트](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)를 참조 하세요.  

 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]와 함께 제공되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0. [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]와 함께 제공되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 함께 제공되는 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 10.5. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]와 함께 제공되는 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client 11.0.  

|Native Client와 비교 하 여 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] SQL Server에 대 한 OLE DB 드라이버의 변경 된 동작|설명|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB가 정의된 배율로만 패딩됩니다.|변환 된 데이터가 서버로 전송 되는 변환의 경우 SQL Server 드라이버 OLE DB 데이터의 후행 0을 **datetime** 값의 최대 길이 까지만 채웁니다. 9자리까지 패딩된 SQL Server Native Client 9.0입니다.|  
|ICommandWithParameter:: SetParameterInfo에 대 한 DBTYPE_DBTIMESTAMP의 유효성을 검사 합니다.|SQL Server 용 OLE DB Driver for ICommandWithParameter:: SetParameterInfo *에 대 한* OLE DB 요구 사항을 구현 하 여 DBTYPE_DBTIMESTAMP에 대 한 소수 자릿수 초의 전체 자릿수를 설정 합니다.|  
|**Sp_columns** 저장 프로시저는 이제 IS_NULLABLE 열에 대해 **"no** " 대신 **"no"** 를 반환 합니다.|SQL Server에 대 한 OLE DB 드라이버에서 이제 **sp_columns** 저장 프로시저는 IS_NULLABLE 열에 대해 **"no** " 대신 **"no"** 를 반환 합니다.|  
|데이터가 범위를 벗어날 때 서로 다른 오류가 반환되었습니다.|**Datetime** 형식의 경우 이전 버전에서 반환 된 것 보다 범위를 벗어난 날짜에 대 한 SQL Server OLE DB 드라이버에서 다른 오류 번호가 반환 됩니다.<br /><br /> 구체적으로 말하면 Native Client 9.0는 **datetime**으로의 문자열 변환 시 범위를 벗어난 모든 연도 값에 대해 22007을 반환 하 고, SQL Server OLE DB 드라이버는 날짜가 **datetime2**에서 지원 되는 범위 내에 있지만 외부에 있는 경우 22008을 반환 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 합니다. **datetime** 또는 **smalldatetime**에서 지원 되는 범위입니다.|  
|반올림이 일을 변경하는 경우 **datetime** 값은 소수 자릿수 초를 자르고 반올림되지 않습니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전에는 서버로 전송된 **datetime** 값에 대한 클라이언트 동작에 의해 값이 1초의 1/300에 가깝게 반올림됩니다. SQL Server에 대 한 OLE DB 드라이버에서이 시나리오는 반올림이 날짜를 변경 하는 경우 소수 자릿수 초의 잘림을 발생 시킵니다.|  
|**Datetime** 값에 대해 가능한 trunction (초)입니다.|SQL Server용 OLE DB 드라이버를 사용하여 빌드한 애플리케이션에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 서버에 연결할 경우 유형 식별자인 DBTYPE_DBTIMESTAMP(OLE DB) 또는 SQL_TIMESTAMP(ODBC) 및 소수 자릿수 0을 사용하여 datetime 열에 바인딩하면 서버에 전송된 시간 데이터 부분에서 초 및 초의 소수 자리 부분이 잘립니다.<br /><br /> 예를 들어<br /><br /> 입력 데이터: 1994-08-21 21:21:36.000<br /><br /> 삽입된 데이터: 1994-08-21 21:21:00.000|  
|DBTYPE_DBTIME에서 DBTYPE_DATE로 OLE DB 데이터 변환을 수행할 때 더 이상 일이 변경되지 않습니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전에는 DBTYPE_DATE의 시간 부분이 자정의 1/2초 내에 있는 경우 OLE DB 변환 코드로 인해 일이 변경되었습니다. SQL Server에 대 한 OLE DB 드라이버에서 일은 변경 되지 않습니다 (소수 자릿수 초는 잘리고 반올림 되지 않음).|  
|IBCPSession:: BCColFmt 변환 변경 내용입니다.|SQL Server에 대 한 OLE DB 드라이버에서 IBCPSession:: BCOColFmt를 사용 하 여 SQLDATETIME 또는 SQLDATETIME를 문자열 형식으로 변환 하는 경우 소수 값을 내보냅니다. 예를 들어 SQLDATETIME 유형을 SQLNVARCHARMAX 유형으로 변환할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전 버전에서는 다음을 반환했습니다.<br /> 1989-02-01 00:00:00.<br />SQL Server용 OLE DB 드라이버는 다음을 반환합니다. <br />1989-02-01 00:00:00.0000000.|  
|이제 BCP API를 사용하는 사용자 지정 응용 프로그램에서 경고를 볼 수 있습니다.|데이터 길이가 모든 유형의 필드에 대해 지정된 길이보다 큰 경우 BCP API에서 경고 메시지를 생성합니다. 이전에는 이 경고가 문자 유형에 대해서만 제공되었으며 모든 유형에 대해 실행되지 않습니다.|  
|날짜/시간 유형으로 바인딩된 **sql_variant**에 빈 문자열을 삽입하면 오류가 생성됩니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0에서는 날짜/시간 유형으로 바인딩된 **sql_variant**에 빈 문자열을 삽입해도 오류가 생성되지 않았습니다. SQL Server에 대 한 OLE DB 드라이버는이 상황에서 오류를 생성 합니다.|  
|트리거가 실행될 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 다른 결과를 반환할 수 있습니다.|[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]에서 변경된 사항으로 인해 **NOCOUNT OFF**가 적용될 때 트리거를 실행하는 명령문에서 다른 결과가 반환될 수도 있습니다. 이 경우 응용 프로그램에서 오류가 발생할 수 있습니다. 이 오류를 해결 하려면 트리거에서 **NOCOUNT on** 을 설정 합니다.|  

## <a name="see-also"></a>참고 항목   
 [SQL Server용 OLE DB 드라이버](../../oledb/oledb-driver-for-sql-server.md)
