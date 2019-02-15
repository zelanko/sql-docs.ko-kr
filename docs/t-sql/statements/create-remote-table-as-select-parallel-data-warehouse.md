---
title: CREATE REMOTE TABLE AS SELECT(병렬 데이터 웨어하우스) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.service: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 16ef8191-7587-45a3-9ee9-7d99b7088de3
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bc410f1a3c232eaed8f5f64603c95581361476c4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024684"
---
# <a name="create-remote-table-as-select-parallel-data-warehouse"></a>CREATE REMOTE TABLE AS SELECT(병렬 데이터 웨어하우스)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스에서 데이터를 선택하고 해당 데이터를 원격 서버의 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 있는 새 테이블로 복사합니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 MPP 쿼리 프로세스의 모든 이점을 갖는 어플라이언스를 사용하여 원격 복사본에 대한 데이터를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능이 필요한 시나리오에 이를 사용합니다.  
  
 원격 서버를 구성하려면 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]의 “원격 테이블 복사”를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙&#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE REMOTE TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name     AT ('<connection_string>')  
    [ WITH ( BATCH_SIZE = batch_size ) ]  
    AS <select_statement>  
[;]  
  
<connection_string> ::=   
    Data Source = { IP_address | hostname } [, port ]; User ID = user_name ;Password = password;  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 원격 테이블을 만들 데이터베이스입니다. *database_name*은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다. 기본값은 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 사용자 로그인에 대한 기본 데이터베이스입니다.  
  
 *schema_name*  
 새 테이블의 스키마입니다. 기본값은 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 사용자 로그인에 대한 기본 스키마입니다.  
  
 *table_name*  
 새 테이블의 이름입니다. 허용된 테이블 이름에 대한 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]의 “개체 이름 지정 규칙”을 참조하세요.  
  
 원격 테이블은 힙으로 생성됩니다. CHECK 제약 조건 또는 트리거가 없습니다. 원격 테이블 열의 데이터 정렬은 원본 테이블 열의 데이터 정렬과 같습니다. 이는 **char**, **nchar**, **varchar** 및 **nvarchar** 형식의 열에 적용됩니다.  
  
 *connection_string*  
 원격 서버 및 데이터베이스에 연결하기 위해 `Data Source`, `User ID` 및 `Password` 매개 변수를 지정하는 문자열입니다.  
  
 연결 문자열은 세미콜론으로 구분된 키 및 값 쌍입니다. 키워드는 대/소문자를 구분하지 않습니다. 키 및 값 쌍 간의 공백은 무시됩니다. 그러나 값은 데이터 원본에 따라 대/소문자를 구분할 수 있습니다.  
  
 *데이터 원본*  
 이름이나 IP 주소 및 원격 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 TCP 포트 번호를 지정하는 매개 변수입니다.  
  
 *hostname* 또는 *IP_address*  
 원격 서버 컴퓨터의 이름 또는 원격 서버의 IPv4 주소입니다. IPv6 주소는 지원되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명명된 인스턴스를 **Computer_Name\Instance_Name** 또는 **IP_address\Instance_Name** 형식으로 지정할 수 있습니다. 서버는 원격이어야 하되 (local)로 지정할 수 없습니다.  
  
 TCP *port* 번호  
 연결에 사용되는 TCP 포트 번호입니다. 기본 포트 1433에서 수신 대기하지 않는 SQL Server의 인스턴스에 대한 TCP 포트 번호를 0에서 65535 사이로 지정할 수 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다. **ServerA,1450** 또는 **10.192.14.27,1435**  
  
