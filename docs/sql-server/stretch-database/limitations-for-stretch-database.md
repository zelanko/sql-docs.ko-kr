---
title: Stretch Database에 대한 제한 사항 | Microsoft 문서
ms.date: 06/14/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, limitations
- Stretch Database, blocking issues
- limitations (Stretch Database)
- blocking issues (Stretch Database)
ms.assetid: 2b1fbec1-7859-44fc-8417-724fc57a59c0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 90e6bbd804d69af00d8e006d3ca363e09dacd8c3
ms.sourcegitcommit: ec1f01b4bb54621de62ee488decf9511d651d700
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56240767"
---
# <a name="limitations-for-stretch-database"></a>Stretch Database에 대한 제한 사항
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  스트레치 사용 데이터베이스와 관련된 제한 사항 및 현재 테이블에 스트레치를 사용할 수 없게 하는 제한 사항에 대해 알아봅니다.  
  
##  <a name="Caveats"></a> 스트레치 사용 테이블에 대한 제한 사항  
  
스트레치 사용 테이블에는 다음과 같은 제한 사항이 적용됩니다.  
  
### <a name="constraints"></a>제약 조건  
-   마이그레이션된 데이터를 포함하는 Azure 테이블의 UNIQUE 제약 조건 및 PRIMARY KEY 제약 조건에는 고유성이 적용되지 않습니다.  
  
### <a name="dml-operations"></a>DML 작업  
-   스트레치 사용 테이블이나 스트레치 사용 테이블을 포함하는 뷰에서는 마이그레이션된 행 또는 마이그레이션할 수 있는 행을 업데이트하거나 삭제할 수 없습니다.  
  
-   연결된 서버의 스트레치 사용 테이블에 행을 삽입할 수 없습니다.  
  
### <a name="indexes"></a>인덱스  
-   스트레치 사용 테이블을 포함하는 뷰에 대해서는 인덱스를 만들 수 없습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인덱스의 필터는 원격 테이블로 전파되지 않습니다.  
  
##  <a name="Limitations"></a> 현재 테이블에 스트레치를 사용할 수 없게 하는 제한 사항  
   
 현재 테이블에 스트레치를 사용할 수 없게 하는 항목은 다음과 같습니다.  
  
 ### <a name="table-properties"></a>테이블 속성  
-   1,023개 이상의 열 또는 998개 이상의 인덱스가 있는 테이블  
  
-   FILESTREAM 데이터를 포함하는 FileTable 또는 테이블  
  
-   복제되었거나 변경 추적 또는 변경 데이터 캡처를 사용 중인 테이블  
  
-   메모리 액세스에 최적화된 테이블  
  
### <a name="data-types"></a>데이터 형식  
-   text, ntext 및 image  
  
-   TIMESTAMP  
  
-   sql_variant  
  
-   XML  
  
-   geometry, geography, hierarchyid 및 CLR 사용자 정의 형식을 포함하는 CLR 데이터 형식  
  
 ### <a name="column-types"></a>열 유형  
 -   COLUMN_SET  
  
-   계산 열  
  
### <a name="constraints"></a>제약 조건  
-   DEFAULT 제약 조건 및 CHECK 제약 조건  
  
-   테이블을 참조하는 외래 키 제약 조건. 부모-자식 관계(예: Order 및 Order_Detail)에서 자식 테이블(Order_Detail)에는 스트레치를 사용하도록 설정할 수 있지만 부모 테이블(Order)에는 설정할 수 없습니다.  
  
### <a name="indexes"></a>인덱스  
-   전체 텍스트 인덱스  
  
-   XML 인덱스  
  
-   공간 인덱스  
  
-   테이블을 참조하는 인덱싱된 뷰  
  
## <a name="see-also"></a>참고 항목  
 [스트레치 데이터베이스 관리자를 실행하여 스트레치 데이터베이스용 데이터베이스 및 테이블 식별](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)   
 [데이터베이스에서 Stretch Database 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [테이블에서 스트레치 데이터베이스 활성화](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
