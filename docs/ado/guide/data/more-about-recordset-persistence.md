---
title: 레코드 집합 지 속성에 대 한 자세한 정보 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bee7d185d5f598a2f0a086bb7e3bea49ddfff88c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924904"
---
# <a name="more-about-recordset-persistence"></a>레코드 집합 지속성에 대한 자세한 정보
ADO 레코드 집합 개체는 [Save](../../../ado/reference/ado-api/save-method.md) 메서드를 사용 하 여 **레코드 집합** 개체의 내용을 파일에 저장 하는 것을 지원 합니다. 영구적으로 저장 된 파일은 로컬 드라이브, 서버 또는 웹 사이트의 URL로 존재할 수 있습니다. 나중에이 파일을 **Recordset** 개체의 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드 또는 [Connection](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 메서드를 사용 하 여 복원할 수 있습니다.  
  
 또한 [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) 메서드는 **레코드 집합** 개체를 사용자가 지정 하는 문자를 사용 하 여 열과 행을 구분 하는 형식으로 변환 합니다.  
  
 **레코드 집합**을 유지 하려면 먼저 파일에 저장할 수 있는 형식으로 변환 합니다. **레코드 집합** 개체는 ADTG (독점적인 Advanced Data TableGram) 형식 또는 open XML(EXTENSIBLE MARKUP LANGUAGE) (XML) 형식으로 저장할 수 있습니다. ADTG 예제는 다음 섹션에 나와 있습니다. XML 지 속성에 대 한 자세한 내용은 [xml 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)를 참조 하세요.  
  
 지속형 파일에 보류 중인 변경 내용을 저장 합니다. 이렇게 하면 **레코드 집합** 개체를 반환 하는 쿼리를 실행 하 고, **레코드 집합**을 편집 하 고, 보류 중인 변경 내용을 저장 하 고, 나중에 **레코드 집합**을 복원 하 고 저장 된 보류 중인 변경 내용으로 데이터 원본을 업데이트할 수 있습니다.  
  
 **스트림** 개체를 영구적으로 저장 하는 방법에 대 한 자세한 내용은 [스트림 및 지 속성](../../../ado/guide/data/streams-and-persistence.md)을 참조 하세요.  
  
 **레코드 집합** 지 속성의 예는 XML 레코드 집합 지 속성 시나리오를 참조 하세요.  
  
## <a name="example"></a>예제  
  
### <a name="save-a-recordset"></a>레코드 집합을 저장 합니다.  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>레코드 집합을 사용 하 여 지속형 파일 열기:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 필요에 따라 **레코드 집합** 에 활성 연결이 없는 경우 모든 기본값을 그대로 적용 하 고 다음과 같은 코드를 만들 수 있습니다.  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>연결을 사용 하 여 지속형 파일 열기:  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>RDS를 사용 하 여 지속형 파일을 엽니다. DataControl  
 이 경우 **서버** 속성은 설정 되지 않습니다.  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>참고 항목  
 [GetString 메서드 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Microsoft OLE DB 지 속성 공급자 (ADO 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [스트림 및 지속성](../../../ado/guide/data/streams-and-persistence.md)
