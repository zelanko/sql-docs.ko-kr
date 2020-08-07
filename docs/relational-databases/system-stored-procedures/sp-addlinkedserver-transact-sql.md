---
title: sp_addlinkedserver (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlinkedserver_TSQL
- sp_addlinkedserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlinkedserver
ms.assetid: fed3adb0-4c15-4a1a-8acd-1b184aff558f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 401fd85dec1370f81845b77de6e078ea18269891
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823338"
---
# <a name="sp_addlinkedserver-transact-sql"></a>sp_addlinkedserver(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  연결된 서버를 만듭니다. 연결된 서버를 만들면 OLE DB 데이터 원본과 유형이 다른 분산 쿼리에 액세스할 수 있습니다. **Sp_addlinkedserver**를 사용 하 여 연결 된 서버를 만든 후에는이 서버에 대해 분산 쿼리를 실행할 수 있습니다. 연결된 서버를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 정의한 경우에는 원격 저장 프로시저를 실행할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_addlinkedserver [ @server= ] 'server' [ , [ @srvproduct= ] 'product_name' ]   
     [ , [ @provider= ] 'provider_name' ]  
     [ , [ @datasrc= ] 'data_source' ]   
     [ , [ @location= ] 'location' ]   
     [ , [ @provstr= ] 'provider_string' ]   
     [ , [ @catalog= ] 'catalog' ]   
```  
  
## <a name="arguments"></a>인수  
[ @server =] * \' 서버 \' *          
만들려고 하는 연결된 서버의 이름입니다. *server* 은 **sysname**이며 기본값은 없습니다.  
  
[ @srvproduct =] * \' product_name \' *          
연결된 서버로 추가할 OLE DB 데이터 원본의 제품 이름입니다. *product_name* 은 **nvarchar (** 128 **)** 이며 기본값은 NULL입니다. **SQL Server**경우 *provider_name*, *data_source*, *위치*, *provider_string*및 *카탈로그* 를 지정할 필요가 없습니다.  
  
[ @provider =] * \' provider_name \' *          
이 데이터 원본에 해당하는 OLE DB 공급자의 고유 PROGID(프로그래밍 ID)입니다. *provider_name* 은 현재 컴퓨터에 설치 된 지정 된 OLE DB 공급자에 대해 고유 해야 합니다. *provider_name* 은 **nvarchar (128)** 이며 기본값은 NULL입니다. 그러나 *provider_name* 생략 하면 SQLNCLI가 사용 됩니다. 

> [!NOTE]
> SQLNCLI를 사용 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자로 리디렉션됩니다. OLE DB 공급자는 지정한 PROGID와 함께 레지스트리에 등록됩니다.

> [!IMPORTANT] 
> 이전의 Microsoft OLE DB Provider for SQL Server(SQLOLEDB) 및 SQL Server Native Client OLE DB 공급자(SQLNCLI)는 계속 사용되지 않으며, 새로운 개발 작업에 사용하지 않는 것이 좋습니다. 대신 최신 서버 기능으로 업데이트되는 새로운 [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md)(MSOLEDBSQL)를 사용하세요.
  
[ @datasrc =] * \' data_source \' *          
 OLE DB 공급자가 해석하는 데이터 원본의 이름입니다. *data_source* 은 **nvarchar (** 4000 **)** 입니다. *data_source* 은 DBPROP_INIT_DATASOURCE 속성으로 전달 되어 OLE DB 공급자를 초기화 합니다.  
  
[ @location =] * \' 위치 \' *          
 OLE DB 공급자에 의해 해석된 데이터베이스의 위치입니다. *location* 은 **nvarchar (** 4000 **)** 이며 기본값은 NULL입니다. *위치* 는 DBPROP_INIT_LOCATION 속성으로 전달 되어 OLE DB 공급자를 초기화 합니다.  
  
[ @provstr =] * \' provider_string \' *          
 고유한 데이터 원본을 나타내는 OLE DB 공급자의 연결 문자열입니다. *provider_string* 은 **nvarchar (** 4000 **)** 이며 기본값은 NULL입니다. *provstr* 는 IDataInitialize에 전달 되거나 OLE DB 공급자를 초기화 하기 위해 DBPROP_INIT_PROVIDERSTRING 속성으로 설정 됩니다.  
  
 Native Client OLE DB 공급자에 대해 연결 된 서버를 만들 때 server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 키워드 as server =*servername*instancename을 사용 하 여 인스턴스를 지정 하 여 \\ *instancename* 의 특정 인스턴스를 지정할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *servername* 은가 실행 되는 컴퓨터의 이름이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 *instancename* 은 사용자가 연결 될 특정 인스턴스의 이름입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]
> 미러된 데이터베이스에 액세스하려면 연결 문자열이 데이터베이스 이름을 포함해야 합니다. 이 이름은 데이터 액세스 공급자의 장애 조치(Failover) 시도를 지원하는 데 필요합니다. ** \@ Provstr** 또는 ** \@ catalog** 매개 변수에 데이터베이스를 지정할 수 있습니다. 필요에 따라 연결 문자열이 장애 조치(Failover) 파트너 이름을 제공할 수도 있습니다.  
  
[ @catalog =] * \' 카탈로그 \' *       
 OLE DB 공급자에 연결할 때 사용되는 카탈로그입니다. *catalog* 는 **sysname**이며 기본값은 NULL입니다. *카탈로그* 는 DBPROP_INIT_CATALOG 속성으로 전달 되어 OLE DB 공급자를 초기화 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 연결된 서버를 정의한 경우 카탈로그는 연결된 서버가 매핑된 기본 데이터베이스를 참조합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 다음 표에서는 OLE DB를 통해 액세스할 수 있는 데이터 원본에 대해 연결된 서버를 설정하는 방법을 보여 줍니다. 특정 데이터 원본에 대해 여러 가지 방법을 사용하여 연결된 서버를 설정할 수 있습니다. 따라서 데이터 원본 유형에 대한 행이 여러 개 있을 수 있습니다. 또한이 표에서는 연결 된 서버를 설정 하는 데 사용할 **sp_addlinkedserver** 매개 변수 값을 보여 줍니다.  
  
|원격 OLE DB 데이터 원본|OLE DB 공급자|product_name|provider_name|data_source|위치|provider_string|카탈로그|  
|-------------------------------|---------------------|-------------------|--------------------|------------------|--------------|----------------------|-------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <sup>1</sup> (기본값)||||||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자||**SQLNCLI**|기본 인스턴스에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 네트워크 이름|||데이터베이스 이름(옵션)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자||**SQLNCLI**|*서버 이름* \\ *instancename* (특정 인스턴스의 경우)|||데이터베이스 이름(옵션)|  
|Oracle 버전 8 이상|Oracle Provider for OLE DB|임의의 값|**OraOLEDB.Oracle**|Oracle 데이터베이스의 별칭||||  
|Access/Jet|Microsoft OLE DB Provider for Jet|임의의 값|**Microsoft.Jet.OLEDB.4.0**|Jet 데이터베이스 파일의 전체 경로||||  
|ODBC 데이터 원본|ODBC용 Microsoft OLE DB 공급자|임의의 값|**MSDASQL**|ODBC 데이터 원본의 시스템 DSN||||  
|ODBC 데이터 원본|ODBC용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB 공급자|임의의 값|**MSDASQL**|||ODBC 연결 문자열||  
|파일 시스템|[!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Indexing Service|임의의 값|**MSIDXS**|인덱싱 서비스 카탈로그 이름||||  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 스프레드시트|[!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet|임의의 값|**Microsoft.Jet.OLEDB.4.0**|Excel 파일의 전체 경로||Excel 5.0||  
|IBM DB2 데이터베이스|[!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for DB2|임의의 값|**DB2OLEDB**|||[!INCLUDE[msCoName](../../includes/msconame-md.md)]OLE DB Provider FOR DB2 설명서를 참조 하세요.|DB2 데이터베이스의 카탈로그 이름|  
  
 <sup>1</sup> 연결 된 서버를 설정 하는이 방법은 연결 된 서버의 이름을 원격 인스턴스의 네트워크 이름과 동일 하 게 강제 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *Data_source* 를 사용 하 여 서버를 지정 합니다.  
  
 <sup>2</sup> "Any"는 제품 이름이 모든 이름일 수 있음을 나타냅니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자 이름이 지정 되지 않은 경우 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 이름으로이 지정 된 경우에 사용 되는 공급자입니다. 이 공급자의 이전 이름인 SQLOLEDB를 지정하더라도 카탈로그에 보관될 때는 SQLNCLI로 변경됩니다.  
  
 *Data_source*, *location*, *provider_string*및 *catalog* 매개 변수는 연결 된 서버가 가리키는 데이터베이스를 식별 합니다. 이러한 매개 변수 중 하나가 NULL이면 해당되는 OLE DB 초기화 속성이 설정되지 않습니다.  
  
 클러스터형 환경에서 OLE DB 데이터 원본을 가리키는 파일 이름을 지정할 때는 UNC(Universal Naming Convention) 이름이나 공유 드라이브를 사용하여 위치를 지정하십시오.  
  
 사용자 정의 트랜잭션 내에서는 **sp_addlinkedserver** 을 실행할 수 없습니다.  
  
> [!IMPORTANT]
> **Sp_addlinkedserver**를 사용 하 여 연결 된 서버를 만들면 모든 로컬 로그인에 대 한 기본 자체 매핑이 추가 됩니다. 비 공급자의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 된 로그인이 서비스 계정으로 공급자에 대 한 액세스 권한을 얻을 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이와 같은 경우 관리자는 `sp_droplinkedsrvlogin <linkedserver_name>, NULL`을 사용하여 전역 매핑을 제거해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 `sp_addlinkedserver`문에 `ALTER ANY LINKED SERVER` 권한이 필요 합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]( **새 연결 된 서버** 대화 상자는 고정 서버 역할의 멤버 자격이 필요한 방식으로 구현 됩니다 `sysadmin` .  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-microsoft-sql-server-ole-db-provider"></a>A. Microsoft SQL Server OLE DB 공급자 사용  
 다음 예에서는 `SEATTLESales`라는 연결된 서버를 만듭니다. 제품 이름은 `SQL Server`이고 공급자 이름은 사용하지 않았습니다.  
  
```sql  
USE master;  
GO  
EXEC sp_addlinkedserver   
   N'SEATTLESales',  
   N'SQL Server';  
GO  
```  

 다음 예에서는 `S1_instance1` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB 드라이버를 사용 하 여 인스턴스에 연결 된 서버를 만듭니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

```sql  
EXEC sp_addlinkedserver     
   @server=N'S1_instance1',   
   @srvproduct=N'',  
   @provider=N'MSOLEDBSQL',   
   @datasrc=N'S1\instance1';  
```  

 다음 예에서는 `S1_instance1` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용 하 여 인스턴스에 연결 된 서버를 만듭니다.  
 
> [!IMPORTANT] 
> SQL Server Native Client OLE DB 공급자(SQLNCLI)는 사용 중단 상태로 유지되므로 새로운 개발 작업에 사용하지 않는 것이 좋습니다. 대신 최신 서버 기능으로 업데이트되는 새로운 [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md)(MSOLEDBSQL)를 사용하세요.
  
```sql  
EXEC sp_addlinkedserver     
   @server=N'S1_instance1',   
   @srvproduct=N'',  
   @provider=N'SQLNCLI',   
   @datasrc=N'S1\instance1';  
```  
  
### <a name="b-using-the-microsoft-ole-db-provider-for-microsoft-access"></a>B. Microsoft OLE DB Provider for Microsoft Access 사용  
 Microsoft.Jet.OLEDB.4.0 공급자는 2002-2003 형식을 사용하는 Microsoft Access 데이터베이스에 연결합니다. 다음 예에서는 `SEATTLE Mktg`라는 연결된 서버를 만듭니다.  
  
> [!NOTE]  
> 이 예에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access와 Sample **northwind** 데이터베이스가 모두 설치 되어 있고 **northwind** 데이터베이스가 C:\Msoffice\Access\Samples.에 있는 것으로 가정 합니다.  
  
```sql  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Mktg',   
   @provider = N'Microsoft.Jet.OLEDB.4.0',   
   @srvproduct = N'OLE DB Provider for Jet',  
   @datasrc = N'C:\MSOffice\Access\Samples\Northwind.mdb';  
GO  
```  
  
 Microsoft.ACE.OLEDB.12.0 공급자는 2007 형식을 사용하는 Microsoft Access 데이터베이스에 연결합니다. 다음 예에서는 `SEATTLE Mktg`라는 연결된 서버를 만듭니다.  
  
> [!NOTE]  
> 이 예에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access와 Sample **northwind** 데이터베이스가 모두 설치 되어 있고 **northwind** 데이터베이스가 C:\Msoffice\Access\Samples.에 있는 것으로 가정 합니다.  
  
```sql  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Mktg',   
   @provider = N'Microsoft.ACE.OLEDB.12.0',   
   @srvproduct = N'OLE DB Provider for ACE',  
   @datasrc = N'C:\MSOffice\Access\Samples\Northwind.accdb';  
GO  
```  
  
### <a name="c-using-the-microsoft-ole-db-provider-for-odbc-with-the-data_source-parameter"></a>C. data_source 매개 변수와 함께 Microsoft OLE DB Provider for ODBC 사용  
 다음 예에서는 `SEATTLE Payroll` [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB PROVIDER for ODBC ( `MSDASQL` ) 및 *data_source* 매개 변수를 사용 하는 라는 연결 된 서버를 만듭니다.  
  
> [!NOTE]  
> 연결된 서버를 사용하려면 지정한 ODBC 데이터 원본 이름이 서버에서 시스템 DSN으로 정의되어 있어야 합니다.  
  
```sql  
EXEC sp_addlinkedserver   
   @server = N'SEATTLE Payroll',   
   @srvproduct = N'',  
   @provider = N'MSDASQL',   
   @datasrc = N'LocalServer';  
GO  
```  
  
### <a name="d-using-the-microsoft-ole-db-provider-for-excel-spreadsheet"></a>D. Excel 스프레드시트에서 Microsoft OLE DB 공급자 사용  
 Jet 용 OLE DB 공급자를 사용 하 여 1997-2003 형식의 Excel 스프레드시트에 액세스 하는 연결 된 서버 정의를 만들려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 먼저 선택할 excel 워크시트의 열과 행을 지정 하 여 excel에서 명명 된 범위를 만듭니다. 범위의 이름은 분산 쿼리에서 테이블 이름으로 참조할 수 있습니다.  
  
```sql  
EXEC sp_addlinkedserver 'ExcelSource',  
   'Jet 4.0',  
   'Microsoft.Jet.OLEDB.4.0',  
   'c:\MyData\DistExcl.xls',  
   NULL,  
   'Excel 5.0';  
GO  
```  
  
 Excel 스프레드시트의 데이터를 액세스하려면 셀 범위에 이름을 연결하십시오. 다음 쿼리를 사용하면 앞에서 설정한 연결된 서버를 통해 지정한 명명된 범위인 `SalesData`를 표 형태로 액세스할 수 있습니다.  
  
```sql  
SELECT *  
   FROM ExcelSource...SalesData;  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 원격 공유에 대한 액세스 권한을 갖는 도메인 계정에서 실행되는 경우에는 매핑된 드라이브 대신 UNC 경로를 사용할 수 있습니다.  
  
```sql  
EXEC sp_addlinkedserver 'ExcelShare',  
   'Jet 4.0',  
   'Microsoft.Jet.OLEDB.4.0',  
   '\\MyServer\MyShare\Spreadsheets\DistExcl.xls',  
   NULL,  
   'Excel 5.0';  
```  
  
 ACE 공급자를 사용하여 Excel 2007 형식의 Excel 스프레드시트에 연결하려면  
  
```sql  
EXEC sp_addlinkedserver @server = N'ExcelDataSource',   
@srvproduct=N'ExcelData', @provider=N'Microsoft.ACE.OLEDB.12.0',   
@datasrc=N'C:\DataFolder\People.xlsx',  
@provstr=N'EXCEL 12.0' ;  
  
```  
  
### <a name="e-using-the-microsoft-ole-db-provider-for-jet-to-access-a-text-file"></a>E. Microsoft OLE DB Provider for Jet을 사용하여 텍스트 파일 액세스  
 다음 예에서는 Access.mdb 파일의 테이블에서처럼 파일을 연결하지 않고 직접 텍스트 파일에 액세스하기 위해 연결된 서버를 만듭니다. 공급자는 `Microsoft.Jet.OLEDB.4.0`이고 공급자 문자열은 `Text`입니다.  
  
 데이터 원본은 텍스트 파일을 포함하는 디렉터리의 전체 경로 이름입니다. 텍스트 파일의 구조를 정의하는 Schema.ini 파일은 반드시 텍스트 파일과 동일한 디렉터리에 있어야 합니다. Schema.ini 파일을 만드는 방법은 Jet Database Engine 설명서를 참조하십시오.  
  
```sql  
--Create a linked server.  
EXEC sp_addlinkedserver txtsrv, N'Jet 4.0',   
   N'Microsoft.Jet.OLEDB.4.0',  
   N'c:\data\distqry',  
   NULL,  
   N'Text';  
GO  
  
--Set up login mappings.  
EXEC sp_addlinkedsrvlogin txtsrv, FALSE, Admin, NULL;  
GO  
  
--List the tables in the linked server.  
EXEC sp_tables_ex txtsrv;  
GO  
  
--Query one of the tables: file1#txt  
--using a four-part name.   
SELECT *   
FROM txtsrv...[file1#txt];  
```  
  
### <a name="f-using-the-microsoft-ole-db-provider-for-db2"></a>F. Microsoft OLE DB Provider for DB2 사용  
 다음 예에서는 `DB2`를 사용하는 `Microsoft OLE DB Provider for DB2`라는 연결된 서버를 만듭니다.  
  
```sql  
EXEC sp_addlinkedserver  
   @server=N'DB2',  
   @srvproduct=N'Microsoft OLE DB Provider for DB2',  
   @catalog=N'DB2',  
   @provider=N'DB2OLEDB',  
   @provstr=N'Initial Catalog=PUBS;  
       Data Source=DB2;  
       HostCCSID=1252;  
       Network Address=XYZ;  
       Network Port=50000;  
       Package Collection=admin;  
       Default Schema=admin;';  
```  
  
### <a name="g-add-a-sssdsfull-as-a-linked-server-for-use-with-distributed-queries-on-cloud-and-on-premises-databases"></a>G. [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]클라우드 및 온-프레미스 데이터베이스에서 분산 쿼리와 함께 사용할 연결 된 서버로를 추가 합니다.  
 을 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 연결 된 서버로 추가한 다음 온-프레미스 및 클라우드 데이터베이스를 포괄 하는 분산 쿼리와 함께 사용할 수 있습니다. 온-프레미스 회사 네트워크 및 Azure 클라우드를 포괄 하는 데이터베이스 하이브리드 솔루션에 대 한 구성 요소입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Box 제품에는 연결 된 서버로 정의 된 원격 원본 (비 데이터 원본의 데이터 포함)의 데이터와 로컬 데이터 원본의 데이터를 결합 하는 쿼리를 작성할 수 있는 분산 쿼리 기능이 포함 되어 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 모든 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (가상 마스터 제외)를 개별 연결 된 서버로 추가한 다음 데이터베이스 응용 프로그램에서 다른 데이터베이스로 직접 사용할 수 있습니다.  
  
 을 사용 하는 경우의 이점에는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 관리 효율성, 고가용성, 확장성, 친숙 한 개발 모델 작업, 관계형 데이터 모델 등이 있습니다. 데이터베이스 응용 프로그램의 요구 사항에 따라 클라우드에서 사용 하는 방법이 결정 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 됩니다. 모든 데이터를 한 번에 이동 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 하거나 데이터 중 일부를 점진적으로 이동 하 여 나머지 데이터를 온-프레미스로 유지할 수 있습니다. 이러한 하이브리드 데이터베이스 응용 프로그램의 경우 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 이제를 연결 된 서버로 추가할 수 있으며 데이터베이스 응용 프로그램은 분산 쿼리를 실행 하 여 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 및 온-프레미스 데이터 원본의 데이터를 결합할 수 있습니다.  
  
 다음은 분산 쿼리를 사용 하 여에 연결 하는 방법을 설명 하는 간단한 예제입니다 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] .  
  
