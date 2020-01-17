---
title: 보조 선택적 XML 인덱스 만들기, 변경 및 삭제 | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
ms.assetid: 45128105-833b-40a9-9cc9-1ae03ac0b52b
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: ee462efca08173d6571fe5a3b3971b8f0460988a
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258367"
---
# <a name="create-alter-and-drop-secondary-selective-xml-indexes"></a>보조 선택적 XML 인덱스 만들기, 변경 및 삭제
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  새 보조 선택적 XML 인덱스를 만들거나 기존 보조 선택적 XML 인덱스를 변경 또는 삭제하는 방법에 대해 설명합니다.  
  
##  <a name="create"></a> 보조 선택적 XML 인덱스 만들기  
  
### <a name="how-to-create-a-secondary-selective-xml-index"></a>방법: 보조 선택적 XML 인덱스 만들기  
 **Transact-SQL을 사용하여 보조 선택적 XML 인덱스 만들기**  
 CREATE XML INDEX 문을 호출하여 보조 선택적 XML 인덱스를 만듭니다. 자세한 내용은 [CREATE XML INDEX&#40;선택적 XML 인덱스&#41;](../../t-sql/statements/create-xml-index-selective-xml-indexes.md)를 참조하세요.  
  
 **예제**  
  
 다음 예에서는 `'pathabc'`경로에서 보조 선택적 XML 인덱스를 만듭니다. 인덱싱할 경로는 CREATE SELECTIVE XML INDEX 문을 사용하여 해당 경로를 만들 때 지정한 경로 이름으로 식별됩니다. 자세한 내용은 [CREATE SELECTIVE XML INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md)를 참조하세요.  
  
```sql  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="alter"></a> 보조 선택적 XML 인덱스 변경  
 보조 선택적 XML 인덱스에 대해서는 ALTER 문이 지원되지 않습니다. 보조 선택적 XML 인덱스를 변경하려면 기존 인덱스를 삭제하고 다시 만드십시오.  
  
### <a name="how-to-alter-a-secondary-selective-xml-index"></a>방법: 보조 선택적 XML 인덱스 변경  
 **Transact-SQL을 사용하여 보조 선택적 XML 인덱스 변경**  
 1.  DROP INDEX 문을 호출하여 기존의 보조 선택적 XML 인덱스를 삭제합니다. 자세한 내용은 [DROP INDEX&#40;선택적 XML 인덱스&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md)를 참조하세요.  
  
2.  CREATE XML INDEX 문을 호출하여 원하는 옵션으로 인덱스를 다시 만듭니다. 자세한 내용은 [CREATE XML INDEX&#40;선택적 XML 인덱스&#41;](../../t-sql/statements/create-xml-index-selective-xml-indexes.md)를 참조하세요.  
  
 **예제**  
  
 다음 예에서는 보조 선택적 XML 인덱스를 삭제하고 다시 만들어 변경합니다.  
  
```sql  
DROP INDEX filt_sxi_index_c  
  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="drop"></a> 보조 선택적 XML 인덱스 삭제  
  
### <a name="how-to-drop-a-secondary-selective-xml-index"></a>방법: 보조 선택적 XML 인덱스 삭제  
 **Transact-SQL을 사용하여 보조 선택적 XML 인덱스 삭제**  
 DROP INDEX 문을 호출하여 보조 선택적 XML 인덱스를 삭제합니다. 자세한 내용은 [DROP INDEX&#40;선택적 XML 인덱스&#41;](../../t-sql/statements/drop-index-selective-xml-indexes.md)를 참조하세요.  
  
 **예제**  
  
 다음 예에서는 DROP INDEX 문을 보여 줍니다.  
  
```sql  
DROP INDEX ssxi_index  
ON tbl  
```  
  
  
## <a name="see-also"></a>참고 항목  
 [SXI&#40;선택적 XML 인덱스&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
  
  
