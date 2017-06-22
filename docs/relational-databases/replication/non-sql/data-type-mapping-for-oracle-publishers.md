---
title: "Oracle 게시자에 대한 데이터 형식 매핑 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: 6da0e4f4-f252-4b7e-ba60-d2e912aa278e
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6eb74ce4647046c91fa199c260abeb1ae1845f66
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="data-type-mapping-for-oracle-publishers"></a>Oracle 게시자에 대한 데이터 형식 매핑
  Oracle 데이터 형식 및 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식이 항상 정확히 일치하지는 않습니다. Oracle 테이블을 게시할 때 가능한 일치하는 데이터 형식이 자동으로 선택됩니다. 단일 데이터 형식 매핑이 명확하지 않으면 대체 데이터 형식 매핑이 제공됩니다. 대체 매핑을 선택하는 방법은 아래의 "대체 데이터 형식 매핑 지정" 섹션을 참조하십시오.  
  
 다음 표에서는 Oracle 게시자에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자로 데이터 이동 시 Oracle과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 간에 데이터 형식이 기본적으로 매핑되는 방법을 보여 줍니다. 대체 형식 열은 대체 매핑을 사용할 수 있는지 여부를 나타냅니다.  
  
|Oracle 데이터 형식|SQL Server 데이터 형식|대체 형식|  
|----------------------|--------------------------|------------------|  
|BFILE|VARBINARY(MAX)|예|  
|BLOB|VARBINARY(MAX)|예|  
|CHAR([1-2000])|CHAR([1-2000])|예|  
|CLOB|VARCHAR(MAX)|예|  
|DATE|DATETIME|예|  
|FLOAT|FLOAT|아니요|  
|FLOAT([1-53])|FLOAT([1-53])|아니요|  
|FLOAT([54-126])|FLOAT|아니요|  
|INT|NUMERIC(38)|예|  
|INTERVAL|DATETIME|예|  
|LONG|VARCHAR(MAX)|예|  
|LONG RAW|IMAGE|예|  
|NCHAR([1-1000])|NCHAR([1-1000])|아니요|  
|NCLOB|NVARCHAR(MAX)|예|  
|NUMBER|FLOAT|예|  
|NUMBER([1-38])|NUMERIC([1-38])|아니요|  
|NUMBER([0-38],[1-38])|NUMERIC([0-38],[1-38])|예|  
|NVARCHAR2([1-2000])|NVARCHAR([1-2000])|아니요|  
|RAW([1-2000])|VARBINARY([1-2000])|아니요|  
|REAL|FLOAT|아니요|  
|ROWID|CHAR(18)|아니요|  
|TIMESTAMP|DATETIME|예|  
|TIMESTAMP(0-7)|DATETIME|예|  
|TIMESTAMP(8-9)|DATETIME|예|  
|TIMESTAMP(0-7) WITH TIME ZONE|VARCHAR(37)|예|  
|TIMESTAMP(8-9) WITH TIME ZONE|VARCHAR(37)|아니요|  
|TIMESTAMP(0-7) WITH LOCAL TIME ZONE|VARCHAR(37)|예|  
|TIMESTAMP(8-9) WITH LOCAL TIME ZONE|VARCHAR(37)|아니요|  
|UROWID|CHAR(18)|아니요|  
|VARCHAR2([1-4000])|VARCHAR([1-4000])|예|  
  
## <a name="considerations-for-data-type-mapping"></a>데이터 형식 매핑에 대한 고려 사항  
 Oracle 데이터베이스에서 데이터를 복제할 때는 다음 데이터 형식 문제를 고려하십시오.  
  
### <a name="unsupported-data-types"></a>지원되지 않는 데이터 형식  
 다음 데이터 형식은 지원되지 않으므로 이러한 형식이 있는 열은 복제할 수 없습니다.  
  
-   개체 유형  
  
-   XML 유형  
  
-   Varrays  
  
