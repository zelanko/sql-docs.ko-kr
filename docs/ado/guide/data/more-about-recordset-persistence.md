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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924904"
---
# <a name="more-about-recordset-persistence"></a>레코드 집합 지속성에 대한 자세한 정보
ADO Recordset 개체를 지 원하는 내용 저장을 **Recordset** 개체를 사용 하 여 파일에 해당 [저장](../../../ado/reference/ado-api/save-method.md) 메서드. 영구적으로 저장 된 파일을 로컬에 있을 수 있습니다 드라이브, 서버 또는 사이트 웹 url입니다. 파일 중 하나를 사용 하 여 복원할 수 있습니다 나중에 [열기](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드의 **레코드 집합** 개체 또는 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 메서드를 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
 또한 합니다 [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) 메서드 변환을 **레코드 집합** 열과 행을 지정 된 문자를 사용 하 여 구분 되는 폼 개체입니다.  
  
 유지 하는 **레코드 집합**, 파일에 저장할 수 있는 형식으로 변환 하 여 시작 합니다. **레코드 집합** 전용 고급 데이터 테이블 그램 (ADTG) 형식 또는 open Extensible Markup Language (XML) 형식에 개체를 저장할 수 있습니다. ADTG 예제는 다음 섹션에 표시 됩니다. XML 지 속성에 대 한 자세한 내용은 참조 하세요. [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)합니다.  
  
 지속된 된 파일에 보류 중인 변경 내용을 저장 합니다. 반환 하는 쿼리를 실행할 수 있도록이 작업을 수행을 **레코드 집합** 개체를 편집 합니다 **레코드 집합**하 고 보류 중인 변경 내용 저장, 나중에 복원 합니다 **레코드 집합**, 차례로 데이터 소스를 업데이트 하는 저장 된를 사용 하 여 보류 중인 변경 내용입니다.  
  
 영구적으로 저장 하는 방법은 **Stream** 개체를 참조 하십시오 [스트림 및 지 속성](../../../ado/guide/data/streams-and-persistence.md)합니다.  
  
 예로 **레코드 집합** 지 속성 XML 레코드 집합 지 속성 시나리오를 참조 하세요.  
  
## <a name="example"></a>예제  
  
### <a name="save-a-recordset"></a>레코드 집합을 저장 합니다.  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>Recordset.Open를 사용 하 여 지속형된 파일을 엽니다.  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 필요에 따라 경우 합니다 **레코드 집합** 는 활성 연결이 없으면, 모든 기본값을 수락 하는 다음 코드:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>Connection.Execute를 사용 하 여 지속형된 파일을 엽니다.  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>Rds.를 사용 하 여 지속형된 파일 열기 DataControl:  
 이 경우에 **서버** 속성이 설정 되지 않았습니다.  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>관련 항목  
 [GetString 메서드 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Microsoft OLE DB 지 속성 공급자 (ADO 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [스트림 및 지속성](../../../ado/guide/data/streams-and-persistence.md)