> [!NOTE]  
>  IP 주소를 사용하여 원격 서버에 연결하는 것이 좋습니다. 네트워크 구성에 따라 컴퓨터 이름을 사용하여 연결할 때는 비 어플라이언스 DNS 서버를 사용하여 올바른 서버에 대한 이름을 확인하는 추가 단계가 필요할 수 있습니다. IP 주소를 사용하여 연결하는 경우에는 이 단계가 필요하지 않습니다. 자세한 내용은 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]의 “DNS 전달자를 사용하여 비 어플라이언스 DNS 이름 확인(분석 플랫폼 시스템)”을 참조하세요.  
  
 *user_name*  
 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인 이름입니다. 최대 문자 수는 128자입니다.  
  
 *password*  
 로그인 암호입니다. 최대 문자 수는 128자입니다.  
  
 *batch_size*  
 일괄 처리당 최대 행 수입니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 대상 서버에 일괄 처리의 행을 보냅니다. *Batch_size*는 0보다 크거나 같은 양의 정수입니다. 기본값은 0입니다.  
  
 WITH *common_table_expression*  
 CTE(공통 테이블 식)라고도 하는 임시로 이름이 지정된 결과 집합을 지정합니다. 자세한 내용은 [WITH common_table_expression&#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)을 참조하세요.  
  
 SELECT \<select_criteria> 새 원격 테이블을 채울 데이터를 지정하는 쿼리 조건자입니다. SELECT 문에 대한 자세한 내용은 [SELECT&#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)를 참조하세요.  
  
## <a name="permissions"></a>Permissions  
 다음이 필요합니다.  
  
-   SELECT 절에 있는 각 개체에 대한 SELECT 권한이 필요합니다.  
  
-   대상 SMP 데이터베이스에 대한 CREATE TABLE 권한이 필요합니다.  
  
-   대상 SMP 스키마에 대한 ALTER, INSERT 및 SELECT 권한이 필요합니다.  
  
## <a name="error-handling"></a>오류 처리  
 원격 데이터베이스로의 데이터 복사에 실패할 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 작업을 중단하고 오류를 기록하며 원격 테이블 삭제를 시도합니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]는 새 테이블의 성공적인 정리를 보장하지 않습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 **원격 대상 서버**:  
  
-   TCP는 원격 서버로 연결하기 위한 기본적이며 유일하게 지원되는 프로토콜입니다.  
  
-   대상 서버는 비 어플라이언스 서버여야 합니다. CREATE REMOTE TABLE은 하나의 어플라이언스에서 다른 곳으로 데이터를 복사하는 데 사용할 수 없습니다.  
  
-   CREATE REMOTE TABLE 문은 새 테이블을 만들기만 수행합니다. 따라서 새 테이블이 처음부터 존재할 수는 없습니다. 원격 데이터베이스와 스키마는 이미 존재해야 합니다.  
  
-   원격 서버에는 어플라이언스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원격 데이터베이스로 전송되는 데이터를 저장할 수 있는 공간이 있어야 합니다.  
  
 **SELECT 문**:  
  
-   선택 조건에서 ORDER BY 및 TOP 절은 지원되지 않습니다.  
  
-   활성화된 트랜잭션 내부 또는 AUTOCOMMIT OFF 설정이 세션에 대해 활성화된 경우에는 CREATE REMOTE TABLE을 실행할 수 없습니다.  
  
 [SET ROWCOUNT&#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md)는 이 문에서 작동하지 않습니다. 비슷한 동작을 얻으려면 [TOP&#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md)를 사용합니다.  
  
## <a name="locking-behavior"></a>잠금 동작  
 원격 테이블을 만든 후에 복사가 시작될 때까지 대상 테이블은 잠겨 있지 않습니다. 따라서 원격 테이블을 만든 후와 복사를 시작하기 전에는 다른 프로세스가 원격 테이블을 삭제할 수 있습니다. 이 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]에서 오류를 생성하고 복사가 실패합니다.  
  
## <a name="metadata"></a>메타데이터  
 [sys.dm_pdw_dms_workers&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)를 사용하여 원격 SMP 서버로 선택한 데이터 복사의 진행률을 확인합니다. PARALLEL_COPY_READER 형식의 행에 이 정보가 포함됩니다.  
  
## <a name="security"></a>보안  
 CREATE REMOTE TABLE은 Windows 인증을 사용하지 않고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 외부 연결 네트워크에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 포트, 관리(administrative) 포트 및 관리(management) 포트 외에 방화벽을 사용해야 합니다.  
  
 실수로 인한 데이터 손실 또는 손상을 방지하려면 어플라이언스에서 대상 데이터베이스로 복사하는 데 사용되는 사용자 계정은 대상 데이터베이스에 대한 최소한의 필요 권한만 가져야 합니다.  
  
 연결 설정을 사용하면 SSL로 보호되는 사용자 이름 및 암호 데이터로(단, 일반 텍스트로 암호화되지 않고 전송되는 실제 데이터와 함께) SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있습니다. 이 경우 악의적인 사용자가 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 로그인하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 이름 및 암호가 포함된 CREATE REMOTE TABLE 문 텍스트를 가로챌 수 있습니다. 이러한 위험을 방지하려면 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결에서 데이터 암호화를 사용합니다.  
  
##  <a name="Examples"></a> 예  
  
### <a name="a-creating-a-remote-table"></a>1. 원격 테이블 만들기  
 이 예제에서는 데이터베이스 `OrderReporting` 및 스키마 `Orders`에 대해 `MyOrdersTable`라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP 원격 테이블을 만듭니다. `OrderReporting` 데이터베이스는 기본 포트 1433에서 수신하는 `SQLA`라는 서버에 있습니다. 서버에 대한 연결에는 암호가 `e4n8@3`인 사용자 `David`의 자격 증명을 사용합니다.  
  
```  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
AS SELECT <select_criteria>;  
```  
  
### <a name="b-querying-the-sysdmpdwdmsworkers-dmv-for-remote-table-copy-status"></a>2. 원격 테이블 복사 상태에 대해 sys.dm_pdw_dms_workers DMV 쿼리  
 이 쿼리는 원격 테이블 복사본에 대한 복사 상태를 확인하는 방법을 보여 줍니다.  
  
```  
SELECT * FROM sys.dm_pdw_dms_workers   
WHERE type = 'PARALLEL_COPY_READER';  
```  
  
### <a name="c-using-a-query-join-hint-with-create-remote-table"></a>C. CREATE REMOTE TABLE로 쿼리 조인 힌트 사용  
 이 쿼리는 CREATE REMOTE TABLE 문에 쿼리 조인 힌트를 사용하는 기본 구문을 보여 줍니다. 쿼리가 제어 노드에 제출된 후 계산 노드에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 계획을 생성할 때 해시 조인 전략을 적용합니다. 조인 힌트 및 OPTION 절을 사용하는 방법에 대한 자세한 내용은 [OPTION 절&#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md)을 참조하세요.  
  
```  
USE ssawPDW;  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
    AS SELECT T1.* FROM OrderReporting.Orders.MyOrdersTable T1   
    JOIN OrderReporting.Order.Customer T2  
    ON T1.CustomerID=T2.CustomerID OPTION (HASH JOIN);  
```  
  
  

