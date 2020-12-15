---
description: OPENDATASOURCE(Transact-SQL)
title: OPENDATASOURCE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/26/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- OPENDATASOURCE
- OPENDATASOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENDATASOURCE function
- remote data access [SQL Server], OPENDATASOURCE
- ad hoc distributed queries
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: 5510b846-9cde-4687-8798-be9a273aad31
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017
ms.openlocfilehash: 2e1245ccb29d0fd7982c62ff22ba7776b0bac839
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97402168"
---
# <a name="opendatasource-transact-sql"></a>OPENDATASOURCE(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  연결된 서버 이름을 사용하지 않고 네 부분으로 된 개체 이름의 일부로 임시 연결 정보를 제공합니다.  

 ![링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
OPENDATASOURCE ( 'provider_name', 'init_string' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 '*provider_name*'  
 데이터 원본에 액세스하는 데 사용하는 OLE DB 공급자의 PROGID로 등록된 이름입니다. *provider_name* 은 기본값이 없는 **char** 데이터 형식입니다.  

 > [!IMPORTANT]
 > 이전의 Microsoft OLE DB Provider for SQL Server(SQLOLEDB) 및 SQL Server Native Client OLE DB 공급자(SQLNCLI)는 계속 사용되지 않으며, 새로운 개발 작업에 사용하지 않는 것이 좋습니다. 대신 최신 서버 기능으로 업데이트되는 새로운 [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md)(MSOLEDBSQL)를 사용하세요.
 
 '*init_string*'  
 대상 공급자의 IDataInitialize 인터페이스로 전달되는 연결 문자열입니다. 공급자 문자열 구문은 세미콜론으로 구분된 키워드-값 쌍으로 구분됩니다(예: **‘** _keyword1_=_value_ **;** _keyword2_=_value_ **’** ).  
  
 공급자에서 지원되는 특정 키워드-값 쌍은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access SDK를 참조하십시오. 이 설명서에서는 기본 구문을 정의합니다. 다음 표에서는 *init_string* 인수에 가장 자주 사용되는 키워드를 나열합니다.  
  
|키워드|OLE DB 속성|유효한 값 및 설명|  
|-------------|---------------------|----------------------------------|  
|데이터 원본|DBPROP_INIT_DATASOURCE|연결할 데이터 원본의 이름입니다. 공급자마다 이 이름을 다른 방법으로 해석합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 경우 서버 이름을 나타냅니다. Jet OLE DB 공급자의 경우에는 .mdb 파일이나 .xls 파일의 전체 경로를 나타냅니다.|  
|위치|DBPROP_INIT_LOCATION|연결할 데이터베이스의 위치입니다.|  
|Extended Properties|DBPROP_INIT_PROVIDERSTRING|공급자별 연결 문자열입니다.|  
|Connect timeout|DBPROP_INIT_TIMEOUT|연결 시도가 실패한 후의 제한 시간 값입니다.|  
|사용자 ID|DBPROP_AUTH_USERID|연결에 사용할 사용자 ID입니다.|  
|암호|DBPROP_AUTH_PASSWORD|연결에 사용할 암호입니다.|  
|카탈로그|DBPROP_INIT_CATALOG|데이터 원본에 연결할 때의 초기 또는 기본 카탈로그 이름입니다.|  
|Integrated Security|DBPROP_AUTH_INTEGRATED|Windows 인증을 지정하는 SSPI입니다.|  
  
## <a name="remarks"></a>설명  
`OPENROWSET`는 열에 대한 데이터 정렬 세트에 관계없이 항상 인스턴스 데이터 정렬을 상속합니다.

`OPENDATASOURCE`는 지정된 공급자에 대해 명시적으로 DisallowAdhocAccess 레지스트리 옵션을 0으로 설정하고 Ad Hoc Distributed Queries 고급 구성 옵션을 설정할 때만 OLE DB 데이터 원본에서 원격 데이터에 액세스하는 데 사용할 수 있습니다. 이러한 옵션을 설정하지 않은 경우 기본적으로 임시 액세스가 허용되지 않습니다.  
  
`OPENDATASOURCE` 함수는 연결된 서버 이름과 동일한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문 위치에서 사용할 수 있습니다. 따라서 `OPENDATASOURCE`는 SELECT, INSERT, UPDATE 또는 DELETE 문에서 테이블이나 뷰 이름을 참조하거나 EXECUTE 문에서 원격 저장 프로시저를 참조하는 네 부분으로 된 이름의 첫 번째 부분으로 사용할 수 있습니다. 원격 저장 프로시저를 실행하는 경우 `OPENDATASOURCE`는 반드시 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 참조해야 합니다. OPENDATASOURCE는 변수를 인수로 받아들이지 않습니다.  
  
`OPENROWSET` 함수처럼 `OPENDATASOURCE`도 자주 액세스되지 않는 OLE DB 데이터 원본만을 참조해야 합니다. 자주 액세스되는 데이터 원본에 대해서는 연결된 서버를 정의하십시오. OPENDATASOURCE와 OPENROWSET은 보안 관리 및 카탈로그 정보 쿼리 기능과 같은 연결된 서버 정의의 모든 기능을 제공하지 않습니다. OPENDATASOURCE가 호출될 때마다 암호를 포함하여 모든 연결 정보를 제공해야 합니다.  
  
> [!IMPORTANT]  
> Windows 인증이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증보다 훨씬 더 안전하므로 가능하면 Windows 인증을 사용해야 합니다. `OPENDATASOURCE`는 연결 문자열에서 명시적 암호와 함께 사용하면 안 됩니다.  
  
각 공급자에 대한 연결 요구 사항은 연결된 서버를 만들 때의 매개 변수에 대한 요구 사항과 비슷합니다. 여러 일반적인 공급자에 대한 자세한 내용은 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 문서를 참조하세요.  
  
`FROM` 절에서 `OPENDATASOURCE`, `OPENQUERY` 또는 `OPENROWSET`에 대한 모든 호출은 두 호출에 동일한 인수가 제공되는 경우에도 업데이트의 대상으로 사용되는 함수에 대한 호출과는 개별적이고 독립적으로 평가됩니다. 특히 이러한 호출 중 하나의 결과에 적용되는 필터 또는 조인 조건은 다른 호출의 결과에 영향을 미치지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 모든 사용자가 OPENDATASOURCE를 실행할 수 있습니다. 원격 서버 연결에 사용되는 사용 권한은 연결 문자열에서 결정됩니다.  
  
## <a name="examples"></a>예제  

### <a name="a-using-opendatasource-with-select-and-the-sql-server-ole-db-driver"></a>A. SELECT 및 SQL Server OLE DB Driver로 OPENDATASOURCE 사용하기  
 다음 예에서는 [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md)를 사용하여 `Seattle1` 원격 서버에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 `HumanResources.Department` 테이블에 액세스합니다. `SELECT` 문은 반환되는 행 집합을 정의하는 데 사용됩니다. 공급자 문자열에는 `Server` 및 `Trusted_Connection` 키워드가 포함됩니다. 이러한 키워드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB Driver가 인식합니다.  
  
```sql  
SELECT GroupName, Name, DepartmentID  
FROM OPENDATASOURCE('MSOLEDBSQL', 'Server=Seattle1;Database=AdventureWorks2016;TrustServerCertificate=Yes;Trusted_Connection=Yes;').HumanResources.Department  
ORDER BY GroupName, Name;  
``` 

### <a name="b-using-opendatasource-with-select-and-the-sql-server-ole-db-provider"></a>B. SELECT 및 SQL Server OLE DB 공급자로 OPENDATASOURCE 사용하기  
다음 예에서는 `Payroll` 서버에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 `London` 인스턴스에 대해 임시 연결을 만들고 `AdventureWorks2012.HumanResources.Employee` 테이블을 쿼리합니다. 

> [!NOTE] 
> SQLNCLI를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 최신 버전의 SQL Server Native Client OLE DB 공급자로 리디렉션됩니다. OLE DB 공급자는 지정한 PROGID와 함께 레지스트리에 등록됩니다. 

> [!IMPORTANT]  
> SQL Server Native Client OLE DB 공급자(SQLNCLI)는 사용 중단 상태로 유지되므로 새로운 개발 작업에 사용하지 않는 것이 좋습니다. 대신 최신 서버 기능으로 업데이트되는 새로운 [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md)(MSOLEDBSQL)를 사용하세요.
  
```sql  
SELECT *  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=London\Payroll;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Employee;  
```  

### <a name="c-using-the-microsoft-ole-db-provider-for-jet"></a>C. Microsoft OLE DB Provider for Jet 사용   
 다음 예에서는 1997 - 2003 형식의 Excel 스프레드시트에 대한 임시 연결을 만듭니다.  
  
```sql  
SELECT * FROM OPENDATASOURCE('Microsoft.Jet.OLEDB.4.0',  
    'Data Source=C:\DataFolder\Documents\TestExcel.xls;Extended Properties=EXCEL 5.0')...[Sheet1$] ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
