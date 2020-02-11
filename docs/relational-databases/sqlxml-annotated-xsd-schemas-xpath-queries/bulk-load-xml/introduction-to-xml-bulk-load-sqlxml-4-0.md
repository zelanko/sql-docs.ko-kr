---
title: XML 대량 로드 소개 (SQLXML)
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nontransacted XML Bulk Load operations
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
- transacted XML Bulk Load operations
- streaming XML data
ms.assetid: 38bd3cbd-65ef-4c23-9ef3-e70ecf6bb88a
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4116bef21a70e6de699046019fd404798826bf18
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75246743"
---
# <a name="introduction-to-xml-bulk-load-sqlxml-40"></a>XML 대량 로드 소개(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML 대량 로드는 반구조화된 XML 데이터를 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 로드할 수 있게 해주는 독립 실행형 COM 개체입니다.  
  
 INSERT 문과 OPENXML 함수를 사용하여 XML 데이터를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 삽입할 수 있습니다. 하지만 많은 양의 XML 데이터를 삽입해야 하는 경우 대량 로드 유틸리티가 더 나은 성능을 제공합니다.  
  
 XML 대량 로드 개체 모델의 Execute 메서드는 두 개의 매개 변수를 사용 합니다.  
  
-   주석이 추가된 XSD(XML 스키마 정의) 또는 XDR(XML-Data Reduced) 스키마. XML 대량 로드 유틸리티는 XML 데이터를 삽입할 SQL Server 테이블을 식별할 때 스키마에 지정된 주석과 이 매핑 스키마를 해석합니다.  
  
-   XML 문서 또는 문서 조각(문서 조각은 단일 최상위 요소가 없는 문서임). XML 대량 로드에서 읽을 수 있는 파일 이름이나 스트림을 지정할 수 있습니다.  
  
 XML 대량 로드는 매핑 스키마를 해석하고 XML 데이터를 삽입할 테이블을 식별합니다.  
  
 사용자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능에 대해 잘 알고 있다고 가정합니다.  
  
-   주석이 추가된 XSD 및 XDR 스키마. 주석이 추가 된 XSD 스키마에 대 한 자세한 내용은 주석이 추가 된 [Xsd 스키마 &#40;SQLXML 4.0&#41;를 ](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)참조 하세요. 주석이 추가 된 XDR 스키마에 대 한 자세한 내용은 [SQLXML 4.0&#41;에서 사용 되지 &#40;주석이 추가 된 Xdr 스키마 ](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)를 참조 하세요.  
  
-   
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] BULK INSERT 문, bcp 유틸리티와 같은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 대량 삽입 메커니즘. 자세한 내용은 [BULK INSERT &#40;transact-sql&#41;](../../../t-sql/statements/bulk-insert-transact-sql.md) 및 [bcp 유틸리티](../../../tools/bcp-utility.md)를 참조 하세요.  
  
## <a name="streaming-of-xml-data"></a>XML 데이터 스트리밍  
 원본 XML 문서가 클 수 있으므로 대량 로드 처리를 위해 전체 문서를 메모리로 읽어 오지는 않습니다. 대신 XML 대량 로드에서 XML 데이터를 스트림으로 해석하고 읽습니다. 유틸리티는 데이터를 읽는 동안 데이터베이스 테이블을 식별하고, XML 데이터 원본에서 적절한 레코드를 생성한 다음 삽입을 위해 해당 레코드를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 보냅니다.  
  
 예를 들어 다음 소스 XML 문서는 ** \<Customer>** 요소와 ** \<Order>** 자식 요소로 구성 됩니다.  
  
```  
<Customer ...>  
    <Order.../>  
    <Order .../>  
     ...  
</Customer>  
...  
```  
  
 XML 대량 로드는 ** \<Customer>** 요소를 읽으므로 customertable에 대 한 레코드를 생성 합니다. /Customer>끝 태그를 읽으면 XML 대량 로드에서 해당 레코드를의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]테이블에 삽입 합니다. ** \<** 마찬가지로 ** \<Order>** 요소를 읽는 경우 XML 대량 로드는 ordertable에 대 한 레코드를 생성 한 다음 ** \</order>** 끝 태그를 읽을 때 해당 레코드를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 삽입 합니다.  
  
