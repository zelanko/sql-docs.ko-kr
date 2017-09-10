---
title: "원격 TABLE AS SELECT (병렬 데이터 웨어하우스) 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 16ef8191-7587-45a3-9ee9-7d99b7088de3
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a0318d108d6dfaaa374af9a1ab8a148ff960dfcd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-remote-table-as-select-parallel-data-warehouse"></a>원격 TABLE AS SELECT (병렬 데이터 웨어하우스) 만들기
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  데이터를 선택는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 데이터베이스 및 해당 데이터를 새 테이블에는 SMP 복사 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원격 서버의 데이터베이스입니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]MPP 쿼리 원격 복사본에 대 한 데이터를 선택 하려면 처리의 모든 이점을 어플라이언스로 사용 합니다. 이 사용 하 여 필요한 시나리오에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능입니다.  
  
 원격 서버를 구성 하려면 "원격 테이블 복사"의 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [TRANSACT-SQL 구문 표기 규칙 &#40; Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 에 원격 테이블을 만들려면 데이터베이스입니다. *a s e _* 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다. 기본값은 대상에 사용자 로그인에 대 한 기본 데이터베이스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.  
  
 *schema_name*  
 새 테이블에 대 한 스키마입니다. 기본값은 대상에 사용자 로그인에 대 한 기본 스키마 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.  
  
 *table_name*  
 새 테이블의 이름입니다. 자세한에 대 한 내용은의 "개체 이름 지정 규칙"를 참조 테이블 이름에 허용 되는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
 원격 테이블을 힙으로 생성 됩니다. Check 제약 조건 또는 트리거 없는지 않습니다. 원격 테이블 열의 데이터 정렬은 원본 테이블 열의 데이터 정렬은와 같습니다. 이 형식의 열에 적용 됩니다 **char**, **nchar**, **varchar**, 및 **nvarchar**합니다.  
  
 *connection_string*  
 문자열을 지정 하는 `Data Source`, `User ID`, 및 `Password` 원격 서버 및 데이터베이스에 연결 하기 위한 매개 변수입니다.  
  
 연결 문자열은 키 / 값 쌍의 세미콜론으로 구분 된 목록입니다. 키워드는 대/소문자 구분 하지 않습니다. 키 / 값 쌍 간의 공백은 무시 됩니다. 그러나 값은 대/소문자 구분, 데이터 원본에 따라 수 있습니다.  
  
 *데이터 원본*  
 매개 변수 이름 또는 IP 주소 및 TCP를 지정 하는 포트 번호에 대 한 원격 SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 *호스트 이름* 또는 *IP_address*  
 원격 서버의 IPv4 주소 또는 원격 서버 컴퓨터의 이름입니다. IPv6 주소가 지원 되지 않습니다. 지정할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명명 된 형식에서 인스턴스 **Computer_Name\Instance_Name** 또는 **IP_address\Instance_Name**합니다. 서버는 원격 팀 이어야 하 고 (local)으로 지정할 수 없습니다.  
  
 TCP *포트* 번호  
 연결에 대 한 TCP 포트 번호입니다. 기본 포트 1433에서 수신 대기 하지 않는 SQL Server의 인스턴스에 대 한 TCP 포트 번호를 0에서 65535 지정할 수 있습니다. 예를 들어: **ServerA, 1450** 또는 **10.192.14.27,1435**  
  
> [!NOTE]  
>  IP 주소를 사용 하 여 원격 서버에 연결 하는 것이 좋습니다. 네트워크 구성에 따라 컴퓨터 이름을 사용 하 여 연결에서 올바른 서버 이름을 확인 하 여 비 어플라이언스 DNS 서버를 사용 하도록 추가 단계가 필요할 수 있습니다. IP 주소를 사용 하 여 연결 하는 경우에이 단계가 필요 하지 않습니다. 자세한 내용은 "해결 비 어플라이언스 DNS 이름 (분석 플랫폼 시스템)에 DNS 전달자를 사용 하 여"의 참조는 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]합니다.  
  
 *user_name*  
 유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인 이름입니다. 최대 문자 수는 128 자입니다.  
  
 *암호*  
 로그인 암호입니다. 최대 문자 수는 128 자입니다.  
  
 *batch_size*  
 최대 일괄 처리당 행 수입니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]대상 서버에 일괄 처리의 행을 보냅니다. *Batch_size* 양의 정수가 > = 0. 기본값은 0입니다.  
  
 와 *common_table_expression*  
 CTE(공통 테이블 식)라고도 하는 임시로 이름이 지정된 결과 집합을 지정합니다. 자세한 내용은 참조 [common_table_expression &AMP; #40; Transact SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 선택 \<select_criteria > 새 원격 테이블을 채울 데이터를 지정 하는 쿼리 조건자입니다. SELECT 문에 대 한 자세한 내용은 참조 하십시오. [select&#40; Transact SQL &#41; ](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 이 필요합니다.  
  
-   SELECT 절에 있는 각 개체에 대 한 SELECT 권한  
  
-   SMP 대상 데이터베이스에서 CREATE TABLE 권한이 필요합니다.  
  
-   ALTER, INSERT 및 대상 SMP 스키마에 대 한 SELECT 권한이 필요합니다.  
  
## <a name="error-handling"></a>오류 처리  
 원격 데이터베이스에 데이터 복사에 실패할 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 작업 중단, 오류를 기록 및 원격 테이블을 삭제 하려고 합니다. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]새 테이블의 정리 성공이 보장 하지 않습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 **원격 대상 서버**:  
  
