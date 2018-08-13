---
title: 지침 및 제한 사항 (SQLXML 4.0) XML Updategram의 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 47b385fcd7758f42f9c7009ef2469b0598309854
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39540373"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>XML updategram에 대한 지침 및 제한 사항(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML updategram 사용 시 다음 사항에 유의하십시오.  
  
-   단일 쌍을 사용 하 여 삽입 작업에 대 한 updategram을 사용 하는 경우  **\<하기 전에 >** 하 고  **\<후 >** 블록 합니다  **\<하기 전에 >** 블록을 생략할 수 있습니다. 삭제 작업의 경우 반대로 합니다  **\<후 >** 블록을 생략할 수 있습니다.  
  
-   여러 개의 updategram을 사용 하는 경우  **\<하기 전에 >** 하 고  **\<후 >** 블록의  **\<동기화 >** 태그를 모두  **\<하기 전에 >** 요소와  **\<후 >** 블록 형식으로 지정 해야 합니다  **\<하기 전에 >** 및  **\<후 >** 쌍입니다.  
  
-   Updategram의 업데이트는 XML 스키마에서 제공한 XML 뷰에 적용됩니다. 따라서 기본 매핑이 성공하려면 updategram에서 스키마 파일 이름을 지정하거나, 파일 이름을 지정하지 않을 경우 요소 및 특성 이름이 데이터베이스의 테이블 및 열 이름과 일치해야 합니다.  
  
-   SQLXML 4.0에서는 updategram의 모든 열 값이 제공된 스키마(XDR 또는 XSD)에서 명시적으로 매핑되어야 해당 자식 요소에 대한 XML 뷰를 만들 수 있습니다. 이 동작은 외래 키의 일부로 암시 된 경우 스키마에 매핑되지 않은 열에 대 한 값을 허용 하는 SQLXML의 이전 버전에서을 **sql: relationship** 주석입니다. 이 변경 사항은 기본 키 값이 자식 요소로 전파되는 것에는 영향을 주지 않습니다. SQLXML 4.0에서 이 동작은 자식 요소에 대해 값이 명시적으로 지정되지 않은 경우에도 수행됩니다.  
  
-   Updategram을 사용 하 여 이진 열에 데이터를 수정 하는 경우 (같은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **이미지** 데이터 형식)에는 매핑 스키마를 제공 해야 합니다는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식 (예를 들어 **sql: datatype = "image"** ) 및 XML 데이터 형식 (예를 들어 **dt: type = "binhex"** 하거나 **dt: type = "binbase64**)를 지정 해야 합니다. Updategram에서는 이진 열에 대 한 데이터를 지정 해야 합니다. 합니다 **sql:url-인코딩** updategram은 매핑 스키마에 지정 된 주석이 무시 됩니다.  
  
-   작성할 때 XSD 스키마를 지정에 대 한 값을 **sql: relation** 또는 **sql: field** 주석 (예를 들어 "Order Details"에서 공백 문자 같은 특수 문자가 포함 되어 있습니다 테이블 이름)이이 값 (예: "[Order Details]") 대괄호로 묶어야 합니다.  
  
-   Updategram을 사용할 때 체인 관계는 지원되지 않습니다. 예를 들어 테이블 A와 C가 테이블 B를 사용하는 체인 관계를 통해 연결된 경우 updategram을 실행하려고 하면 다음 오류가 발생합니다.  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     스키마와 updategram 모두 형식이 올바르고 다른 문제가 없더라도 체인 관계가 있으면 이 오류가 발생합니다.  
  
-   Updategram에 전달 하는 허용 하지 않습니다 **이미지** 업데이트 중 매개 변수로 데이터를 입력 합니다.  
  
-   와 같은 이진 BLOB (large object) 형식을 **텍스트/ntext** 이미지에서 사용할 수 없습니다는  **\<하기 전에 >** 에서 사용 하기 위해 포함 됩니다이 때문에 updategram으로 작업할 때의 블록 동시성 제어 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 BLOB 형식 비교에 대한 제한으로 인해 문제가 발생할 수 있습니다. 예를 들어 LIKE 키워드는 WHERE 절에 열을 비교 합니다 **텍스트** 데이터 형식입니다; 그러나 비교 작업이 실패 BLOB 형식의 데이터 크기가 8k 이상이 있습니다.  
  
-   에 특수 문자가 **ntext** 데이터 비교 BLOB 유형에 대 한 제한으로 인해 SQLXML 4.0을 사용 하 여 문제를 발생할 수 있습니다. 예를 들어, "[serializable]"에서 사용 된  **\<하기 전에 >** 동시성 검사를 열 때 updategram의 블록 **ntext** 형식 다음 SQLOLEDB를 사용 하 여 실패 오류 설명:  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [Updategram 보안 고려 사항 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
