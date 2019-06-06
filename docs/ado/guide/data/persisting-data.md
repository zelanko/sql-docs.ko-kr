---
title: 데이터 유지 | Microsoft Docs
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
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0f2d47229b7383c11740ca3d7a20ad8e420931a5
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700478"
---
# <a name="persisting-data"></a>데이터 유지
(예: 랩톱), 이식 가능한 컴퓨팅 연결 및 연결이 끊긴 상태에서 실행할 수 있는 응용 프로그램에 대 한 필요 하 게 되었습니다. ADO는 개발자에 게 클라이언트 커서를 저장 하는 기능을 제공 하 여이 대 한 지원을 추가 했습니다 **레코드 집합** 디스크를 나중에 다시 로드 합니다.  
  
 일부의 시나리오는이 유형의 다음과 같은 기능을 사용할 수 있습니다.  
  
-   **이동:** 이동 중에 응용 프로그램을 수행 하는 경우 변경 하 고 다음 나중에 데이터베이스에 다시 연결 하 고 수 있는 커밋된 새 레코드를 추가 하는 기능을 제공 하는 중요 한 것입니다.  
  
-   **조회를 자주 업데이트 합니다.** 응용 프로그램에서 테이블은 흔히 조회로-예를 들어 세금 테이블 상태입니다. 자주 업데이트 되 고 읽기 전용. 응용 프로그램이 시작 될 때마다 서버에서이 데이터를 읽고, 대신 응용 프로그램 단순히 데이터를 로드할 수에서 로컬로 지속형 **레코드 집합**합니다.  
  
 Ado에서 저장 하 고 로드할 **레코드 집합**를 사용 합니다 **Recordset.Save** 및 **Recordset.Open(,,,adCmdFile)** ADO 메서드 **레코드 집합**개체입니다.  
  
 사용할 수는 **레코드 집합 저장** 에 ADO를 유지 하는 방법 **레코드 집합** 파일을 디스크에 있습니다. (저장할 수도 있습니다는 **Recordset** ADO를 **Stream** 개체입니다. **Stream** 개체는이 가이드 뒷부분에서 설명 합니다.) 나중에 사용할 수 있습니다는 **열려** 다시 여는 메서드는 **레코드 집합** 사용할 준비가 되 면 합니다. ADO 기본적으로 저장 합니다 **레코드 집합** 고유 Microsoft 고급 데이터 테이블 그램 (ADTG) 형식입니다. 이 이진 형식을 사용 하 여 지정 된 **adPersistADTG PersistFormatEnum** 값입니다. 또는 저장을 선택할 수 있습니다 하 **Recordset** 대신 사용 하 여 XML로 아웃 **adPersistXML**. 레코드 집합을 XML로 저장 하는 방법에 대 한 자세한 내용은 참조 하세요. [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)합니다.  
  
 구문의 합니다 **저장할** 메서드는 다음과 같습니다.  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 처음 저장할 때 합니다 **레코드 집합**를 지정 하는 선택 사항이 *대상*합니다. 생략 하면 *대상*의 값으로 설정 하는 이름의 새 파일이 만들어집니다는 [원본](../../../ado/reference/ado-api/source-property-ado-recordset.md) 속성을 **레코드 집합**합니다.  
  
 생략 *대상* 이후에 호출 하는 경우 **저장** 후 첫 번째 저장 또는 런타임 오류가 발생 합니다. 이후에 호출 하는 경우 **저장할** 새 *대상*의 **레코드 집합** 새 대상에 저장 됩니다. 그러나 새로운 대상 이자 원래 대상은 둘 다 열어야 합니다.  
  
 **저장** 닫지 않습니다를 **레코드 집합** 또는 *대상*이므로 사용 하 여 작업을 계속할 수는 **레코드 집합** 가장 최근의 변경 내용을 저장 합니다. *대상* 될 때까지 열린 상태로 유지 됩니다 합니다 **레코드 집합** 닫혀이 시간 동안 다른 응용 프로그램 읽을 수 있지만 쓸 *대상*합니다.  
  
 보안을 위해 합니다 **저장할** 메서드는 Microsoft Internet Explorer에서 실행 하는 스크립트에서 낮은 및 사용자 지정 보안 설정의 사용만을 허용 합니다.  
  
 경우는 **저장** 메서드는 비동기 하는 동안 **레코드 집합** 인출, 실행 또는 업데이트 작업이 진행에서 **저장** 비동기 작업이 될 때까지 대기 완료 합니다.  
  
 첫 번째 행부터 레코드가 저장 되는 **레코드 집합**합니다. 경우는 **저장** 메서드가 완료 되 면 현재 행 위치가 첫 번째 행으로 이동 합니다 **레코드 집합**합니다.  
  
 최상의 결과 설정 합니다 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient** 사용 하 여 **저장**합니다. 경우 공급자에 게 지원 하지 않습니다 모든 기능을 저장 하는 데 필요한 **레코드 집합** 개체 커서 서비스에서 해당 기능을 제공 합니다.  
  
 경우는 **레코드 집합** 함께 유지 되는 **CursorLocation** 속성이로 설정 **가 adUseServer**, 업데이트 기능을 **레코드집합**제한 됩니다. 일반적으로 단일 테이블 업데이트, 삽입 및 삭제 (공급자 기능에 따라 다름) 수만 있습니다. 합니다 [Resync](../../../ado/reference/ado-api/resync-method.md) 메서드는 또한이 구성에서 사용할 수 있습니다.  
  
 때문에 *대상* OLE DB를 지 원하는 모든 개체를 허용할 수 있는 **IStream** 인터페이스를 저장할 수 있습니다를 **Recordset** ASP에 직접  **응답** 개체입니다.  
  
 다음 예제에서는 **저장** 및 **열려** 메서드를 유지 하는 데 사용 됩니다는 **레코드 집합** 나중에 다시 열:  
  
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
