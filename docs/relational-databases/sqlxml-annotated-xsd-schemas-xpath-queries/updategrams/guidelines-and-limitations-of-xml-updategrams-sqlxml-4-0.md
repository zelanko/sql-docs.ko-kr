---
title: Updategrams의 지침 및 제한 사항 (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9eb717968b191bb7d80f5d68542178bf32734b00
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75241304"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>XML updategram에 대한 지침 및 제한 사항(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML updategram 사용 시 다음 사항에 유의하십시오.  
  
-   **>\<** ** \<>이전** 에 단일 쌍만 포함 하는 삽입 작업에 대해 updategram를 사용 하는 경우 ** \<이전>** 블록을 생략할 수 있습니다. 반대로 삭제 작업의 경우 ** \<after>** 블록을 생략할 수 있습니다.  
  
-   ** \<>이전** 에 updategram를 여러 개 사용 하 고 ** \<** ** \<** sync>태그에서>블록을 사용 하는 경우 ** \<>블록 이전** 및 ** \<>블록 뒤에는** 를 지정 하 여>** \<앞** ** \<에>쌍을** 형성 해야 합니다.  
  
-   Updategram의 업데이트는 XML 스키마에서 제공한 XML 뷰에 적용됩니다. 따라서 기본 매핑이 성공하려면 updategram에서 스키마 파일 이름을 지정하거나, 파일 이름을 지정하지 않을 경우 요소 및 특성 이름이 데이터베이스의 테이블 및 열 이름과 일치해야 합니다.  
  
-   SQLXML 4.0에서는 updategram의 모든 열 값이 제공된 스키마(XDR 또는 XSD)에서 명시적으로 매핑되어야 해당 자식 요소에 대한 XML 뷰를 만들 수 있습니다. 이 동작은 **sql: relationship** 주석에서 외래 키의 일부로 암시 된 경우 스키마에서 매핑되지 않은 열에 대 한 값을 허용 하는 이전 버전의 SQLXML과 다릅니다. 이 변경 사항은 기본 키 값이 자식 요소로 전파되는 것에는 영향을 주지 않습니다. SQLXML 4.0에서 이 동작은 자식 요소에 대해 값이 명시적으로 지정되지 않은 경우에도 수행됩니다.  
  
-   Updategram를 사용 하 여 이진 열 (예: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **image** 데이터 형식)의 데이터를 수정 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 경우에는 데이터 형식 (예: **sql: datatype = "image"**) 및 XML 데이터 형식 (예: **dt: type = "binhex"** 또는 **dt: type = "binbase64**)을 지정 해야 하는 매핑 스키마를 제공 해야 합니다. Updategram에 이진 열의 데이터를 지정 해야 합니다. 매핑 스키마에 지정 된 **sql: url 인코딩** 주석은 updategram에서 무시 됩니다.  
  
-   XSD 스키마를 작성할 때 **sql: relation** 또는 **sql: field** annotation에 지정 하는 값에 공백 문자 (예: "order details" 테이블 이름)와 같은 특수 문자가 포함 된 경우이 값을 대괄호로 묶어야 합니다 (예: "[order details]").  
  
-   Updategram을 사용할 때 체인 관계는 지원되지 않습니다. 예를 들어 테이블 A와 C가 테이블 B를 사용하는 체인 관계를 통해 연결된 경우 updategram을 실행하려고 하면 다음 오류가 발생합니다.  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     스키마와 updategram 모두 형식이 올바르고 다른 문제가 없더라도 체인 관계가 있으면 이 오류가 발생합니다.  
  
-   Updategrams은 업데이트 하는 동안 **이미지** 형식 데이터를 매개 변수로 전달 하는 것을 허용 하지 않습니다.  
  
-   Updategrams으로 작업할 때에 ** \<>** 는 **text/ntext** 및 images와 같은 BLOB (Binary large object) 형식을에서 사용 하면 안 됩니다 .이는 동시성 제어에 사용 하기 위해이를 포함 하기 때문입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 BLOB 형식 비교에 대한 제한으로 인해 문제가 발생할 수 있습니다. 예를 들어 LIKE 키워드는 **text** 데이터 형식의 열을 비교 하기 위해 WHERE 절에 사용 됩니다. 그러나 데이터 크기가 8K 보다 큰 BLOB 유형의 경우에는 비교가 실패 합니다.  
  
-   **Ntext** 데이터의 특수 문자는 BLOB 형식 비교에 대 한 제한 사항 때문에 SQLXML 4.0에 문제가 발생할 수 있습니다. 예를 들어 **ntext** 형식의 열에 대 한 동시성 검사에 사용 될 때 updategram의 ** \<before>** 블록에 "[Serializable]"을 사용 하면 다음과 같은 SQLOLEDB 오류 설명과 함께 실패 합니다.  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [Updategram 보안 고려 사항은 SQLXML 4.0&#41;&#40;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
