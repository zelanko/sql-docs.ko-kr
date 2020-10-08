---
description: SQLBrowseConnect
title: SQLBrowseConnect | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBrowseConnect function
ms.assetid: 57faf388-c7ca-4696-9845-34e0a10cc5f7
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3aed2ce31a79a51eadd9db7fdc1afc042d01efaa
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91811155"
---
# <a name="sqlbrowseconnect"></a>SQLBrowseConnect
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **SQLBrowseConnect** 는 세 가지 수준의 연결 정보로 분류할 수 있는 키워드를 사용 합니다. 다음 표에서는 각 키워드에 대해 유효한 값 목록의 반환 여부와 키워드가 선택 사항인지 여부를 보여 줍니다.  
  
## <a name="level-1"></a>수준 1  
  
|키워드|목록 반환 여부|선택 사항 여부|Description|  
|-------------|--------------------|---------------|-----------------|  
|DSN|해당 없음|예|**Sqldatasources**원본에서 반환 되는 데이터 원본의 이름입니다. DRIVER 키워드가 사용되는 경우에는 DSN 키워드를 사용할 수 없습니다.|  
|DRIVER|해당 없음|예|Microsoft® [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 드라이버 이름은 { [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client 11}입니다. DSN 키워드가 사용되는 경우에는 DRIVER 키워드를 사용할 수 없습니다.|  
  
## <a name="level-2"></a>수준 2  
  
|키워드|목록 반환 여부|선택 사항 여부|Description|  
|-------------|--------------------|---------------|-----------------|  
|SERVER|예|예|데이터 원본이 있는 네트워크의 서버 이름입니다. "(로컬)"이란 용어를 서버로 입력할 수 있으며, 이 경우 네트워크로 연결되지 않은 버전인 경우에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 복사본을 사용할 수 있습니다.|  
|UID|예|예|사용자 로그인 ID입니다.|  
|PWD|예|예(사용자에 따라 달라짐)|사용자가 지정한 암호입니다.|  
|APP|예|예|**SQLBrowseConnect**를 호출 하는 응용 프로그램의 이름입니다.|  
|WSID|예|예|워크스테이션 ID입니다. 일반적으로 애플리케이션이 실행되는 컴퓨터의 네트워크 이름입니다.|  
  
## <a name="level-3"></a>Level 3  
  
|키워드|목록 반환 여부|선택 사항 여부|Description|  
|-------------|--------------------|---------------|-----------------|  
|DATABASE|예|예|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 이름입니다.|  
|LANGUAGE|예|예|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 국가별 언어입니다.|  
  
 **SQLBrowseConnect** 는 ODBC 데이터 원본 정의에 저장 된 데이터베이스 및 언어 키워드의 값을 무시 합니다. **SQLBrowseConnect** 에 전달 된 연결 문자열에 지정 된 데이터베이스 또는 언어가 잘못 된 경우 **SQLBrowseConnect** 는 SQL_NEED_DATA 및 수준 3 연결 특성을 반환 합니다.  
  
 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)를 호출 하 여 설정 되는 다음 특성은 **SQLBrowseConnect**에서 반환 하는 결과 집합을 결정 합니다.  
  
|attribute|Description|  
|---------------|-----------------|  
|SQL_COPT_SS_BROWSE_CONNECT|SQL_MORE_INFO_YES로 설정 된 경우 **SQLBrowseConnect** 는 서버 속성의 확장 문자열을 반환 합니다.<br /><br /> 다음은 **SQLBrowseConnect**에 의해 반환 되는 확장 문자열의 예입니다.<br /><br /> <br /><br /> `ServerName\InstanceName;Clustered:No;Version:8.00.131`<br /><br /> <br /><br /> 이 문자열에서 세미콜론은 서버에 대한 다양한 정보 부분을 구분합니다. 서로 다른 서버 인스턴스를 구분하려면 쉼표를 사용합니다.|  
|SQL_COPT_SS_BROWSE_SERVER|서버 이름이 지정 된 경우 **SQLBrowseConnect** 는 지정 된 서버에 대 한 정보를 반환 합니다. SQL_COPT_SS_BROWSE_SERVER가 NULL로 설정 된 경우 **SQLBrowseConnect** 는 도메인에 있는 모든 서버에 대 한 정보를 반환 합니다.<br /><br /> <br /><br /> 네트워크 문제로 인해 **SQLBrowseConnect** 는 모든 서버에서 적시에 응답을 받지 못할 수 있습니다. 그러므로 반환되는 서버 목록은 각 요청이 있을 때마다 다를 수 있습니다.|  
|SQL_COPT_SS_BROWSE_CACHE_DATA|SQL_COPT_SS_BROWSE_CACHE_DATA 특성이 SQL_CACHE_DATA_YES로 설정되었을 때 버퍼 길이가 결과를 저장하기에 부족한 경우 데이터를 청크로 인출할 수 있습니다. 이 길이는 SQLBrowseConnect에 대 한 BufferLength 인수에 지정 됩니다.<br /><br /> 더 많은 데이터를 사용할 수 있을 때 SQL_NEED_DATA가 반환됩니다. 검색할 데이터가 더 없는 경우 SQL_SUCCESS가 반환됩니다.<br /><br /> 기본값은 SQL_CACHE_DATA_NO입니다.|  
  
## <a name="sqlbrowseconnect-support-for-high-availability-disaster-recovery"></a>고가용성 재해 복구를 위한 SQLBrowseConnect 지원  
 **SQLBrowseConnect** 를 사용 하 여 클러스터에 연결 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] [고가용성, 재해 복구를 위한 SQL Server Native Client 지원](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)을 참조 하세요.  
  
## <a name="sqlbrowseconnect-support-for-service-principal-names-spns"></a>SPN(서비스 사용자 이름)에 대한 SQLBrowseConnect 지원  
 연결이 열릴 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 및 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD를 연결을 여는 데 사용하는 인증 방법으로 설정합니다.  
  
 Spn에 대 한 자세한 내용은 [클라이언트 연결 &#40;ODBC&#41;에서 spn&#41; &#40;서비스 사용자 이름 ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)을 참조 하세요.  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|SQL_COPT_SS_BROWSE_CACHE_DATA에 대한 설명을 포함시켰습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQLBrowseConnect 함수](../../odbc/reference/syntax/sqlbrowseconnect-function.md)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
