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
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67989252"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>SQL Server 2005 Native Client에서 애플리케이션 업데이트
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 이후에 OLE DB Driver for SQL Server에 대해 이루어진 주요 변경 사항을 설명합니다.  

 MDAC(Microsoft Data Access Components)에서 SQL Server용 OLE DB 드라이버로 업그레이드하는 경우에도 몇 가지 동작 차이점이 표시될 수 있습니다. 자세한 내용은 [MDAC에서 OLE DB Driver for SQL Server로 애플리케이션 업데이트](../../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)를 참조하세요.  

 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 함께 제공되는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 9.0. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 함께 제공되는 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 10.0.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 함께 제공되는 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 10.5. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]와 함께 제공되는 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client 11.0.  

|[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client와 비교하여 OLE DB Driver for SQL Server의 동작이 변경됨|Description|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB가 정의된 배율로만 패딩됩니다.|변환된 데이터가 서버로 전송되는 변환의 경우 OLE DB Driver for SQL Server는 데이터의 후행 0을 **datetime** 값의 최대 길이까지만 패딩합니다. 9자리까지 패딩된 SQL Server Native Client 9.0입니다.|  
|ICommandWithParameter::SetParameterInfo에 대한 DBTYPE_DBTIMESTAMP의 유효성을 검사합니다.|OLE DB Driver for SQL Server는 ICommandWithParameter::SetParameterInfo에서 *bScale*에 대한 OLE DB 요구 사항을 구현하여 DBTYPE_DBTIMESTAMP에 대해 소수 초 정밀도로 설정합니다.|  
|이제 **sp_columns** 저장 프로시저는 IS_NULLABLE 열에 대해 **"NO "** 대신 **"NO"** 를 반환합니다.|OLE DB Driver for SQL Server에서 **sp_columns** 저장 프로시저는 IS_NULLABLE 열에 대해 **"NO "** 대신 **"NO"** 를 반환합니다.|  
|데이터가 범위를 벗어날 때 서로 다른 오류가 반환되었습니다.|**datetime** 유형의 경우 범위를 벗어난 날짜에 대해 이전 버전에서 반환된 것과는 다른 오류 번호가 OLE DB Driver for SQL Server에서 반환됩니다.<br /><br /> 구체적으로, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0에서는 **datetime**으로의 문자열 변환 시 범위를 벗어난 모든 연도 값에 대해 22007을 반환했지만 OLE DB Driver for SQL Server에서는 날짜가 **datetime2**에서 지원되는 범위 내에 있지만 **datetime** 또는 **smalldatetime**에서 지원되는 범위를 벗어날 때 22008을 반환합니다.|  
|반올림이 일을 변경하는 경우 **datetime** 값은 소수 자릿수 초를 자르고 반올림되지 않습니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전에는 서버로 전송된 **datetime** 값에 대한 클라이언트 동작에 의해 값이 1초의 1/300에 가깝게 반올림됩니다. OLE DB Driver for SQL Server부터 이 시나리오를 사용하면 반올림으로 인해 일이 변경되는 경우 소수 자릿수 초가 잘립니다.|  
|**datetime** 값에서 초가 잘릴 수 있습니다.|SQL Server용 OLE DB 드라이버를 사용하여 빌드한 애플리케이션에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 서버에 연결할 경우 유형 식별자인 DBTYPE_DBTIMESTAMP(OLE DB) 또는 SQL_TIMESTAMP(ODBC) 및 소수 자릿수 0을 사용하여 datetime 열에 바인딩하면 서버에 전송된 시간 데이터 부분에서 초 및 초의 소수 자리 부분이 잘립니다.<br /><br /> 다음은 그 예입니다.<br /><br /> 입력 데이터: 1994-08-21 21:21:36.000<br /><br /> 삽입된 데이터: 1994-08-21 21:21:00.000|  
|DBTYPE_DBTIME에서 DBTYPE_DATE로 OLE DB 데이터 변환을 수행할 때 더 이상 일이 변경되지 않습니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전에는 DBTYPE_DATE의 시간 부분이 자정의 1/2초 내에 있는 경우 OLE DB 변환 코드로 인해 일이 변경되었습니다. OLE DB Driver for SQL Server에서 일이 변경되지 않습니다(소수 자릿수 초가 잘리고 반올림되지 않음).|  
|IBCPSession::BCColFmt 변환이 변경됩니다.|OLE DB Driver for SQL Server에서 IBCPSession::BCOColFmt를 사용하여 SQLDATETIME 또는 SQLDATETIME을 문자열 유형으로 변환하면 소수 값이 내보내집니다. 예를 들어 SQLDATETIME 유형을 SQLNVARCHARMAX 유형으로 변환할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전 버전에서는 다음을 반환했습니다.<br /> 1989-02-01 00:00:00.<br />SQL Server용 OLE DB 드라이버는 다음을 반환합니다. <br />1989-02-01 00:00:00.0000000.|  
|이제 BCP API를 사용하는 사용자 지정 애플리케이션에서 경고를 볼 수 있습니다.|데이터 길이가 모든 유형의 필드에 대해 지정된 길이보다 큰 경우 BCP API에서 경고 메시지를 생성합니다. 이전에는 이 경고가 문자 유형에 대해서만 제공되었으며 모든 유형에 대해 실행되지 않습니다.|  
|날짜/시간 유형으로 바인딩된 **sql_variant**에 빈 문자열을 삽입하면 오류가 생성됩니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0에서는 날짜/시간 유형으로 바인딩된 **sql_variant**에 빈 문자열을 삽입해도 오류가 생성되지 않았습니다. OLE DB Driver for SQL Server에서는 이 경우 올바르게 오류를 생성합니다.|  
|트리거가 실행될 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 다른 결과를 반환할 수 있습니다.|[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]에서 변경된 사항으로 인해 **NOCOUNT OFF**가 적용될 때 트리거를 실행하는 명령문에서 다른 결과가 반환될 수도 있습니다. 이 경우 애플리케이션에서 오류가 발생할 수 있습니다. 이 오류를 해결하려면 트리거에서 **NOCOUNT ON**을 설정합니다.|  

## <a name="see-also"></a>참고 항목   
 [SQL Server용 OLE DB 드라이버](../../oledb/oledb-driver-for-sql-server.md)
