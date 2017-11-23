---
title: OPENDATASOURCE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENDATASOURCE
- OPENDATASOURCE_TSQL
dev_langs: TSQL
helpviewer_keywords:
- data sources [SQL Server]
- OPENDATASOURCE function
- remote data access [SQL Server], OPENDATASOURCE
- ad hoc distributed queries
- OLE DB data sources [SQL Server]
- ad hoc connection information
ms.assetid: 5510b846-9cde-4687-8798-be9a273aad31
caps.latest.revision: "41"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e2ddb99a84c910c89aedaa086eb10e3f9de7abb9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="opendatasource-transact-sql"></a>OPENDATASOURCE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  연결된 서버 이름을 사용하지 않고 네 부분으로 된 개체 이름의 일부로 임시 연결 정보를 제공합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
OPENDATASOURCE ( provider_name, init_string )  
```  
  
## <a name="arguments"></a>인수  
 *provider_name*  
 데이터 원본에 액세스하는 데 사용하는 OLE DB 공급자의 PROGID로 등록된 이름입니다. *provider_name* 는 **char** 데이터 형식, 기본값은 없습니다.  
  
 *다음은 init_string*  
 대상 공급자의 IDataInitialize 인터페이스에 전달 된 연결 문자열입니다. 공급자 문자열 구문은 세미콜론으로 구분와 같은 키워드-값 쌍 기반: **'***keyword1*=*값***;** *keyword2*=*값***'**합니다.  
  
 공급자에서 지원되는 특정 키워드-값 쌍은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access SDK를 참조하십시오. 이 설명서에서는 기본 구문을 정의합니다. 다음 표에서 가장 자주 사용 되는 목록을 키워드는 *은 init_string* 인수입니다.  
  
|키워드|OLE DB 속성|유효한 값 및 설명|  
|-------------|---------------------|----------------------------------|  
|데이터 원본|DBPROP_INIT_DATASOURCE|연결할 데이터 원본의 이름입니다. 공급자마다 이 이름을 다른 방법으로 해석합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 경우 서버 이름을 나타냅니다. Jet OLE DB 공급자의 경우에는 .mdb 파일이나 .xls 파일의 전체 경로를 나타냅니다.|  
|위치|DBPROP_INIT_LOCATION|연결할 데이터베이스의 위치입니다.|  
|Extended Properties|DBPROP_INIT_PROVIDERSTRING|공급자별 연결 문자열입니다.|  
|Connect timeout|DBPROP_INIT_TIMEOUT|연결 시도가 실패한 후의 제한 시간 값입니다.|  
|사용자 ID|DBPROP_AUTH_USERID|연결에 사용할 사용자 ID입니다.|  
|암호|DBPROP_AUTH_PASSWORD|연결에 사용할 암호입니다.|  
|Catalog|DBPROP_INIT_CATALOG|데이터 원본에 연결할 때의 초기 또는 기본 카탈로그 이름입니다.|  
|Integrated Security|DBPROP_AUTH_INTEGRATED|Windows 인증을 지정하는 SSPI입니다.|  
  
## <a name="remarks"></a>주의  
 OPENDATASOURCE는 지정된 공급자에 대해 명시적으로 DisallowAdhocAccess 레지스트리 옵션을 0으로 설정하고 Ad Hoc Distributed Queries 고급 구성 옵션을 설정할 때만 OLE DB 데이터 원본에서 원격 데이터에 액세스하는 데 사용할 수 있습니다. 이러한 옵션을 설정하지 않은 경우 기본적으로 임시 액세스가 허용되지 않습니다.  
  
 OPENDATASOURCE 함수는 연결된 서버 이름과 동일한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문 위치에서 사용할 수 있습니다. 따라서 OPENDATASOURCE는 SELECT, INSERT, UPDATE 또는 DELETE 문에서 테이블이나 뷰 이름을 참조하거나 EXECUTE 문에서 원격 저장 프로시저를 참조하는 네 부분으로 된 이름의 첫 번째 부분으로 사용할 수 있습니다. 원격 저장 프로시저를 실행하는 경우 OPENDATASOURCE는 반드시 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 참조해야 합니다. OPENDATASOURCE는 변수를 인수로 받아들이지 않습니다.  
  
 OPENROWSET 함수처럼 OPENDATASOURCE도 자주 액세스되지 않는 OLE DB 데이터 원본만을 참조해야 합니다. 자주 액세스되는 데이터 원본에 대해서는 연결된 서버를 정의하십시오. OPENDATASOURCE와 OPENROWSET은 보안 관리 및 카탈로그 정보 쿼리 기능과 같은 연결된 서버 정의의 모든 기능을 제공하지 않습니다. OPENDATASOURCE가 호출될 때마다 암호를 포함하여 모든 연결 정보를 제공해야 합니다.  
  
> [!IMPORTANT]  
>  Windows 인증이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증보다 훨씬 더 안전하므로 가능하면 Windows 인증을 사용해야 합니다. OPENDATASOURCE는 연결 문자열에서 명시적 암호와 함께 사용하면 안 됩니다.  
  
 각 공급자에 대한 연결 요구 사항은 연결된 서버를 만들 때의 매개 변수에 대한 요구 사항과 비슷합니다. 여러 일반적인 공급자에 대 한 세부 정보는 항목에 나열 된 [sp_addlinkedserver &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
 FROM 절에서 OPENDATASOURCE, OPENQUERY 또는 OPENROWSET에 대한 모든 호출은 두 호출에 동일한 인수가 제공되는 경우에도 업데이트의 대상으로 사용되는 함수에 대한 호출과는 개별적이고 독립적으로 평가됩니다. 특히 이러한 호출 중 하나의 결과에 적용되는 필터 또는 조인 조건은 다른 호출의 결과에 영향을 미치지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 모든 사용자가 OPENDATASOURCE를 실행할 수 있습니다. 원격 서버 연결에 사용되는 사용 권한은 연결 문자열에서 결정됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Payroll` 서버에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 `London` 인스턴스에 대해 임시 연결을 만들고 `AdventureWorks2012.HumanResources.Employee` 테이블을 쿼리합니다. SQLNCLI를 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자로 리디렉션됩니다.  
  
```  
SELECT *  
FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source=London\Payroll;Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Employee  
```  
  
 다음 예에서는 1997 - 2003 형식의 Excel 스프레드시트에 대한 임시 연결을 만듭니다.  
  
```  
SELECT * FROM OPENDATASOURCE('Microsoft.Jet.OLEDB.4.0',  
'Data Source=C:\DataFolder\Documents\TestExcel.xls;Extended Properties=EXCEL 5.0')...[Sheet1$] ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
  