-   중첩 테이블  
  
-   REF를 사용하는 열  
  
### <a name="the-date-data-type"></a>DATE 데이터 형식  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 날짜 범위는 1753 A.D. 9999 A.D.까지이지만 Oracle의 날짜 범위는 4712 B.C.에서 4712 A.D.까지입니다. DATE 형식 열에 SQL Server의 범위를 벗어나는 값이 있을 경우 이 열에 대해 대체 데이터 형식인 VARCHAR(19)를 선택합니다.  
  
### <a name="float-and-number-types"></a>FLOAT 및 NUMBER 형식  
 FLOAT 및 NUMBER 데이터 형식 매핑 중에 지정하는 전체 자릿수 및 소수 자릿수는 Oracle 데이터베이스에서 해당 데이터 형식을 사용하는 열에 지정된 전체 자릿수 및 소수 자릿수에 따라 달라집니다. 전체 자릿수는 숫자의 모든 자릿수이고 소수 자릿수는 숫자에서 소수점 오른쪽에 있는 자릿수입니다. 예를 들어 123.45의 전체 자릿수는 5이고 소수 자릿수는 2입니다.  
  
 Oracle에서는 NUMBER(4,5)처럼 전체 자릿수보다 큰 소수 자릿수로 숫자를 정의할 수 있지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 전체 자릿수가 소수 자릿수보다 크거나 같아야 합니다. 데이터가 잘리지 않도록 하기 위해 Oracle 게시자에서 소수 자릿수가 전체 자릿수보다 클 경우 데이터 형식이 매핑될 때 전체 자릿수가 소수 자릿수와 동일하게 설정됩니다.NUMBER(4,5)는 NUMERIC(5,5)로 매핑됩니다.  
  
> [!NOTE]  
>  NUMBER에 대한 소수 자릿수와 전체 자릿수를 지정하지 않으면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 기본적으로 최대 소수 자릿수(8)와 최대 전체 자릿수(38)를 사용합니다. 데이터를 복제할 때 더 나은 저장소를 사용하고 성능을 높이려면 Oracle에서 특정 소수 자릿수와 전체 자릿수를 설정하는 것이 좋습니다.  
  
### <a name="large-object-types"></a>큰 개체 유형  
 Oracle에서는 최대 4GB를 지원하지만 SQL Server에서는 최대 2GB를 지원합니다. 2GB 이상으로 복제된 데이터는 잘립니다.  
  
 Oracle 테이블에 BFILE 열이 포함되어 있는 경우에는 이 열의 데이터가 파일 시스템에 저장됩니다. 다음 구문을 사용하여 복제 관리 사용자 계정에 데이터가 저장되어 있는 디렉터리에 대한 액세스 권한을 부여해야 합니다.  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 큰 개체 유형에 대한 자세한 내용은 [Oracle 게시자에 대한 디자인 고려 사항 및 제한 사항](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)에서 "큰 개체에 대한 고려 사항" 섹션을 참조하세요.  
  
## <a name="specifying-alternative-data-type-mappings"></a>대체 데이터 형식 매핑 지정  
 일반적으로 기본 데이터 형식 매핑이 적합하지만 많은 Oracle 데이터 형식의 경우 기본값을 사용하지 않고 대체 매핑 집합에서 데이터 형식 매핑을 선택할 수 있습니다. 다음 두 가지 방법으로 대체 매핑을 지정할 수 있습니다.  
  
-   저장 프로시저나 새 게시 마법사를 사용하여 아티클별로 기본값을 덮어씁니다.  
  
-   저장 프로시저를 사용하여 이후의 모든 아티클에 대한 기본값을 전역으로 변경합니다. 기존 아티클에 대한 기본값은 변경되지 않습니다.  
  
 대체 데이터 형식 매핑을 지정하려면 [Specify Data Type Mappings for an Oracle Publisher](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle 게시자에 대한 디자인 고려 사항 및 제한 사항](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
