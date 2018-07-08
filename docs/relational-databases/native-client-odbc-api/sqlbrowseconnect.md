---
title: SQLBrowseConnect | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBrowseConnect function
ms.assetid: 57faf388-c7ca-4696-9845-34e0a10cc5f7
caps.latest.revision: 54
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 78c2b7b8c6da683da00e725dd31f1b80cb05c57d
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429343"
---
# <a name="sqlbrowseconnect"></a>SQLBrowseConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLBrowseConnect** 세 수준의 연결 정보로 분류할 수 있는 키워드를 사용 하 여 합니다. 다음 표에서는 각 키워드에 대해 유효한 값 목록의 반환 여부와 키워드가 선택 사항인지 여부를 보여 줍니다.  
  
## <a name="level-1"></a>수준 1  
  
|키워드|목록 반환 여부|선택 사항 여부|Description|  
|-------------|--------------------|---------------|-----------------|  
|DSN|해당 사항 없음|아니요|반환 된 데이터 원본의 이름을 **SQLDataSources**합니다. DRIVER 키워드가 사용되는 경우에는 DSN 키워드를 사용할 수 없습니다.|  
|DRIVER|해당 사항 없음|아니요|Microsoft® [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 이름은 {[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11}입니다. DSN 키워드가 사용되는 경우에는 DRIVER 키워드를 사용할 수 없습니다.|  
  
## <a name="level-2"></a>수준 2  
  
|키워드|목록 반환 여부|선택 사항 여부|Description|  
|-------------|--------------------|---------------|-----------------|  
|SERVER|예|아니요|데이터 원본이 있는 네트워크의 서버 이름입니다. "(로컬)"이란 용어를 서버로 입력할 수 있으며, 이 경우 네트워크로 연결되지 않은 버전인 경우에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 복사본을 사용할 수 있습니다.|  
|UID|아니요|예|사용자 로그인 ID입니다.|  
|PWD|아니요|예(사용자에 따라 달라짐)|사용자가 지정한 암호입니다.|  
|APP|아니요|예|응용 프로그램 호출의 이름을 **SQLBrowseConnect**합니다.|  
|WSID|아니요|예|워크스테이션 ID입니다. 일반적으로 응용 프로그램이 실행되는 컴퓨터의 네트워크 이름입니다.|  
  
## <a name="level-3"></a>수준 3  
  
|키워드|목록 반환 여부|선택 사항 여부|Description|  
|-------------|--------------------|---------------|-----------------|  
|DATABASE|예|예|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 이름입니다.|  
|LANGUAGE|예|예|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 국가별 언어입니다.|  
  
 **SQLBrowseConnect** ODBC 데이터 원본 정의에 저장 된 데이터베이스 및 언어 키워드는 변수의 값을 무시 합니다. 데이터베이스 또는 연결 문자열에 지정 된 언어에 전달 하는 경우 **SQLBrowseConnect** 올바르지 **SQLBrowseConnect** SQL_NEED_DATA 및 수준 3 연결 특성을 반환 합니다.  
  
 호출 하 여 설정 되는 다음 특성을 [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)에서 반환한 결과 집합을 결정 **SQLBrowseConnect**합니다.  
  
|attribute|Description|  
|---------------|-----------------|  
|SQL_COPT_SS_BROWSE_CONNECT|Sql_more_info_yes로 설정 되어 있으면 **SQLBrowseConnect** 서버 속성의 확장된 문자열을 반환 합니다.<br /><br /> 다음은에서 반환 하는 확장된 문자열의 예로 **SQLBrowseConnect**:<br /><br /> <br /><br /> `ServerName\InstanceName;Clustered:No;Version:8.00.131`<br /><br /> <br /><br /> 이 문자열에서 세미콜론은 서버에 대한 다양한 정보 부분을 구분합니다. 서로 다른 서버 인스턴스를 구분하려면 쉼표를 사용합니다.|  
|SQL_COPT_SS_BROWSE_SERVER|서버 이름이 지정 됩니다 **SQLBrowseConnect** 지정 된 서버에 대 한 정보를 반환 합니다. SQL_COPT_SS_BROWSE_SERVER가 NULL로 설정 된 경우 **SQLBrowseConnect** 도메인의 모든 서버에 대 한 정보를 반환 합니다.<br /><br /> <br /><br /> 네트워크 문제로 인해 유의 **SQLBrowseConnect** 모든 서버 로부터 시기 적절 하 게 응답을 받지 못할 수 있습니다. 그러므로 반환되는 서버 목록은 각 요청이 있을 때마다 다를 수 있습니다.|  
|SQL_COPT_SS_BROWSE_CACHE_DATA|SQL_COPT_SS_BROWSE_CACHE_DATA 특성이 SQL_CACHE_DATA_YES로 설정되었을 때 버퍼 길이가 결과를 저장하기에 부족한 경우 데이터를 청크로 인출할 수 있습니다. 이 길이 SQLBrowseConnect BufferLength 인수에 지정 됩니다.<br /><br /> 더 많은 데이터를 사용할 수 있을 때 SQL_NEED_DATA가 반환됩니다. 검색할 데이터가 더 없는 경우 SQL_SUCCESS가 반환됩니다.<br /><br /> 기본값은 SQL_CACHE_DATA_NO입니다.|  
  
## <a name="sqlbrowseconnect-support-for-high-availability-disaster-recovery"></a>고가용성 재해 복구를 위한 SQLBrowseConnect 지원  
 사용 하 여 대 한 자세한 내용은 **SQLBrowseConnect** 에 연결 하는 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 클러스터를 참조 하십시오 [SQL Server Native Client Support for High Availability, Disaster Recovery](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)합니다.  
  
## <a name="sqlbrowseconnect-support-for-service-principal-names-spns"></a>SPN(서비스 사용자 이름)에 대한 SQLBrowseConnect 지원  
 연결이 열릴 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 및 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD를 연결을 여는 데 사용하는 인증 방법으로 설정합니다.  
  
 Spn에 대 한 자세한 내용은 참조 하세요. [서비스 사용자 이름 &#40;Spn&#41; 클라이언트 연결의 &#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)합니다.  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|SQL_COPT_SS_BROWSE_CACHE_DATA에 대한 설명을 포함시켰습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SQLBrowseConnect 함수](http://go.microsoft.com/fwlink/?LinkId=59329)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
