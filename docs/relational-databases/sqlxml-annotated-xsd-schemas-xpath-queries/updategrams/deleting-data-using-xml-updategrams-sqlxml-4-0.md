---
title: XML Updategrams을 사용 하 여 데이터 삭제 (SQLXML)
description: SQLXML 4.0에서 XML updategram를 사용 하 여 데이터를 삭제 하는 방법에 대해 알아봅니다.
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
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 085a1f8def37870f4fe5e449e4c206ed376f8d2a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462884"
---
# <a name="deleting-data-using-xml-updategrams-sqlxml-40"></a>XML Updategram을 사용하여 데이터 삭제(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Updategram는 레코드 인스턴스가 블록에 **\<before>** 해당 레코드가 없는 블록에 표시 되는 경우 삭제 작업을 나타냅니다 **\<after>** . 이 경우 updategram는 데이터베이스에서 블록의 레코드를 삭제 합니다 **\<before>** .  
  
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
  
 **\<after>** Updategram가 삭제 작업만 수행 하는 경우 태그를 생략할 수 있습니다. 선택적 **매핑 스키마** 특성을 지정 하지 않으면 **\<ElementName>** updategram에 지정 된가 데이터베이스 테이블에 매핑되고 자식 요소 또는 특성은 테이블의 열에 매핑됩니다.  
  
 Updategram에 지정 된 요소가 테이블에서 둘 이상의 행과 일치 하거나 행과 일치 하지 않는 경우 updategram는 오류를 반환 하 고 전체 블록을 취소 합니다 **\<sync>** . Updategram의 요소는 한 번에 하나의 레코드만 삭제할 수 있습니다.  
  
## <a name="examples"></a>예  
 이 섹션의 예에서는 기본 매핑을 사용합니다. 즉, Updategram에 매핑 스키마가 지정되어 있지 않습니다. 매핑 스키마를 사용 하는 updategram의 추가 예제는 [Updategram &#40;SQLXML 4.0&#41;에서 주석이 추가 된 매핑 스키마 지정 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)을 참조 하세요.  
  
 다음 예제를 사용 하 여 작업 예제를 만들려면 [SQLXML 예를 실행 하기 위한 요구 사항](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)에 지정 된 요구 사항을 충족 해야 합니다.  
  
### <a name="a-deleting-a-record-by-using-an-updategram"></a>A. Updategram을 사용하여 단일 레코드 삭제  
 다음 Updategram은 HumanResources.Shift 테이블에서 레코드 두 개를 삭제합니다.  
  
 이러한 예에서 Updategram은 매핑 스키마를 지정하지 않으므로 요소 이름은 테이블 이름에 매핑되고 특성 또는 하위 요소는 열에 매핑되는 기본 매핑을 사용합니다.  
  
 이 첫 번째 updategram는 특성 중심 이며 블록에서 두 교대 교대 (야간 및 야간 시간)을 식별 **\<before>** 합니다. 블록에 해당 레코드가 없기 때문에 **\<after>** 이는 삭제 작업입니다.  
  
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
  
1.  [XML Updategrams &#40;SQLXML 4.0&#41;를 사용 하 여 데이터 삽입 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)에서 예제 B ("updategram를 사용 하 여 여러 레코드 삽입")를 완료 합니다.  
  
2.  위의 updategram을 메모장에 복사 하 고 [XML Updategrams &#40;SQLXML 4.0&#41;를 사용 하 여 데이터 삽입 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)에서 완료 하는 데 사용한 것과 동일한 폴더 ("updategram를 사용 하 여 여러 레코드 삽입")에 Updategram-RemoveShifts.xml로 저장 합니다.  
  
3.  SQLXML 4.0 테스트 스크립트(Sqlxml4test.vbs)를 만든 다음 이 스크립트를 사용하여 Updategram을 실행합니다.  
  
     자세한 내용은 [ADO를 사용 하 여 SQLXML 4.0 쿼리 실행](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Updategram 보안 고려 사항은 SQLXML 4.0&#41;&#40;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
