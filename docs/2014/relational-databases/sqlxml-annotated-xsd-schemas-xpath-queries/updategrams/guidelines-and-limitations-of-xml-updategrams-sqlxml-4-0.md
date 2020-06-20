---
title: XML Updategrams의 지침 및 제한 사항 (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e28f4258aef27403c107158dd13efe5ada02c03
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84996244"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>XML updategram에 대한 지침 및 제한 사항(SQLXML 4.0)
  XML updategram 사용 시 다음 사항에 유의하십시오.  
  
-   Updategram를 사용 하 여 단일 쌍의 and 블록만 포함 하는 삽입 작업을 수행 하는 경우에는 **\<before>** **\<after>** 블록을 **\<before>** 생략할 수 있습니다. 반대로 삭제 작업의 경우에는 **\<after>** 블록을 생략할 수 있습니다.  
  
-   태그에서 여러 개의 및 블록을 사용 하는 updategram를 사용 하는 경우에는 **\<before>** **\<after>** **\<sync>** **\<before>** 블록과 블록을 모두 **\<after>** 형성 하 고 쌍으로 지정 해야 합니다 **\<before>** **\<after>** .  
  
-   Updategram의 업데이트는 XML 스키마에서 제공한 XML 뷰에 적용됩니다. 따라서 기본 매핑이 성공하려면 updategram에서 스키마 파일 이름을 지정하거나, 파일 이름을 지정하지 않을 경우 요소 및 특성 이름이 데이터베이스의 테이블 및 열 이름과 일치해야 합니다.  
  
-   SQLXML 4.0에서는 updategram의 모든 열 값이 제공된 스키마(XDR 또는 XSD)에서 명시적으로 매핑되어야 해당 자식 요소에 대한 XML 뷰를 만들 수 있습니다. 이 동작은 이전 버전의 SQLXML에서 달라진 동작입니다. 이전 버전에서는 열 값이 `sql:relationship` 주석에서 외래 키의 일부로 암시된 경우 스키마에서 열 값을 매핑하지 않아도 되었습니다. 이 변경 사항은 기본 키 값이 자식 요소로 전파되는 것에는 영향을 주지 않습니다. SQLXML 4.0에서 이 동작은 자식 요소에 대해 값이 명시적으로 지정되지 않은 경우에도 수행됩니다.  
  
-   Updategram를 사용 하 여 이진 열 (예: 데이터 형식)의 데이터를 수정 하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `image` [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식 (예: `sql:datatype="image"` ) 및 XML 데이터 형식 (예: `dt:type="binhex"` 또는 `dt:type="binbase64` )을 지정 해야 하는 매핑 스키마를 제공 해야 합니다. Updategram에서는 이진 열에 대한 데이터를 지정해야 합니다. 매핑 스키마에 지정된 `sql:url-encode` 주석은 updategram에서 무시됩니다.  
  
-   XSD 스키마를 작성할 때 `sql:relation` 또는 `sql:field` 주석에 대해 지정하는 값에 "Order Details" 테이블 이름처럼 공백 문자 같은 특수 문자가 포함되면 "[Order Details]"처럼 값을 대괄호로 묶어야 합니다.  
  
-   Updategram을 사용할 때 체인 관계는 지원되지 않습니다. 예를 들어 테이블 A와 C가 테이블 B를 사용하는 체인 관계를 통해 연결된 경우 updategram을 실행하려고 하면 다음 오류가 발생합니다.  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     스키마와 updategram 모두 형식이 올바르고 다른 문제가 없더라도 체인 관계가 있으면 이 오류가 발생합니다.  
  
-   Updategram은 업데이트 중 `image` 형식 데이터를 매개 변수로 전달하는 것을 허용하지 않습니다.  
  
-   Updategrams으로 작업할 때는 및 이미지와 같은 BLOB (Binary large object) 형식을 `text/ntext` 블록에 사용 하면 안 **\<before>** 됩니다. 동시성 제어에 사용 하기 위해 이러한 형식을 포함 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 BLOB 형식 비교에 대한 제한으로 인해 문제가 발생할 수 있습니다. 예를 들어 LIKE 키워드는 `text` 데이터 형식의 열을 비교하기 위해 WHERE 절에 사용되지만 BLOB 형식의 데이터 크기가 8K 이상이면 비교 작업이 실패합니다.  
  
-   SQLXML 4.0에서는 BLOB 형식 비교에 대한 제한으로 인해 `ntext` 데이터에 특수 문자가 있으면 문제가 발생할 수 있습니다. 예를 들어 **\<before>** 형식의 열에 대 한 동시성 검사에 사용 될 때 updategram의 블록에 "[Serializable]"을 사용 하면 `ntext` 다음과 같은 SQLOLEDB 오류 설명과 함께 실패 합니다.  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [Updategram 보안 고려 사항은 SQLXML 4.0&#41;&#40;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
