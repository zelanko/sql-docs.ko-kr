---
title: 데이터를 유지 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 438a09dd8f835653f9b2c76d73b7ce7f4583c1a5
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272202"
---
# <a name="persisting-data"></a>데이터 유지
(예: 랩톱을 사용 하 여) 휴대용 컴퓨팅 연결 되거나 연결이 끊긴 상태에서 실행할 수 있는 응용 프로그램에 대 한 필요 하 게 되었습니다. ADO는 커서를 저장 하는 기능을 개발자에 게 제공 하 여이 대 한 지원을 추가 했습니다 **레코드 집합** 디스크에 나중에 다시 로드 합니다.  
  
 일부 경우에이 유형의 기능을 포함 하 여 다음을 사용할 수 있습니다.  
  
-   **여행:** 이동 중에 응용 프로그램을 받은 경우에 변경 내용을 확인 하 고 다음 나중에 데이터베이스에 다시 연결 및 커밋 수 있는 새 레코드를 추가 하는 기능을 제공 하는 데 반드시 필요 합니다.  
  
-   **자주 업데이트 되는 조회:** 보통 응용 프로그램 테이블 조회로 사용 됩니다-예를 들어 간단히 로드할 합니다. 자주 업데이트 되 고 읽기 전용으로 설정 됩니다. 응용 프로그램이 시작 될 때마다 서버에서이 데이터를 읽고, 하는 대신 응용 프로그램 단순히 데이터를 로드할 수에서 논리적 지속형 **레코드 집합**합니다.  
  
 Ado에서 저장 하 고 로드할 **레코드 집합**를 사용 하 여는 **Recordset.Save** 및 **Recordset.Open(,,,adCmdFile)** ADO에 대 한 메서드 **레코드 집합**개체입니다.  
  
 사용할 수 있습니다는 **레코드 집합 저장** 메서드 여 ADO를 **레코드 집합** 디스크에 파일에 있습니다. (저장할 수도 있습니다는 **레코드 집합** ADO에 **스트림** 개체입니다. **스트림** 개체는이 가이드의 뒷부분에 나오는 설명 합니다.) 이상 버전에서는 사용할 수 있습니다는 **열려** 메서드를 다시 열려면는 **레코드 집합** 는 사용 합니다. ADO 기본적으로 저장 된 **레코드 집합** 전용 Microsoft 고급 데이터 테이블 그램 (ADTG) 형식으로. 이 이진 형식을 사용 하 여 지정 되는 **adPersistADTG PersistFormatEnum** 값입니다. 또는 저장 하도록 선택할 수 있습니다 프로그램 **레코드 집합** 대신 사용 하 여 XML로 아웃 **adPersistXML**합니다. 레코드 집합을 XML로 저장 하는 방법에 대 한 자세한 내용은 참조 [XML 형식의 레코드 지속](../../../ado/guide/data/persisting-records-in-xml-format.md)합니다.  
  
 구문은 **저장** 메서드는 다음과 같습니다.  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 처음으로 저장 하면는 **레코드 집합**를 지정 하는 선택 사항이 *대상*합니다. 생략 하면 *대상*, 새 파일의 값으로 설정 하는 이름으로 생성 됩니다는 [소스](../../../ado/reference/ado-api/source-property-ado-recordset.md) 의 속성은 **레코드 집합**합니다.  
  
 생략 *대상* 이후에 호출 **저장** 후 첫 번째 저장 또는 런타임 오류가 발생 합니다. 않으면 런타임 **저장** 를 새 *대상*, **레코드 집합** 새 대상에 저장 됩니다. 그러나 새 대상 및 원본 대상 둘 다 열려 있을 합니다.  
  
 **저장** 닫지 않습니다는 **레코드 집합** 또는 *대상*계속 작업할 수 있으므로 **레코드 집합** 가장 최근의 변경 내용을 저장 합니다. *대상* 될 때까지 열린 상태로 유지 됩니다는 **레코드 집합** 닫혀 있으며이 기간 동안 다른 응용 프로그램을 읽을 수 있지만에 쓸 *대상*합니다.  
  
 보안상의 이유로 **저장** 메서드는 Microsoft Internet Explorer에서 실행 되는 스크립트에서 낮은 및 사용자 지정 보안 설정의 사용만을 허용 합니다.  
  
 경우는 **저장** 동안 비동기 메서드는 **레코드 집합** 인출, 실행 또는 업데이트 작업이 진행 중인 **저장** 비동기 작업이 될 때까지 대기 완료 합니다.  
  
 레코드의 첫 번째 행부터 저장 되는 **레코드 집합**합니다. 경우는 **저장** 메서드가 완료 되 면 현재 행의 위치가의 첫 번째 행으로 이동 되는 **레코드 집합**합니다.  
  
 최상의 결과 위해 설정 된 [앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient** 와 **저장**합니다. 경우에 공급자가 지원 하지 저장 하는 데 필요한 기능을 모두 **레코드 집합** 개체 커서 서비스에서 해당 기능을 제공 합니다.  
  
 경우는 **레코드 집합** 함께 유지는 **앞** 속성이로 설정 **가 adUseServer**, 업데이트 기능에 대 한는 **레코드 집합**제한 됩니다. 일반적으로 단일 테이블 업데이트, 삽입 및 삭제 (공급자 기능에 따라 다름) 허용 됩니다. [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드는 또한이 구성에서 사용할 수 없습니다.  
  
 때문에 *대상* 지 원하는 OLE DB 개체를 허용할 수 있는 **IStream** 인터페이스를 저장할 수 있습니다는 **레코드 집합** ASP에 직접  **응답** 개체입니다.  
  
 다음 예제에서는 **저장** 및 **열려** 메서드는 유지 하는 데 사용 되는 **레코드 집합** 나중에 다시 열:  
  
```  
'BeginPersist  
   conn.ConnectionString = _  
   "Provider=SQLOLEDB;Data Source=MySQLServer;" _  
      & "Integrated Security=SSPI;Initial Catalog=pubs"  
   conn.Open  
  
   conn.Execute "create table testtable (dbkey int " & _  
      "primary key, field1 char(10))"  
   conn.Execute "insert into testtable values (1, 'string1')"  
  
   Set rst.ActiveConnection = conn  
   rst.CursorLocation = adUseClient  
  
   rst.Open "select * from testtable", conn, adOpenStatic, _  
      adLockBatchOptimistic  
  
   'Change the row on the client  
   rst!field1 = "NewValue"  
  
   'Save to a file--the .dat extension is an example; choose  
   'your own extension. The changes will be saved in the file  
   'as well as the original data.  
   MyFile = Dir("c:\temp\temptbl.dat")  
   If MyFile <> "" Then  
       Kill "c:\temp\temptbl.dat"  
   End If  
  
   rst.Save "c:\temp\temptbl.dat", adPersistADTG  
   Set rst = Nothing  
  
   'Now reload the data from the file  
   Set rst = New ADODB.Recordset  
   rst.Open "c:\temp\temptbl.dat", , adOpenStatic, _  
      adLockBatchOptimistic, adCmdFile  
  
   Debug.Print "After Loading the file from disk"  
   Debug.Print "   Current Edited Value: " & rst!field1.Value  
   Debug.Print "   Value Before Editing: " & rst!field1.OriginalValue  
  
   'Note that you can reconnect to a connection and  
   'submit the changes to the data source  
   Set rst.ActiveConnection = conn  
   rst.UpdateBatch  
'EndPersist  
```  
  
## <a name="remarks"></a>Remarks  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [레코드 집합 지속성에 대한 자세한 정보](../../../ado/guide/data/more-about-recordset-persistence.md)  
  
-   [필터링된 계층적 레코드 집합 유지](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)  
  
-   [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
