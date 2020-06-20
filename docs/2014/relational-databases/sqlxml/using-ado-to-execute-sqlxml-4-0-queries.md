---
title: ADO를 사용하여 SQLXML 4.0 쿼리 실행
ms.custom: ''
ms.date: 12/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- query testers [SQLXML]
- test scripts
- ADO [SQLXML]
- queries [SQLXML], ADO
- SQLXML, ADO
ms.assetid: 3d54e3bb-7c5f-427e-82f8-1403a54c4f53
author: rothja
ms.author: jroth
ms.openlocfilehash: 50fea140fec2b59e1869d8aaf15e37220ac28bd1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065649"
---
# <a name="using-ado-to-execute-sqlxml-40-queries"></a>ADO를 사용하여 SQLXML 4.0 쿼리 실행
  SQLXML의 이전 버전에서는 SQLXML IIS 가상 디렉터리와 SQLXML ISAPI 필터를 사용하여 HTTP 기반 쿼리 실행이 지원되었습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터 SQLXML IIS 가상 디렉터리 및 SQLXML ISAPI 필터와 유사하고 겹치는 기능이 네이티브 XML 웹 서비스와 함께 제공되므로 SQLXML 4.0에서는 이러한 구성 요소가 제거되었습니다.  
  
 또는 MDAC(Microsoft Data Access Components) 2.6 이상에서 처음 도입된 ADO(ActiveX Data Objects)에 대한 SQLXML 확장을 이용하여 쿼리를 실행하고 COM 기반 애플리케이션에서 SQLXML 4.0을 사용할 수 있습니다.  
  
 이 항목에서는 SQLXML 및 ADO를 VBScript(Visual Basic Scripting Edition) 애플리케이션(파일 확장명이 .vbs인 스크립트)의 일부로 사용하는 방법을 보여 줍니다. SQLXML 4.0 설명서의 쿼리 예제를 다시 만들고 테스트하는 데 유용한 초기 설치 절차를 제공합니다.  
  
## <a name="creating-the-sqlxml-40-test-script"></a>SQLXML 4.0 테스트 스크립트 만들기  
 이 절차에서는 ADO 2.6 이상의 SQLXML ADO 확장을 이용하여 SQLXML 쿼리를 실행하는 데 사용할 수 있는 VBScript(.vbs) 파일인 Sqlxml4test.vbs를 만듭니다.  
  
#### <a name="to-create-the-sqlxml-40-query-tester-using-ado-vbscript"></a>ADO를 사용하여 SQLXML 4.0 쿼리 테스터를 만들려면(VBScript)  
  
1.  아래 VBScript 코드를 복사 하 여 텍스트 파일에 붙여 넣습니다. 파일을 Sqlxml4test.vbs로 저장합니다.  
  
    ```vb
    WScript.Echo "Query process may take a few seconds to complete. Please be patient."  
  
    ' Note that for SQL Server Native Client to be used as the data provider,  
    ' it needs to be installed on the client computer first. Also, SQLXML extensions   
    ' for ADO are used and available in MDAC 2.6 or later.  
  
    'Set script variables.  
    inputFile = "@@FILE_NAME@@"  
    strServer = "@@SERVER_NAME@@"  
    strDatabase = "@@DATABASE_NAME@@"  
    dbGuid = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  
    ' Establish ADO connection to SQL Server and   
    ' create an instance of the ADO Command object.  
    Set conn = CreateObject("ADODB.Connection")  
    Set cmd = CreateObject("ADODB.Command")  
    conn.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Server=" & strServer & _  
              ";Database=" & strDatabase & ";Integrated Security=SSPI"  
    Set cmd.ActiveConnection = conn  
  
    ' Create the input stream as an instance of the ADO Stream object.  
    Set inStream = CreateObject("ADODB.Stream")  
    inStream.Open  
    inStream.Charset = "utf-8"  
    inStream.LoadFromFile inputFile  
  
    ' Set ADO Command instance to use input stream.  
    Set cmd.CommandStream = inStream  
  
    ' Set the command dialect.  
    cmd.Dialect = dbGuid  
  
    ' Set a second ADO Stream instance for use as a results stream.   
    Set outStream = CreateObject("ADODB.Stream")  
    outStream.Open  
  
    ' Set dynamic properties used by the SQLXML ADO command instance.   
    cmd.Properties("XML Root").Value = "ROOT"  
    cmd.Properties("Output Encoding").Value = "UTF-8"  
  
    ' Connect the results stream to the command instance and execute the command.  
    cmd.Properties("Output Stream").Value = outStream  
    cmd.Execute , , 1024  
  
    ' Echo cropped/partial results to console.  
    WScript.Echo Left(outStream.ReadText, 1023)  
  
    inStream.Close  
    outStream.Close  
    ```  
  
