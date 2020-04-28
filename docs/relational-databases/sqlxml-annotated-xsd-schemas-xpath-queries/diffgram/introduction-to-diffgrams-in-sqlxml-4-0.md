---
title: SQLXML 4.0의 DiffGrams 소개
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3994a9d0bc863367edf5b1844772b94a63f19d4d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75257247"
---
# <a name="introduction-to-diffgrams-in-sqlxml-40"></a>SQLXML 4.0의 DiffGrams 소개
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 항목에서는 DiffGrams에 대해 간략하게 소개합니다.  
  
## <a name="diffgram-format"></a>DiffGram 형식  
 일반 DiffGram 형식은 다음과 같습니다.  
  
```  
<?xml version="1.0"?>  
<diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
   <DataInstance>  
      ...  
   </DataInstance>  
   [<diffgr:before>  
        ...  
   </diffgr:before>]  
  
   [<diffgr:errors>  
        ...  
   </diffgr:errors>]  
</diffgr:diffgram>  
```  
  
 DiffGram 형식은 다음과 같은 블록으로 구성됩니다.  
  
 **\<DataInstance>**  
 이 요소의 이름 **Datainstance**는이 설명서의 설명을 위해 사용 됩니다. 예를 들어 .NET Framework의 데이터 집합에서 DiffGram을 생성 한 경우 데이터 집합의 **이름** 속성 값이이 요소의 이름으로 사용 됩니다. 이 블록에는 수정되지 않은 데이터를 포함하여 변경 후의 모든 관련 데이터가 포함됩니다. DiffGram 처리 논리는이 블록에서 **diffgr: hasChanges** 특성이 지정 되지 않은 요소를 무시 합니다.  
  
 **\<diffgr: 이전>**  
 이 선택적 블록에는 업데이트하거나 삭제해야 하는 원래 레코드 인스턴스(요소)가 포함됩니다. DiffGram에서 수정 (업데이트 또는 삭제) 하는 모든 데이터베이스 테이블은 ** \<before>** 블록에 최상위 요소로 나타나야 합니다.  
  
 **\<diffgr: 오류>**  
 이 선택적 블록은 DiffGram 처리 논리에서 무시됩니다.  
  
## <a name="diffgram-annotations"></a>DiffGram 주석  
 이러한 주석은 DiffGram 네임 스페이스 **"urn: 스키마-microsoft-com: diffgram-01"** 에 정의 되어 있습니다.  
  
 **id**  
 이 특성은 ** \<>** ** \<** 하기 전에의 요소를 쌍으로 연결 하는 데 사용 되며,>데이터 인스턴스는 블록을 사용 합니다.  
  
 **hasChanges**  
 삽입 또는 업데이트 작업의 경우 DiffGram은 **삽입** 또는 **수정**된 값을 사용 하 여이 특성을 지정 해야 합니다. 이 특성이 없는 경우 ** \<datainstance>** 의 해당 요소는 처리 논리에서 무시 되 고 업데이트가 수행 되지 않습니다. 작업 예제는 [DiffGram 예 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)를 참조 하세요.  
  
 **parentID**  
 이 특성은 DiffGram에서 요소 간의 부모-자식 관계를 지정하는 데 사용됩니다. 이 특성은 \<before> 블록에만 표시 됩니다. SQLXML에서 업데이트를 적용할 때 사용됩니다. 부모-자식 관계는 DiffGram에서 요소가 처리되는 순서를 결정하는 데 사용됩니다.  
  
## <a name="understanding-the-diffgram-processing-logic"></a>DiffGram 처리 논리 이해  
 DiffGram 처리 논리는 특정 규칙에 따라 작업이 삽입, 업데이트 또는 삭제 작업인지를 결정합니다. 다음 표에서는 이러한 규칙에 대해 설명합니다.  
  
|작업(Operation)|Description|  
|---------------|-----------------|  
|삽입|DiffGram은 요소가 ** \<datainstance>** 블록에 표시 되 고 해당 ** \<하는 이전>** 블록에는 나타나지 않고 요소에 대해 **diffgr: haschanges** 특성이 지정 된 (**diffgr: haschanges = inserted**) 삽입 작업을 나타냅니다. 이 경우 DiffGram은 ** \<datainstance** 에 지정 된 레코드 인스턴스를 데이터베이스에>삽입 합니다.<br /><br /> **Diffgr: hasChanges** 특성이 지정 되지 않은 경우 요소는 처리 논리에서 무시 되 고 삽입이 수행 되지 않습니다. 작업 예제는 [DiffGram 예 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)를 참조 하세요.|  
|업데이트|DiffGram은 ** \<datainstance>** 블록에 해당 요소가 있는 경우 (즉 \<, 두 요소에 동일한 값을 가진 **diffgr: id** 특성이 있는 경우), **diffgr: haschanges** 특성은 ** \<datainstance>** 블록의 요소에서 **수정** 된 값으로 지정 된 before> 블록에 업데이트 작업을 나타냅니다.<br /><br /> Datainstance>블록의 요소에 **diffgr: haschanges** 특성이 지정 되지 않은 경우 처리 논리에 의해 오류가 반환 됩니다. ** \<** 작업 예제는 [DiffGram 예 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)를 참조 하세요.<br /><br /> ParentID 블록 ** \<>** 에 **diffgr:** 이 지정 된 경우 **parentID** 로 지정 된 요소의 부모-자식 관계를 사용 하 여 레코드가 업데이트 되는 순서를 결정 합니다.|  
|DELETE|DiffGram은 요소가 ** \<before>** 블록에 표시 되 고 해당 ** \<datainstance>** 블록에는 없는 경우 삭제 작업을 나타냅니다. 이 경우 DiffGram은 데이터베이스의 ** \<before>** 블록에 지정 된 레코드 인스턴스를 삭제 합니다. 작업 예제는 [DiffGram 예 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)를 참조 하세요.<br /><br /> ParentID 블록 ** \<>** 에 **diffgr:** 이 지정 된 경우 **parentID** 로 지정 된 요소의 부모-자식 관계를 사용 하 여 레코드가 삭제 되는 순서를 결정 합니다.|  
  
> [!NOTE]  
>  DiffGrams에 매개 변수를 전달할 수는 없습니다.  
  
  
