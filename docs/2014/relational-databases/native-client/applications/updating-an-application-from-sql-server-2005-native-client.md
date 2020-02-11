---
title: SQL Server 2005 Native Client에서 애플리케이션 업데이트 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, updating applications
ms.assetid: 1e1e570c-7f14-4e16-beab-c328e3fbdaa8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf12faa1dc32044c6dc40c048d463394d6841b2e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046488"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>SQL Server 2005 Native Client에서 애플리케이션 업데이트
  이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 이후에 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client에 대해 이루어진 주요 변경 사항을 설명합니다.  
  
 MDAC(Microsoft Data Access Components)에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client으로 업그레이드하는 경우에도 몇 가지 동작 차이점이 표시될 수 있습니다. 자세한 내용은 [MDAC에서 SQL Server Native Client 응용 프로그램 업데이트](updating-an-application-to-sql-server-native-client-from-mdac.md)를 참조 하세요.  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 함께 제공되는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 9.0. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 함께 제공되는 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 10.0.  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 함께 제공되는 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client 10.5. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]와 함께 제공되는 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client 11.0.  
  
|
  [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이후에 SQL Server Native Client에서 변경된 동작|Description|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB가 정의된 배율로만 패딩됩니다.|변환된 데이터가 서버로 전송되는 변환의 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]부터 해당)는 데이터의 후행 0을 `datetime` 값의 최대 길이까지만 패딩합니다. 9자리까지 패딩된 SQL Server Native Client 9.0입니다.|  
|ICommandWithParameter:: SetParameterInfo에 대 한 DBTYPE_DBTIMESTAMP 유효성을 검사 합니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client (부터 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)])는 DBTYPE_DBTIMESTAMP에 대 한 소수 자릿수 초의 소수 자릿수를 설정 하기 위해 ICommandWithParameter:: SetParameterInfo의 *bscale* 에 대 한 OLE DB 요구 사항을 구현 합니다.|  
|이제 `sp_columns` 저장 프로시저는 IS_NULLABLE 열에 대해 **"no** " 대신 **"no** "를 반환 합니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]()부터 저장 프로시저 `sp_columns` 는 이제 IS_NULLABLE 열에 대해 **"no** " 대신 **"no** "를 반환 합니다.|  
|SQLSetDescRec, SQLBindParameter 및 SQLBindCol는 이제 일관성 확인을 수행 합니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전에는 SQL_DESC_DATA_PTR를 설정 해도 SQLSetDescRec, SQLBindParameter 또는 SQLBindCol의 모든 설명자 형식에 대 한 일관성 확인이 수행 되지 않았습니다.|  
|이제 SQLCopyDesc에서 설명자 일관성 검사를 수행 합니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전에는 특정 레코드에 SQL_DESC_DATA_PTR 필드가 설정 된 경우 SQLCopyDesc에서 일관성 확인을 수행 하지 않았습니다.|  
|SQLGetDescRec는 더 이상 설명자 일관성 검사를 수행 하지 않습니다.|Native Client [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 10.0 이전에는 SQL_DESC_DATA_PTR 필드가 설정 되었을 때 SQLGetDescRec에서 설명자 일관성 검사를 수행 했습니다. ODBC 사양과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 이상 버전에서는 필요하지 않으므로 이 일관성 검사는 더 이상 수행되지 않습니다.|  
|데이터가 범위를 벗어날 때 서로 다른 오류가 반환되었습니다.|
  `datetime` 유형의 경우 범위를 벗어난 날짜에 대해 이전 버전에서 반환된 것과는 다른 오류 번호가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]부터 해당)에서 반환됩니다.<br /><br /> 구체적으로, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0에서는 `datetime`으로의 문자열 변환 시 범위를 벗어난 모든 연도 값에 대해 22007을 반환했지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 버전 10.0([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)])부터는 날짜가 `datetime2`에서 지원되는 범위 내에 있지만 `datetime` 또는 `smalldatetime`에서 지원되는 범위를 벗어날 때 22008을 반환합니다.|  