-   TCP는 기본 템플릿이 고만 원격 서버에 연결 하기 위한 프로토콜을 지원 합니다.  
  
-   대상 서버에는 비 어플라이언스 서버의 이어야 합니다. CREATE REMOTE TABLE 하나의 기기에서 데이터를 다른 위치로 복사를 사용할 수 없습니다.  
  
-   CREATE REMOTE TABLE 문에만 새 테이블을 만듭니다. 따라서 새 테이블이 이미 있을 수 없습니다. 원격 데이터베이스와 스키마 이미 있어야 합니다.  
  
-   원격 서버에 기기에서 전송 되는 데이터를 저장할 수 있는 공간이 있어야 합니다.는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원격 데이터베이스입니다.  
  
 **SELECT 문의**:  
  
-   선택 조건에는 ORDER BY 및 TOP 절은 지원 되지 않습니다.  
  
-   활성화 된 트랜잭션 내부 또는 세션에 대 한 자동 커밋 해제 옵션 활성화 된 경우 CREATE REMOTE TABLE는 실행할 수 없습니다.  
  
 [SET ROWCOUNT &#40; Transact SQL &#41; ](../../t-sql/statements/set-rowcount-transact-sql.md) 이 문에서 아무 효과가 없습니다. 비슷한 동작이 얻기 위해 사용 하 여 [top&#40; Transact SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
## <a name="locking-behavior"></a>잠금 동작  
 원격 테이블을 만든 후에 복사 시작 될 때까지 대상 테이블 잠겨 있지 않습니다. 없으므로,이 만든 후 및 복사를 시작 하기 전에 원격 테이블을 삭제 하는 다른 프로세스에 대 한 가능 합니다. 이 경우 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 에서 오류를 생성 하 고 복사가 실패 합니다.  
  
## <a name="metadata"></a>메타데이터  
 사용 하 여 [sys.dm_pdw_dms_workers &#40; Transact SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md) 원격 SMP 서버에 선택한 데이터를 복사 진행률을 볼 수 있습니다. 행 PARALLEL_COPY_READER 형식과이 정보를 포함 합니다.  
  
## <a name="security"></a>보안  
 CREATE REMOTE TABLE 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 원격 연결을 인증 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스이거나 Windows 인증을 사용 하지 않습니다.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 의 예외와 함께 외부 연결 네트워크에 방화벽 사용, 수 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 포트, 관리 포트 및 관리 포트입니다.  
  
 실수로 인 한 데이터 손실 또는 손상을 방지 하려면 대상 데이터베이스에 필요한 최소 권한만 기기에서 대상 데이터베이스로 복사 하는 데 사용 되는 사용자 계정에 게 있어야 합니다.  
  
 연결 설정을 사용 하면 SMP에 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 일반 텍스트로 암호화 되지 않은 전송 되는 실제 데이터 하면서도 사용자 이름 및 암호 데이터를 보호 하는 SSL을 사용 합니다. 악의적인 사용자가 포함 된 CREATE REMOTE TABLE 문 텍스트를 가로채어 이러한 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP에 로그온 하려면 사용자 이름 및 암호 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스. 이러한 위험을 방지 하려면 SMP에 대 한 연결에서 데이터 암호화를 사용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.  
  
##  <a name="Examples"></a> 예  
  
### <a name="a-creating-a-remote-table"></a>1. 원격 테이블 만들기  
 이 예제에서는 만듭니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 라는 SMP 원격 테이블 `MyOrdersTable` 데이터베이스 `OrderReporting` 및 스키마 `Orders`합니다. `OrderReporting` 이라는 서버에 데이터베이스가 `SQLA` 기본 포트 1433에서 수신 하는 합니다. 서버에 연결 하는 사용자의 자격 증명을 사용 하 여 `David`, 암호는 `e4n8@3`합니다.  
  
```  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
AS SELECT <select_criteria>;  
```  
  
### <a name="b-querying-the-sysdmpdwdmsworkers-dmv-for-remote-table-copy-status"></a>2. 원격 테이블 복사 상태에 대 한 sys.dm_pdw_dms_workers DMV를 쿼리합니다.  
 이 쿼리에서 원격 테이블 복사본에 대 한 복사 상태를 확인 하는 방법을 보여 줍니다.  
  
```  
SELECT * FROM sys.dm_pdw_dms_workers   
WHERE type = 'PARALLEL_COPY_READER';  
```  
  
### <a name="c-using-a-query-join-hint-with-create-remote-table"></a>3. CREATE REMOTE TABLE 쿼리 조인 힌트 사용  
 이 쿼리에서 쿼리 조인 힌트가 CREATE REMOTE TABLE을 사용 하기 위한 기본 구문을 보여 줍니다. 쿼리 제출 하는 제어 노드에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 계산 노드에서 실행을 적용 됩니다. 해시 조인 전략을 생성할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 계획. 조인 힌트와 OPTION 절을 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. [OPTION 절 &#40; Transact SQL &#41; ](../../t-sql/queries/option-clause-transact-sql.md).  
  
```  
USE ssawPDW;  
CREATE REMOTE TABLE OrderReporting.Orders.MyOrdersTable  
AT ( 'Data Source = SQLA, 1433; User ID = David; Password = e4n8@3;' )  
    AS SELECT T1.* FROM OrderReporting.Orders.MyOrdersTable T1   
    JOIN OrderReporting.Order.Customer T2  
    ON T1.CustomerID=T2.CustomerID OPTION (HASH JOIN);  
```  
  
  


