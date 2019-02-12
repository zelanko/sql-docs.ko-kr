---
title: DiffGram ADO (SQLXML 4.0)을 사용 하 여 실행 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], SQLOLEDB Provider
- ADO [SQLXML]
- SQLXMLOLEDB Provider, DiffGrams
- data providers [SQLXML], SQLOLEDB Provider
- DiffGrams [SQLXML], ADO
ms.assetid: 741fce82-de83-4923-86eb-30acb5b9a5e6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bedf38e837eec6a061be30f147616bb3d9f28c23
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56019734"
---
# <a name="executing-a-diffgram-by-using-ado-sqlxml-40"></a>ADO를 사용하여 DiffGram 실행(SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  이 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 응용 프로그램은 ADO를 사용하여 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 설정하고 DiffGram을 실행합니다. 이 응용 프로그램에서 DiffGram 및 XSD 스키마는 파일에 저장됩니다. 응용 프로그램은 지정된 파일에서 DiffGram을 로드합니다. Diffgram은 (및 연결된 된 XSD 스키마) 중 하나를 사용할 수 있습니다에 설명 된 [DiffGram 예](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
 다음은 예제 응용 프로그램의 프로세스입니다.  
  
-   **conn** 개체 (**ADODB. 연결**) 특정 서버에서 실행 중인 SQL Server 인스턴스에 대 한 연결을 설정 합니다.  
  
-   합니다 **cmd** 개체 (**ADODB.Command**) 설정된 된 연결에서 실행 합니다.  
  
-   명령 언어가 DBGUID_MSSQLXML로 설정됩니다.  
  
-   DiffGram 명령 스트림에 복사 됩니다 (**strmIn**) 파일에서입니다.  
  
-   명령의 출력 스트림에로 설정 되는 **StrmOut** 개체 (**ADODB 합니다. Stream**) 나타나면 데이터를 반환 합니다.  
  
-   SQLOLEDB 공급자를 사용하면 기본적으로 Sqlxmlx.dll에서 제공되는 Microsoft SQLXML 기능을 사용할 수 있게 됩니다. SQLOLEDB 공급자를 사용 하 여 Sqlxml4.dll를 사용 하는 **SQLXML 버전** 속성 **SQLXML.4.0** SQLOLEDB 공급자에 **연결** 개체입니다.  
  
-   명령(DiffGram)이 실행됩니다.  
  
 예제 응용 프로그램 코드는 다음과 같습니다.  
  
> [!NOTE]  
>  코드에서 연결 문자열에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정해야 합니다.  
  
```  
Private Sub Command1_Click()  
  Dim cmd As New ADODB.Command  
  Dim conn As New ADODB.Connection  
  Dim strmOut As New ADODB.Stream  
  Dim strmIn As New ADODB.Stream  
  
  'Open a connection to SQL Server.  
  conn.Provider = "SQLOLEDB"  
  conn.Open "server=SqlServerName; database=tempdb; Integrated Security=SSPI; "  
  conn.Properties("SQLXML Version") = "SQLXML.4.0"  
  Set cmd.ActiveConnection = conn  
  strmIn.Open  
  strmIn.Charset = "UTF-8"  
  strmIn.LoadFromFile "C:\SomeFilePath\SampleDiffGram.xml"  
  strmIn.Position = 0  
  Set cmd.CommandStream = strmIn  
  
  strmOut.Open  
  cmd.Properties("Output Stream").Value = strmOut  
  cmd.Properties("Output Encoding").Value = "UTF-8"  
  
  cmd.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  cmd.Properties("Mapping Schema") = "C:\SomeFilePath\SampleDiffGram.xml"  
  cmd.Execute , , adExecuteStream  
  strmOut.Position = 0  
  Set cmd = Nothing  
  strmOut.Charset = "UTF-8"  
  strmOut.SaveToFile "C:\DropIt.txt", adSaveCreateOverWrite  
  strmOut.Close  
  Set strmOut = Nothing  
  
End Sub  
```  
  
### <a name="to-test-the-diffgram"></a>DiffGram을 테스트하려면  
  
1.  사용자 컴퓨터의 폴더로 Diffgram과 해당 XSD 스키마 중 하나에 나와 있는 예제 중 하나에서 복사 [DiffGram 예](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
2.  Visual Basic을 열고 표준 EXE 프로젝트를 만듭니다.  
  
3.  프로젝트에 다음 참조를 추가합니다.  
  
    ```  
    Microsoft ActiveX Data Objects 2.8 Library  
    ```  
  
4.  도구 상자에서을 클릭 **단추**, 폼에서 단추를 그립니다.  
  
5.  단추를 두 번 클릭하여 코드를 편집하고 이 항목에서 제공된 응용 프로그램 코드를 추가합니다.  
  
6.  코드에 DiffGram 및 XSD 파일 이름을 지정합니다. 연결 문자열 역시 적절하게 편집합니다.  
  
7.  응용 프로그램을 실행합니다. 실행 결과는 사용자가 실행하는 DiffGram에 따라 다릅니다.  
  
  
