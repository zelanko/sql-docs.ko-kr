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
ms.openlocfilehash: 63323fd8ed18f57a68633dce0525d1d37e4978ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924702"
---
# <a name="persisting-data"></a>데이터 유지
휴대용 컴퓨팅 (예: 랩톱 사용)은 연결 된 상태와 연결이 끊어진 상태에서 실행 될 수 있는 응용 프로그램에 대 한 필요성을 생성 했습니다. ADO는 개발자에 게 클라이언트 커서 **레코드 집합** 을 디스크에 저장 하 고 나중에 다시 로드할 수 있는 기능을 제공 하 여이에 대 한 지원을 추가 했습니다.  
  
 다음을 포함 하 여 이러한 유형의 기능을 사용할 수 있는 몇 가지 시나리오가 있습니다.  
  
-   **여행:** 이동 중에 응용 프로그램을 만들 때 나중에 데이터베이스에 다시 연결 하 고 커밋할 수 있는 새 레코드를 추가 하 고 추가 하는 기능을 제공 하는 것이 중요 합니다.  
  
-   **자주 업데이트 되지 않는 조회:** 일반적으로 응용 프로그램에서 테이블이 조회로 사용 됩니다 (예: 상태 세금 테이블). 자주 업데이트 되지 않으며 읽기 전용입니다. 응용 프로그램이 시작 될 때마다 서버에서이 데이터를 다시 읽는 하는 대신 응용 프로그램은 로컬로 유지 되는 **레코드 집합**에서 데이터를 로드 하기만 하면 됩니다.  
  
 ADO에서 **레코드 집합**을 저장 하 고 로드 하려면 Ado **레코드 집합** 개체에 대해 **레코드 집합. save** 및 **Recordset. Open (,,,, adcmdfile)** 메서드를 사용 합니다.  
  
 **레코드 집합 저장** 메서드를 사용 하 여 디스크의 파일에 ADO **레코드 집합** 을 유지할 수 있습니다. ( **레코드 집합** 을 ADO **Stream** 개체에 저장할 수도 있습니다. **Stream** 개체는이 가이드의 뒷부분에서 설명 합니다. 나중에 **Open** 메서드를 사용 하 여 레코드 집합을 사용할 준비가 되 면 해당 **레코드 집합** 을 다시 열 수 있습니다. 기본적으로 ADO는 독점적 Microsoft Advanced Data TableGram (ADTG) 형식으로 **레코드 집합** 을 저장 합니다. 이 이진 형식은 **AdPersistADTG PersistFormatEnum** 값을 사용 하 여 지정 됩니다. 또는 **Adpersistxml**을 사용 하 여 **레코드 집합** 을 XML로 저장 하도록 선택할 수 있습니다. 레코드 집합을 XML로 저장 하는 방법에 대 한 자세한 내용은 [Xml 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)를 참조 하세요.  
  
 **Save** 메서드의 구문은 다음과 같습니다.  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 처음으로 **레코드 집합**을 저장할 때 *대상을*지정 하는 것이 선택 사항입니다. *Destination*을 생략 하면 **레코드 집합**의 [Source](../../../ado/reference/ado-api/source-property-ado-recordset.md) 속성 값으로 설정 된 이름으로 새 파일이 생성 됩니다.  
  
 첫 번째 저장 또는 런타임 오류가 발생 한 후 나중에 **save** 를 호출할 경우에는 *Destination* 을 생략 합니다. 이후에 새 *대상*으로 **Save** 를 호출 하면 해당 **레코드 집합이** 새 대상에 저장 됩니다. 그러나 새 대상과 원래 대상이 둘 다 열립니다.  
  
 **저장** **은 레코드 집합 또는** *대상을*닫지 않으므로 **레코드 집합** 을 사용 하 여 계속 작업 하 고 최근 변경 내용을 저장할 수 있습니다. *대상* 은 **레코드 집합** 을 닫을 때까지 열린 상태로 유지 됩니다 .이 기간 동안에는 다른 응용 프로그램에서 *대상*에 쓸 수 있지만 쓸 수는 없습니다.  
  
 보안을 위해 **Save** 메서드는 Microsoft Internet Explorer에서 실행 되는 스크립트에서 낮은 및 사용자 지정 보안 설정을 사용 하도록 허용 합니다.  
  
 비동기 **레코드 집합** 페치, 실행 또는 업데이트 작업이 진행 되는 동안 **save** 메서드가 호출 되 면 **저장** 은 비동기 작업이 완료 될 때까지 대기 합니다.  
  
 레코드는 레코드 **집합**의 첫 번째 행부터 저장 됩니다. **Save** 메서드가 완료 되 면 현재 행 위치가 **레코드 집합**의 첫 번째 행으로 이동 합니다.  
  
 최상의 결과를 위해 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성을 **adUseClient** 로 설정 하 고 **Save**를 사용 합니다. 공급자가 **레코드 집합** 개체를 저장 하는 데 필요한 일부 기능을 지원 하지 않는 경우 Cursor Service가 해당 기능을 제공 합니다.  
  
 **CursorLocation** 속성이 **aduseserver**로 설정 된 상태에서 **레코드 집합** 을 유지 하면 **레코드 집합** 에 대 한 업데이트 기능이 제한 됩니다. 일반적으로는 단일 테이블 업데이트, 삽입 및 삭제만 허용 됩니다 (공급자 기능에 따라 다름). 다시 [동기화](../../../ado/reference/ado-api/resync-method.md) 메서드는이 구성 에서도 사용할 수 없습니다.  
  
 *Destination* 매개 변수는 OLE DB **IStream** 인터페이스를 지 원하는 개체를 받아들일 수 있으므로 **레코드 집합** 을 ASP **Response** 개체에 직접 저장할 수 있습니다.  
  
 다음 예제에서는 **저장** 및 **열기** 메서드를 사용 하 여 **레코드 집합** 을 유지 하 고 나중에 다시 엽니다.  
  
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
  
## <a name="remarks"></a>설명  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [레코드 집합 지속성에 대한 자세한 정보](../../../ado/guide/data/more-about-recordset-persistence.md)  
  
-   [필터링된 계층적 레코드 집합 유지](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)  
  
-   [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