```sql  
-- Configure the linked server  
-- Add one Azure SQL Database as Linked Server  
EXEC sp_addlinkedserver  
  @server='myLinkedServer', -- here you can specify the name of the linked server  
  @srvproduct='',       
  @provider='sqlncli', -- using SQL Server Native Client  
  @datasrc='myServer.database.windows.net',   -- add here your server name  
  @location='',  
  @provstr='',  
  @catalog='myDatabase'  -- add here your database name as initial catalog (you cannot connect to the master database)  

-- Add credentials and options to this linked server  
EXEC sp_addlinkedsrvlogin  
  @rmtsrvname = 'myLinkedServer',  
  @useself = 'false',  
  @rmtuser = 'myLogin',             -- add here your login on Azure DB  
  @rmtpassword = 'myPassword' -- add here your password on Azure DB  

EXEC sp_serveroption 'myLinkedServer', 'rpc out', true;  

-- Now you can use the linked server to execute 4-part queries  
-- You can create a new table in the Azure DB  
EXEC ('CREATE TABLE t1tutut2(col1 int not null CONSTRAINT PK_col1 PRIMARY KEY CLUSTERED (col1) )') at myLinkedServer  
-- Insert data from your local SQL Server  
EXEC ('INSERT INTO t1tutut2 VALUES(1),(2),(3)') at myLinkedServer  
  
-- Query the data using 4-part names  
SELECT * FROM myLinkedServer.myDatabase.dbo.myTable  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;분산 쿼리 저장 프로시저](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [Transact-sql&#41;sp_addserver &#40;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [Transact-sql&#41;sp_dropserver &#40;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [Transact-sql&#41;sp_serveroption &#40;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [Transact-sql&#41;sp_setnetname &#40;](../../relational-databases/system-stored-procedures/sp-setnetname-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
