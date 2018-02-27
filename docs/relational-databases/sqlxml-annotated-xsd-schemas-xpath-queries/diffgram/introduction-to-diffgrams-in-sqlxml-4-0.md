---
title: "SQLXML 4.0의에서 DiffGrams 소개 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- annotations [SQLXML]
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: 1902d67f-baf3-46e6-a36c-b24b5ba6f8ea
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5743cbab13add72e27351c74424e09bc028496d9
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
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
 이 요소의 이름을 **DataInstance**,이 설명서에서 설명 용으로 사용 됩니다. 예를 들어,.NET Framework의 값의 데이터 집합에서 DiffGram을 생성 하는 경우는 **이름** 이 요소의 이름으로는 데이터 집합의 속성을 사용할 수는 있습니다. 이 블록에는 수정되지 않은 데이터를 포함하여 변경 후의 모든 관련 데이터가 포함됩니다. 이 블록의 요소를 무시 하는 DiffGram 처리 논리는 **diffgr: haschanges** 특성이 지정 되지 않았습니다.  
  
 **\<diffgr:before>**  
 이 선택적 블록에는 업데이트하거나 삭제해야 하는 원래 레코드 인스턴스(요소)가 포함됩니다. 모든 데이터베이스 (업데이트 또는 삭제)을 수정 중인 테이블 DiffGram으로에서 최상위 요소로 표시 해야 합니다는  **\<하기 전에 >** 블록입니다.  
  
 **\<diffgr:errors>**  
 이 선택적 블록은 DiffGram 처리 논리에서 무시됩니다.  
  
## <a name="diffgram-annotations"></a>DiffGram 주석  
 이러한 주석은 DiffGram 네임 스페이스에 정의 된 **":-microsoft-com:xml-diffgram-01"**:  
  
 **id**  
 이 특성의 요소와 쌍으로 연결을 사용 하 여  **\<하기 전에 >** 및  **\<DataInstance >** 블록입니다.  
  
 **hasChanges**  
 삽입 또는 업데이트 작업에 대 한 DiffGram이 특성을 지정 해야이 값을 가진 **삽입** 또는 **수정**합니다. 이 특성이 없으면의 해당 요소는  **\<DataInstance >** 처리를 통해 무시 논리 및 업데이트가 수행 됩니다. 작업 예제를 참조 하십시오. [DiffGram 예 &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
 **parentID**  
 이 특성은 DiffGram에서 요소 간의 부모-자식 관계를 지정하는 데 사용됩니다. 이 특성에만 표시 됩니다는 \<하기 전에 > 블록입니다. SQLXML에서 업데이트를 적용할 때 사용됩니다. 부모-자식 관계는 DiffGram에서 요소가 처리되는 순서를 결정하는 데 사용됩니다.  
  
## <a name="understanding-the-diffgram-processing-logic"></a>DiffGram 처리 논리 이해  
 DiffGram 처리 논리는 특정 규칙에 따라 작업이 삽입, 업데이트 또는 삭제 작업인지를 결정합니다. 다음 표에서는 이러한 규칙에 대해 설명합니다.  
  
|연산|Description|  
|---------------|-----------------|  
|Insert|DiffGram에서 요소가 표시 될 때 삽입 작업을 나타냅니다는  **\<DataInstance >** 블록에는 있지만 해당  **\<하기 전에 >** 블록과 **diffgr: haschanges** 특성이 지정 된 (**diffgr: haschanges = inserted**) 요소에 있습니다. DiffGram에 지정 된 레코드 인스턴스를 삽입 하는 경우에  **\<DataInstance >** 데이터베이스에는 블록입니다.<br /><br /> 경우는 **diffgr: haschanges** 특성이 지정 되지 않은, 요소가 처리 논리에서 무시 되 고 없는 삽입을 수행 합니다. 작업 예제를 참조 하십시오. [DiffGram 예 &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).|  
|Update|DiffGram에서 요소가 없는 경우 업데이트 작업을 나타냅니다는 \<하기 전에 >의 해당 요소는 블록의  **\<DataInstance >** 블록 (즉, 두 요소 모두는 **diffgr: id** 동일한 값을 가진 특성이) 및 **diffgr: haschanges** 특성의 값이 지정 **수정** 의 요소에는  **\<DataInstance >** 블록입니다.<br /><br /> 경우는 **diffgr: haschanges** 에서 요소 특성을 지정 하지 않으면는  **\<DataInstance >** 블록 처리 논리에서 오류가 반환 됩니다. 작업 예제를 참조 하십시오. [DiffGram 예 &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> 경우 **diffgr: parentid** 에 지정 된 된  **\<하기 전에 >** 요소에서 지정 된 부모-자식 관계를 차단 **parentID** 레코드 업데이트 되는 순서가 결정 됩니다.|  
|Delete|DiffGram에서 요소가 표시 될 때 삭제 작업을 나타냅니다는  **\<하기 전에 >** 블록에는 있지만 해당  **\<DataInstance >** 블록입니다. DiffGram에 지정 된 레코드 인스턴스를 삭제 하는 경우에  **\<하기 전에 >** 데이터베이스에서 블록입니다. 작업 예제를 참조 하십시오. [DiffGram 예 &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).<br /><br /> 경우 **diffgr: parentid** 에 지정 된 된  **\<하기 전에 >** 요소에서 지정 된 부모-자식 관계를 차단 **parentID** 레코드가 삭제 되는 순서를 결정 합니다.|  
  
> [!NOTE]  
>  DiffGrams에 매개 변수를 전달할 수는 없습니다.  
  
  