2.  테스트하려는 예제와 테스트 환경에 대해 다음 스크립트 값을 업데이트합니다.  
  
    -   "`@@FILE_NAME@@`"을 찾아 해당 템플릿 파일 이름으로 바꿉니다.  
  
    -   "`@@SERVER_NAME@@`"을 찾아 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름(예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 로컬로 실행되고 있는 경우 "`(local)`")으로 바꿉니다.  
  
    -   "`@@DATABASE_NAME@@`"을 찾아 데이터베이스 이름(예를 들어 "`AdventureWorks2012`" 또는 "`tempdb`")으로 바꿉니다.  
  
     컴퓨터에 로컬로 다시 만들려는 예제에 대한 특정 지침에 명시된 경우 다른 값을 업데이트합니다.  
  
3.  파일을 저장하고 닫습니다.  
  
4.  컴퓨터에 로컬로 다시 만들려는 예제에 포함되는 XML 템플릿 또는 스키마와 같은 추가 파일을 만들었는지 확인합니다. 이러한 파일은 테스트 스크립트 파일(Sqlxml4test.vbs)을 저장한 디렉터리와 같은 디렉터리에 있어야 합니다.  
  
5.  SQLXML 4.0 테스트 스크립트를 사용하는 방법에 대한 다음 섹션의 지침을 따릅니다.  
  
## <a name="using-the-sqlxml-40-test-script"></a>SQLXML 4.0 테스트 스크립트 사용  
 다음 절차에서는 Sqlxml4test.vbs 파일을 사용하여 이 설명서에서 제공하는 예제 쿼리를 테스트하는 방법에 대해 설명합니다.  
  
#### <a name="to-use-the-sqlxml-40-query-tester"></a>SQLXML 4.0 쿼리 테스터를 사용하려면  
  
1.  다음과 같이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client가 설치되어 있는지 확인합니다.  
  
    1.  **시작** 메뉴에서 **설정**을 가리킨 다음 **제어판**을 클릭 합니다.  
  
    2.  제어판에서 **프로그램 추가/제거** 를 엽니다.  
  
    3.  현재 설치 된 프로그램 목록에서 **Microsoft SQL Server Native Client** 가 목록에 나타나는지 확인 합니다.  
  
        > [!NOTE]  
        >  Native Client를 설치 해야 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 경우 [SQL Server Native Client 설치](../native-client/applications/installing-sql-server-native-client.md)를 참조 하세요.  
  
2.  클라이언트 컴퓨터에 대해 설치된 MDAC 버전이 2.6 이상인지 확인합니다. MDAC 버전 정보를 확인 해야 하는 경우 Microsoft 웹 사이트에서 무료 다운로드로 제공 되는 MDAC 구성 요소 검사기 도구를 사용할 수 있습니다 [https://www.microsoft.com/](https://www.microsoft.com/) . 자세한 내용을 보려면 Microsoft 웹 사이트에서 "MDAC 구성 요소 검사기"를 검색 하십시오.  
  
3.  스크립트를 실행합니다.  
  
     명령줄에서 Cscript.exe를 사용하거나 Sqlxml4test.vbs 파일을 두 번 클릭하여 Windows 스크립트 호스트(WScript.exe)를 호출하면 VBScript 파일을 실행할 수 있습니다.  
  
     스크립트를 실행하면 쿼리 결과를 스크립트 출력으로 반환하고 표시하기까지 스크립트를 실행하는 데 시간이 걸릴 수 있음을 경고하는 메시지가 표시됩니다. 출력이 나타나면 출력 내용을 예제의 예상 출력과 비교합니다.  
  
  