## <a name="transacted-and-nontransacted-xml-bulk-load-operations"></a>트랜잭션 및 비트랜잭션 XML 대량 로드 작업  
 XML 대량 로드는 트랜잭션 또는 비트랜잭션 모드로 작동할 수 있습니다. 일반적으로 트랜잭션이 아닌 모드에서 대량 로드 하는 경우 (즉, 트랜잭션 속성이 FALSE로 설정 됨) 다음 조건 중 하나가 true 인 경우 성능이 최적화 됩니다.  
  
-   데이터를 대량 로드되는 테이블이 인덱스 없이 비어 있습니다.  
  
-   테이블에 데이터와 고유한 인덱스가 있습니다.  
  
 트랜잭션이 아닌 방법을 사용하면 대량 로드 프로세스에서 문제가 발생할 경우 부분 롤백은 발생할 수 있어도 롤백이 보장되지 않습니다. 트랜잭션이 아닌 대량 로드는 데이터베이스가 비어 있을 때 적합합니다. 따라서 문제가 발생할 경우 데이터베이스를 지우고 XML 대량 로드를 다시 시작할 수 있습니다.  
  
> [!NOTE]  
>  트랜잭션이 아닌 모드에서 XML 대량 로드는 기본 내부 트랜잭션을 사용하고 커밋합니다. Transaction 속성이 TRUE로 설정 된 경우 XML 대량 로드는이 트랜잭션에서 commit을 호출 하지 않습니다.  
  
 Transaction 속성이 TRUE로 설정 된 경우 XML 대량 로드는 매핑 스키마에서 식별 되는 각 테이블에 대해 하나씩 임시 파일을 만듭니다. XML 대량 로드는 먼저 원본 XML 문서의 레코드를 이러한 임시 파일에 저장합니다. 그런 다음 [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT 문이 파일에서 이러한 레코드를 검색하여 해당 테이블에 저장합니다. TempFilePath 속성을 사용 하 여 이러한 임시 파일의 위치를 지정할 수 있습니다. XML 대량 로드에 사용하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 계정에 이 경로에 대한 액세스 권한이 있어야 합니다. TempFilePath 속성이 지정 되지 않은 경우 TEMP 환경 변수에 지정 된 기본 파일 경로를 사용 하 여 임시 파일을 만듭니다.  
  
 Transaction 속성이 FALSE (기본 설정)로 설정 된 경우 XML 대량 로드는 OLE DB 인터페이스 IRowsetFastLoad를 사용 하 여 데이터를 대량 로드 합니다.  
  
 ConnectionString 속성이 연결 문자열을 설정 하 고 Transaction 속성이 TRUE로 설정 된 경우 XML 대량 로드는 자체 트랜잭션 컨텍스트에서 작동 합니다. 예를 들어 XML 대량 로드에서 해당 트랜잭션을 시작하고 필요에 따라 커밋 또는 롤백합니다.  
  
 ConnectionCommand 속성이 기존 연결 개체와의 연결을 설정 하 고 Transaction 속성이 TRUE로 설정 되 면, XML 대량 로드는 각각 성공 또는 실패 하는 경우 COMMIT 또는 ROLLBACK 문을 실행 하지 않습니다. 오류가 있으면 XML 대량 로드는 해당 오류 메시지를 반환합니다. COMMIT 또는 ROLLBACK 문의 사용 여부는 대량 로드를 시작한 클라이언트에 의해 결정됩니다. XML 대량 로드에 사용 되는 연결 개체는 ICommand 형식 이거나 ADO 명령 개체 여야 합니다.  
  
 SQLXML 4.0에서 ConnectionObject는 Transaction 속성이 FALSE로 설정 된 상태에서 사용할 수 없습니다. 전달 된 세션에서 두 개 이상의 IRowsetFastLoad 인터페이스를 열 수 없기 때문에 비 트랜잭션 모드는 ConnectionObject에서 지원 되지 않습니다.  
  
  
