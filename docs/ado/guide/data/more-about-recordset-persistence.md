---
title: "지 속성 레코드 집합에 대 한 자세한 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5dedcc3c1326c8b71844637c24f81835472ae9e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="more-about-recordset-persistence"></a>지 속성 레코드 집합에 대 한 자세한 정보
ADO 레코드 집합 개체의 콘텐츠를 저장 하도록 지원는 **레코드 집합** 개체를 사용 하 여 파일에 해당 [저장](../../../ado/reference/ado-api/save-method.md) 메서드. 영구적으로 저장 된 파일은 로컬에 있을 수 있습니다 드라이브, 서버 또는 사이트는 웹에서 URL로 합니다. 사용 하 여 파일을 복원할 수 나중의 [열려](../../../ado/reference/ado-api/open-method-ado-recordset.md) 의 메서드는 **레코드 집합** 개체 또는 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 의 메서드는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다.  
  
 또한는 [GetString](../../../ado/reference/ado-api/getstring-method-ado.md) 메서드 변환은 **레코드 집합** 개체의 열과 행은 지정 된 문자를 구분 하는 폼입니다.  
  
 유지 하는 **레코드 집합**, 먼저 파일에 저장할 수 있는 형식으로 변환 합니다. **레코드 집합** 개체를 소유 하는 고급 데이터 테이블 그램 (ADTG) 형식 또는 open Extensible Markup Language (XML) 형식에 저장할 수 있습니다. 다음 섹션에 ADTG 예가 나와 있습니다. XML 지 속성에 대 한 자세한 내용은 참조 [XML 형식의 레코드 지속](../../../ado/guide/data/persisting-records-in-xml-format.md)합니다.  
  
 지속된 된 파일에 보류 중인 변경 내용을 저장 합니다. 반환 하는 쿼리를 실행할 수 있도록이 수행 하는 **레코드 집합** 개체, 편집은 **레코드 집합**, 저장 하 고 보류 중인 변경 내용, 나중에 복원 하는 **레코드 집합**, 한 다음 저장 된 데이터 원본을 업데이트 보류 중인 변경 내용입니다.  
  
 영구적으로 저장 하는 방법에 대 한 내용은 **스트림** 개체 참조 [스트림 및 지 속성](../../../ado/guide/data/streams-and-persistence.md)합니다.  
  
 에 대 한 예제 **레코드 집합** 지 속성 XML 레코드 집합 지 속성 시나리오를 참조 하십시오.  
  
## <a name="example"></a>예제  
  
### <a name="save-a-recordset"></a>레코드 집합을 저장 합니다.  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>Recordset.Open으로 지속형된 파일을 엽니다.  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 필요에 따라 경우는 **레코드 집합** 가 현재 연결 되어 있지, 모든 기본값을 적용 하 고 다음 코드:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>Connection.Execute로 지속형된 파일을 엽니다.  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>Rds. 지속형된 파일을 열 DataControl:  
 이 경우에 **서버** 속성이 설정 되지 않았습니다.  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>관련 항목:  
 [GetString 메서드 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Microsoft OLE DB 지 속성 공급자 (ADO 서비스 공급자)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [스트림 및 지속성](../../../ado/guide/data/streams-and-persistence.md)