|반올림이 일을 변경하는 경우 `datetime` 값은 소수 자릿수 초를 자르고 반올림되지 않습니다.|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전에는 서버로 전송된 `datetime` 값에 대한 클라이언트 동작에 의해 값이 1초의 1/300에 가깝게 반올림됩니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0부터 이 시나리오를 사용하면 반올림으로 인해 일이 변경되는 경우 소수 자릿수 초가 잘립니다.|  
|
  `datetime` 값에서 초가 잘릴 수 있습니다.|
  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 이상 버전을 사용하여 빌드한 애플리케이션에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2005 서버에 연결할 경우 유형 식별자인 DBTYPE_DBTIMESTAMP(OLE DB) 또는 SQL_TIMESTAMP(ODBC) 및 소수 자릿수 0을 사용하여 datetime 열에 바인딩하면 서버에 전송된 시간 데이터 부분에서 초 및 초의 소수 자리 부분이 잘립니다.<br /><br /> 다음은 그 예입니다.<br /><br /> 입력 데이터: 1994-08-21 21:21:36.000<br /><br /> 삽입된 데이터: 1994-08-21 21:21:00.000|  
|DBTYPE_DBTIME에서 DBTYPE_DATE로 OLE DB 데이터 변환을 수행할 때 더 이상 일이 변경되지 않습니다.|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이전에는 DBTYPE_DATE의 시간 부분이 자정의 1/2초 내에 있는 경우 OLE DB 변환 코드로 인해 일이 변경되었습니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0부터 일이 변경되지 않습니다(소수 자릿수 초가 잘리고 반올림되지 않음).|  
|IBCPSession:: BCColFmt 변환 변경 내용입니다.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0부터 IBCPSession:: BCOColFmt를 사용 하 여 SQLDATETIME 또는 SQLDATETIME를 문자열 형식으로 변환 하는 경우 소수 값을 내보냅니다. 예를 들어 SQLDATETIME 유형을 SQLNVARCHARMAX 유형으로 변환할 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client의 이전 버전에서는 다음을 반환했습니다.<br /><br /> 1989-02-01 00:00:00. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이상 버전에서 1989-02-01 00:00:00.0000000을 반환합니다.|  
|전송된 데이터 크기가 SQL_LEN_DATA_AT_EXEC에 지정된 길이와 일치해야 합니다.|SQL_LEN_DATA_AT_EXEC를 사용하는 경우 데이터 크기가 SQL_LEN_DATA_AT_EXEC로 지정한 길이와 일치해야 합니다. SQL_DATA_AT_EXEC를 사용할 수도 있지만 SQL_LEN_DATA_AT_EXEC를 사용하면 성능이 향상됩니다.|  
|이제 BCP API를 사용하는 사용자 지정 애플리케이션에서 경고를 볼 수 있습니다.|데이터 길이가 모든 유형의 필드에 대해 지정된 길이보다 큰 경우 BCP API에서 경고 메시지를 생성합니다. 이전에는 이 경고가 문자 유형에 대해서만 제공되었으며 모든 유형에 대해 실행되지 않습니다.|  
|날짜/시간 유형으로 바인딩된 `sql_variant`에 빈 문자열을 삽입하면 오류가 생성됩니다.|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0에서는 날짜/시간 유형으로 바인딩된 `sql_variant`에 빈 문자열을 삽입해도 오류가 생성되지 않았습니다. 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 이상에서는 이 경우 올바르게 오류를 생성합니다.|  
|SQL_C_TYPE _TIMESTAMP 및 DBTYPE_DBTIMESTAMP 매개 변수 유효성 검사가 더 엄격해졌습니다.|[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 이전에는 `datetime` 값이 `datetime` 및 `smalldatetime` 열 크기에 맞게 반올림 되었습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 
  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 및 이후 버전에서는 소수 자릿수에 대한 ODBC 핵심 사양에 정의된 보다 엄격한 유효성 검사 규칙을 적용합니다. 후행 숫자의 잘림 없이 클라이언트 바인딩에 의해 지정 또는 암시된 소수 자릿수를 사용하여 매개 변수 값을 SQL 유형으로 변환할 수 없는 경우 오류가 반환됩니다.|  
|트리거가 실행될 때 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 다른 결과를 반환할 수 있습니다.|
  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]에서 변경된 사항으로 인해 `NOCOUNT OFF`가 적용될 때 트리거를 실행하는 문에서 다른 결과가 반환될 수도 있습니다. 이 경우 애플리케이션에서 오류가 발생할 수 있습니다. 이 오류를 해결 하려면 트리거에서 `NOCOUNT ON` 를 설정 하거나 SQLMoreResults를 호출 하 여 다음 결과로 이동 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 프로그래밍](../sql-server-native-client-programming.md)  
  
  
