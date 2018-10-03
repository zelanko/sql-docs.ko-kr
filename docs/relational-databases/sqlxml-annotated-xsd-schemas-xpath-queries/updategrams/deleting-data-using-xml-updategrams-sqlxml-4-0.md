---
title: XML Updategrams (SQLXML 4.0)을 사용 하 여 데이터 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- <after> block
- updategrams [SQLXML], deleting data
- <before> block
- mapping-schema attribute
- record deletions [SQLXML]
ms.assetid: 4fb116d7-7652-474a-a567-cb475a20765c
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8246222b24c4f1b6e66e99e64b45550a130553c7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709947"
---
# <a name="deleting-data-using-xml-updategrams-sqlxml-40"></a>XML Updategram을 사용하여 데이터 삭제(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  레코드 인스턴스가 표시 되는 경우는 updategram 삭제 작업을 나타냅니다는  **\<전에 >** 블록에 해당 레코드가 없는  **\<후 >** 블록입니다. updategram에서 레코드를 삭제 하는 경우에  **\<전에 >** 데이터베이스에서 차단 합니다.  
  
 삭제 작업에 대한 Updategram 형식은 다음과 같습니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
       <ElementName />  
      [<ElementName .../>... ]  
   </updg:before>  
    [<updg:after>  
    </updg:after>]  
  </updg:sync>  
</ROOT>  
```  
  
 생략할 수 있는  **\<후 >** 태그를 지정 하면 updategram만 삭제 작업을 수행 하는 경우. 선택적 지정 하지 않은 경우 **매핑 스키마** 특성을  **\<ElementName >** 데이터베이스 테이블에 updategram은 맵 및 자식 요소 또는 특성 지도를 지정 테이블의 열입니다.  
  
 Updategram은 오류를 반환 하 고 전체 취소는 updategram에 지정 된 요소 중 하나는 테이블의 여러 행과 일치, 행과 일치 하지 않습니다  **\<동기화 >** 블록입니다. Updategram의 요소는 한 번에 하나의 레코드만 삭제할 수 있습니다.  
  
## <a name="examples"></a>예  
 이 섹션의 예에서는 기본 매핑을 사용합니다. 즉, Updategram에 매핑 스키마가 지정되어 있지 않습니다. 매핑 스키마를 사용 하는 updategram에 대 한 더 많은 예제를 참조 하세요 [Updategram에 주석이 추가 된 매핑 스키마 지정 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)합니다.  
  
 다음 예제를 사용 하 여 작업 예제를 만들려면에 지정 된 요구 사항을 충족 해야 합니다 [SQLXML 예 실행에 대 한 요구 사항](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)합니다.  
  
### <a name="a-deleting-a-record-by-using-an-updategram"></a>1. Updategram을 사용하여 단일 레코드 삭제  
 다음 Updategram은 HumanResources.Shift 테이블에서 레코드 두 개를 삭제합니다.  
  
 이러한 예에서 Updategram은 매핑 스키마를 지정하지 않으므로 요소 이름은 테이블 이름에 매핑되고 특성 또는 하위 요소는 열에 매핑되는 기본 매핑을 사용합니다.  
  
 이 첫 번째 updategram 특성 중심 이며 2 교대 (하루 저녁 및 밤 밤)에서 식별 된  **\<전에 >** 블록. 해당 레코드가 있기 때문에 해당  **\<후 >** 블록 삭제 작업입니다.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
       <HumanResources.Shift ShiftID="4"  
                        Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift ShiftID="5"  
                        Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:before>  
  <updg:after>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Updategram을 테스트하려면  
  
1.  전체 예제 B ("에 여러 레코드 삽입 된 updategram을 사용 하 여") [XML Updategrams를 사용 하 여 데이터 삽입 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
2.  위의 updategram를 메모장에 복사 하 고 완료 ("여러 레코드 삽입 된 updategram을 사용 하 여")에서 사용한 것과 동일한 폴더에 Updategram RemoveShifts.xml로 저장 [XML Updategrams를 사용 하 여 데이터 삽입 &#40;SQLXML 4.0&#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 Updategram을 실행합니다.  
  
     자세한 내용은 [SQLXML 4.0 쿼리 실행을 사용 하 여 ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Updategram 보안 고려 사항 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
