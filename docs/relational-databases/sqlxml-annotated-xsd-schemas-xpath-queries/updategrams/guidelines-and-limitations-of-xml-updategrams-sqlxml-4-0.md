---
title: 지침 및 제한 사항 (SQLXML 4.0) XML Updategram의 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 08cd4c5cd8bf7aef6472cc46fb573816e7ce7b85
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>XML updategram에 대한 지침 및 제한 사항(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML updategram 사용 시 다음 사항에 유의하십시오.  
  
-   한 쌍의 포함 된 삽입 작업에 대 한 updategram을 사용 하는 경우  **\<하기 전에 >** 및  **\<후 >** 블록의  **\<하기 전에 >** 블록이 생략 될 수 있습니다. 반대로 삭제 작업을 발생 한 경우는  **\<후 >** 블록이 생략 될 수 있습니다.  
  
-   여러 개의 updategram을 사용 하는 경우  **\<하기 전에 >** 및  **\<후 >** 블록에  **\<동기화 >** 둘 다 태그  **\<하기 전에 >** 블록 및  **\<후 >** 블록 형식으로 지정 해야  **\<하기 전에 >** 및  **\<후 >** 쌍입니다.  
  
-   Updategram의 업데이트는 XML 스키마에서 제공한 XML 뷰에 적용됩니다. 따라서 기본 매핑이 성공하려면 updategram에서 스키마 파일 이름을 지정하거나, 파일 이름을 지정하지 않을 경우 요소 및 특성 이름이 데이터베이스의 테이블 및 열 이름과 일치해야 합니다.  
  
-   SQLXML 4.0에서는 updategram의 모든 열 값이 제공된 스키마(XDR 또는 XSD)에서 명시적으로 매핑되어야 해당 자식 요소에 대한 XML 뷰를 만들 수 있습니다. 이 동작은 이전 버전의 SQLXML의 외래 키의 일부로 포함 된 경우 스키마에서 매핑되지 않았다면 열에 대 한 값을 허용 하는 **sql: relationship** 주석입니다. 이 변경 사항은 기본 키 값이 자식 요소로 전파되는 것에는 영향을 주지 않습니다. SQLXML 4.0에서 이 동작은 자식 요소에 대해 값이 명시적으로 지정되지 않은 경우에도 수행됩니다.  
  
-   이진 열에 데이터를 수정 하는 updategram을 사용 하는 경우 (같은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **이미지** 데이터 형식)는 매핑 스키마를 제공 해야 합니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식 (예를 들어 **sql: datatype = "이미지"** ) 및 XML 데이터 형식 (예를 들어 **dt: type = "binhex"** 또는 **dt: type = "binbase64**)을 지정 해야 합니다. Updategram에서는 이진 열에 대 한 데이터를 지정 해야 합니다. **sql:url-인코딩할** updategram에서 매핑 스키마에 지정 된 주석은 무시 됩니다.  
  
-   작성할 때 XSD 스키마에 대 한 지정 된 값은 **sql: relation** 또는 **sql: field** 주석 (예를 들어 "Order Details"에서 공백 문자 같은 특수 문자를 포함 합니다. 테이블 이름)이이 값 (예: "[Order Details]") 대괄호로 묶어야 합니다.  
  
-   Updategram을 사용할 때 체인 관계는 지원되지 않습니다. 예를 들어 테이블 A와 C가 테이블 B를 사용하는 체인 관계를 통해 연결된 경우 updategram을 실행하려고 하면 다음 오류가 발생합니다.  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     스키마와 updategram 모두 형식이 올바르고 다른 문제가 없더라도 체인 관계가 있으면 이 오류가 발생합니다.  
  
-   Updategram에 전달 하는 허용 하지 않는 **이미지** 업데이트 중 매개 변수로 데이터를 입력 합니다.  
  
-   이진 대형 개체 (BLOB)와 같은 형식을 **텍스트/ntext** 이미지에서는 사용할 수 없습니다 및는  **\<하기 전에 >** 에서 사용 하기 위해 포함 됩니다이 때문에 updategram으로 작업할 때의 블록 동시성 제어입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 BLOB 형식 비교에 대한 제한으로 인해 문제가 발생할 수 있습니다. WHERE 절에 열을 비교 하는 것에 대 한 LIKE 키워드는 사용 하는 예를 들어는 **텍스트** 데이터 형식입니다; 그러나 비교 작업이 실패 합니다 데이터의 크기는 8k 이상이 BLOB 형식입니다.  
  
-   에 특수 문자가 **ntext** 데이터 비교 BLOB 형식에 대 한 제한으로 인해 SQLXML 4.0 문제가 발생할 수 있습니다. "[Serializable]" 사용 예를 들어는  **\<하기 전에 >** 동시성의 열 검사를 수행할 때 updategram의 블록 **ntext** 종류는 다음과 같은 SQLOLEDB와 함께 실패 합니다 오류 설명:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>관련 항목:  
 [Updategram 보안 고려 사항 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
