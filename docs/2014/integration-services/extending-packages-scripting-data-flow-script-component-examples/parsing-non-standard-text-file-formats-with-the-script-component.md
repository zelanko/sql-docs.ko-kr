---
title: 스크립트 구성 요소를 사용하여 비표준 텍스트 파일 형식의 구문 분석 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- text file reading [Integration Services]
- Script component [Integration Services], non-standard text file formats
- transformations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: 1fda034d-09e4-4647-9a9f-e8d508c2cc8f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 381f616ec0732616a7c9c1a5d181e5d1ea002ce6
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58393681"
---
# <a name="parsing-non-standard-text-file-formats-with-the-script-component"></a>스크립트 구성 요소를 사용하여 비표준 텍스트 파일 형식의 구문 분석
  원본 데이터가 비표준 형식으로 정렬된 경우 여러 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 변환을 함께 결합하는 것보다 모든 구문 분석 논리를 단일 스크립트에 통합하는 것이 더 쉬울 수 있습니다.  
  
 [예제 1: 행으로 구분 된 레코드의 구문 분석](#example1)  
  
 [예제 2: 부모와 자식 레코드 분](#example2)  
  
> [!NOTE]  
>  여러 데이터 흐름 태스크 및 여러 패키지에서 쉽게 다시 사용할 수 있는 구성 요소를 만들려면 이 스크립트 구성 요소 예제에 있는 코드를 바탕으로 사용자 지정 데이터 흐름 구성 요소를 만들어 보십시오. 자세한 내용은 [사용자 지정 데이터 흐름 구성 요소 개발](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)을 참조하세요.  
  
##  <a name="example1"></a> 예제 1: 행으로 구분된 레코드의 구문 분석  
 이 예에서는 각 데이터 열이 별도의 줄에 나타나는 텍스트 파일을 가져오고 스크립트 구성 요소를 사용하여 이를 대상 테이블로 구문 분석하는 방법을 보여 줍니다.  
  
 데이터 흐름의 변환으로 사용 하 여 스크립트 구성 요소를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [스크립트 구성 요소를 사용 하 여 동기 변환 만들기](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)고 [는 비동기 만들기 스크립트 구성 요소를 사용 하 여 변환](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)합니다.  
  
#### <a name="to-configure-this-script-component-example"></a>스크립트 구성 요소 예를 구성하려면  
  
1.  다음 원본 데이터가 포함된 **rowdelimiteddata.txt**라는 텍스트 파일을 만들고 저장합니다.  
  
    ```  
    FirstName: Nancy  
    LastName: Davolio  
    Title: Sales Representative  
    City: Seattle  
    StateProvince: WA  
  
    FirstName: Andrew  
    LastName: Fuller  
    Title: Vice President, Sales  
    City: Tacoma  
    StateProvince: WA  
  
    FirstName: Steven  
    LastName: Buchanan  
    Title: Sales Manager  
    City: London  
    StateProvince:  
  
    ```  
  
2.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 열고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결합니다.  
  
3.  대상 데이터베이스를 선택하고 새 쿼리 창을 엽니다. 쿼리 창에서 다음 스크립트를 실행하여 대상 테이블을 만듭니다.  
  
    ```  
    create table RowDelimitedData  
    (  
    FirstName varchar(32),  
    LastName varchar(32),  
    Title varchar(32),  
    City varchar(32),  
    StateProvince varchar(32)  
    )  
  
    ```  
  
4.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]를 열고 ParseRowDelim.dtsx라는 새 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 만듭니다.  
  
5.  패키지에 플랫 파일 연결 관리자를 추가하고 이름을 RowDelimitedData로 지정한 다음 해당 플랫 파일 연결 관리자가 이전 단계에서 만든 rowdelimiteddata.txt 파일에 연결하도록 구성합니다.  
  
6.  패키지에 OLE DB 연결 관리자를 추가하고 해당 연결 관리자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 대상 테이블을 만든 데이터베이스에 연결하도록 구성합니다.  
  
7.  패키지에 데이터 흐름 태스크를 추가하고 SSIS 디자이너의 **데이터 흐름** 탭을 클릭합니다.  
  
8.  데이터 흐름에 플랫 파일 원본을 추가하고 해당 플랫 파일 원본이 RowDelimitedData 연결 관리자를 사용하도록 구성합니다. **플랫 파일 원본 편집기**의 **열** 페이지에서 사용 가능한 단일 외부 열을 선택합니다.  
  
9. 데이터 흐름에 스크립트 구성 요소를 추가하고 이 구성 요소를 변환으로 구성합니다. 플랫 파일 원본의 출력을 스크립트 구성 요소에 연결합니다.  
  
10. 스크립트 구성 요소를 두 번 클릭하여 **스크립트 변환 편집기**를 표시합니다.  
  
11. **스크립트 변환 편집기** 대화 상자의 **입력 열** 페이지에서 사용 가능한 단일 입력 열을 선택합니다.  
  
12. 에 **입 / 출력** 페이지를 **스크립트 변환 편집기**출력 0을 선택 하 고 설정, 해당 `SynchronousInputID` None으로 합니다. 길이가 32이고 문자열 유형이 모두 [DT_STR]인 5개의 출력 열을 만듭니다.  
  
    -   FirstName  
  
    -   LastName  
  
    -   Title  
  
    -   City  
  
    -   StateProvince  
  
13. 에 **스크립트** 페이지를 **스크립트 변환 편집기**, 클릭 **스크립트 편집** 에 나와 있는 코드를 입력 하 고는 `ScriptMain` 예제의 클래스입니다. 스크립트 개발 환경과 **스크립트 변환 편집기**를 닫습니다.  
  
14. 데이트 흐름에 SQL Server 대상을 추가합니다. SQL Server 대상이 OLE DB 연결 관리자와 RowDelimitedData 테이블을 사용하도록 구성합니다. 이 대상에 스크립트 구성 요소의 출력을 연결합니다.  
  
15. 패키지를 실행합니다. 패키지의 실행이 완료되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상 테이블의 레코드를 검사합니다.  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
    Dim columnName As String  
    Dim columnValue As String  
  
    ' Check for an empty row.  
    If Row.Column0.Trim.Length > 0 Then  
        columnName = Row.Column0.Substring(0, Row.Column0.IndexOf(":"))  
        ' Check for an empty value after the colon.  
        If Row.Column0.Substring(Row.Column0.IndexOf(":")).TrimEnd.Length > 1 Then  
            ' Extract the column value from after the colon and space.  
            columnValue = Row.Column0.Substring(Row.Column0.IndexOf(":") + 2)  
            Select Case columnName  
                Case "FirstName"  
                    ' The FirstName value indicates a new record.  
                    Me.Output0Buffer.AddRow()  
                    Me.Output0Buffer.FirstName = columnValue  
                Case "LastName"  
                    Me.Output0Buffer.LastName = columnValue  
                Case "Title"  
                    Me.Output0Buffer.Title = columnValue  
                Case "City"  
                    Me.Output0Buffer.City = columnValue  
                Case "StateProvince"  
                    Me.Output0Buffer.StateProvince = columnValue  
            End Select  
        End If  
    End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
        string columnName;  
        string columnValue;  
  
        // Check for an empty row.  
        if (Row.Column0.Trim().Length > 0)  
        {  
            columnName = Row.Column0.Substring(0, Row.Column0.IndexOf(":"));  
            // Check for an empty value after the colon.  
            if (Row.Column0.Substring(Row.Column0.IndexOf(":")).TrimEnd().Length > 1)  
            // Extract the column value from after the colon and space.  
            {  
                columnValue = Row.Column0.Substring(Row.Column0.IndexOf(":") + 2);  
                switch (columnName)  
                {  
                    case "FirstName":  
                        // The FirstName value indicates a new record.  
                        this.Output0Buffer.AddRow();  
                        this.Output0Buffer.FirstName = columnValue;  
                        break;  
                    case "LastName":  
                        this.Output0Buffer.LastName = columnValue;  
                        break;  
                    case "Title":  
                        this.Output0Buffer.Title = columnValue;  
                        break;  
                    case "City":  
                        this.Output0Buffer.City = columnValue;  
                        break;  
                    case "StateProvince":  
                        this.Output0Buffer.StateProvince = columnValue;  
                        break;  
                }  
            }  
        }  
  
    }  
```  
  
##  <a name="example2"></a> 예제 2: 부모 레코드와 자식 레코드 분할  
 이 예에서는 구분 행 뒤에 부모 레코드 행이 있고 그 뒤에 불특정 개수의 자식 레코드 행이 있는 텍스트 파일을 가져오고 스크립트 구성 요소를 사용하여 이를 올바르게 정규화된 부모 및 자식 대상 테이블로 구문 분석하는 방법을 보여 줍니다. 이 간단한 예는 각각의 부모 및 자식 레코드에 둘 이상의 행 또는 열을 사용하는 원본 파일에 맞게 쉽게 조정할 수 있습니다. 단, 각 레코드의 시작 부분과 끝 부분을 식별할 수 있어야 합니다.  
  
> [!CAUTION]  
>  이 예제는 예시 목적으로만 제공됩니다. 이 예제를 두 번 이상 실행하면 대상 테이블에 중복 키 값이 삽입됩니다.  
  
 데이터 흐름의 변환으로 사용 하 여 스크립트 구성 요소를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [스크립트 구성 요소를 사용 하 여 동기 변환 만들기](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)고 [는 비동기 만들기 스크립트 구성 요소를 사용 하 여 변환](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)합니다.  
  
#### <a name="to-configure-this-script-component-example"></a>스크립트 구성 요소 예를 구성하려면  
  
1.  다음 원본 데이터가 포함된 **parentchilddata.txt**라는 텍스트 파일을 만들고 저장합니다.  
  
    ```  
    **********  
    PARENT 1 DATA  
    child 1 data  
    child 2 data  
    child 3 data  
    child 4 data  
    **********  
    PARENT 2 DATA  
    child 5 data  
    child 6 data  
    child 7 data  
    child 8 data  
    **********  
  
    ```  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 열고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결합니다.  
  
3.  대상 데이터베이스를 선택하고 새 쿼리 창을 엽니다. 쿼리 창에서 다음 스크립트를 실행하여 대상 테이블을 만듭니다.  
  
    ```  
    CREATE TABLE [dbo].[Parents]([ParentID] [int] NOT NULL,  
    [ParentRecord] [varchar](32) NOT NULL,  
     CONSTRAINT [PK_Parents] PRIMARY KEY CLUSTERED   
    ([ParentID] ASC))  
    GO  
    CREATE TABLE [dbo].[Children]([ChildID] [int] NOT NULL,  
    [ParentID] [int] NOT NULL,  
    [ChildRecord] [varchar](32) NOT NULL,  
     CONSTRAINT [PK_Children] PRIMARY KEY CLUSTERED   
    ([ChildID] ASC))  
    GO  
    ALTER TABLE [dbo].[Children] ADD CONSTRAINT [FK_Children_Parents] FOREIGN KEY([ParentID])  
    REFERENCES [dbo].[Parents] ([ParentID])  
  
    ```  
  
4.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 열고 SplitParentChild.dtsx라는 새 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 만듭니다.  
  
5.  패키지에 플랫 파일 연결 관리자를 추가하고 이름을 ParentChildData로 지정한 다음 해당 플랫 파일 연결 관리자가 이전 단계에서 만든 parentchilddata.txt 파일에 연결하도록 구성합니다.  
  
6.  패키지에 OLE DB 연결 관리자를 추가하고 해당 연결 관리자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 대상 테이블을 만든 데이터베이스에 연결하도록 구성합니다.  
  
7.  패키지에 데이터 흐름 태스크를 추가하고 SSIS 디자이너의 **데이터 흐름** 탭을 클릭합니다.  
  
8.  데이터 흐름에 플랫 파일 원본을 추가하고 해당 플랫 파일 원본이 ParentChildData 연결 관리자를 사용하도록 구성합니다. **플랫 파일 원본 편집기**의 **열** 페이지에서 사용 가능한 단일 외부 열을 선택합니다.  
  
9. 데이터 흐름에 스크립트 구성 요소를 추가하고 이 구성 요소를 변환으로 구성합니다. 플랫 파일 원본의 출력을 스크립트 구성 요소에 연결합니다.  
  
10. 스크립트 구성 요소를 두 번 클릭하여 **스크립트 변환 편집기**를 표시합니다.  
  
11. **스크립트 변환 편집기** 대화 상자의 **입력 열** 페이지에서 사용 가능한 단일 입력 열을 선택합니다.  
  
12. 에 **입 / 출력** 페이지의 **스크립트 변환 편집기**출력 0, 이름을 parentrecords로 바꾼 다음을 설정 해당 `SynchronousInputID` None으로 합니다. 다음과 같이 2개의 출력 열을 만듭니다.  
  
    -   부호 있는 4바이트 정수 [DT_I4] 형식의 ParentID(기본 키)  
  
    -   길이가 32인 문자열 [DT_STR] 형식의 ParentRecord  
  
13. 두 번째 출력을 만들고 이름을 ChildRecords로 지정합니다. 새 출력의 `SynchronousInputID`는 이미 없음으로 설정되어 있습니다. 다음과 같이 3개의 출력 열을 만듭니다.  
  
    -   부호 있는 4바이트 정수 [DT_I4] 형식의 ChildID(기본 키)  
  
    -   부호 있는 4바이트 정수 [DT_I4] 형식의 ParentID(외래 키)  
  
    -   길이가 50인 문자열 [DT_STR] 형식의 ChildRecord  
  
14. **스크립트 변환 편집기**의 **스크립트** 페이지에서 **스크립트 편집**을 클릭합니다. `ScriptMain` 클래스에서 이 예에 표시된 코드를 입력합니다. 스크립트 개발 환경과 **스크립트 변환 편집기**를 닫습니다.  
  
15. 데이트 흐름에 SQL Server 대상을 추가합니다. 이 대상에 스크립트 구성 요소의 ParentRecords 출력을 연결하고 해당 대상이 OLE DB 연결 관리자와 Parents 테이블을 사용하도록 구성합니다.  
  
16. 데이트 흐름에 다른 SQL Server 대상을 추가합니다. 이 대상에 스크립트 구성 요소의 ChildRecords 출력을 연결하고 해당 대상이 OLE DB 연결 관리자와 Children 테이블을 사용하도록 구성합니다.  
  
17. 패키지를 실행합니다. 패키지의 실행이 완료되면 두 개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상 테이블에 있는 부모 및 자식 레코드를 검사합니다.  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
    Static nextRowIsParent As Boolean = False  
    Static parentCounter As Integer = 0  
    Static childCounter As Integer = 0  
  
    ' If current row starts with separator characters,  
    '  then following row contains new parent record.  
    If Row.Column0.StartsWith("***") Then  
        nextRowIsParent = True  
    Else  
        If nextRowIsParent Then  
            ' Current row contains parent record.  
            parentCounter += 1  
            Me.ParentRecordsBuffer.AddRow()  
            Me.ParentRecordsBuffer.ParentID = parentCounter  
            Me.ParentRecordsBuffer.ParentRecord = Row.Column0  
            nextRowIsParent = False  
        Else  
            ' Current row contains child record.  
            childCounter += 1  
            Me.ChildRecordsBuffer.AddRow()  
            Me.ChildRecordsBuffer.ChildID = childCounter  
            Me.ChildRecordsBuffer.ParentID = parentCounter  
            Me.ChildRecordsBuffer.ChildRecord = Row.Column0  
        End If  
    End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
    int static_Input0_ProcessInputRow_childCounter = 0;  
    int static_Input0_ProcessInputRow_parentCounter = 0;  
    bool static_Input0_ProcessInputRow_nextRowIsParent = false;  
  
        // If current row starts with separator characters,   
        // then following row contains new parent record.   
        if (Row.Column0.StartsWith("***"))  
        {  
            static_Input0_ProcessInputRow_nextRowIsParent = true;  
        }  
        else  
        {  
            if (static_Input0_ProcessInputRow_nextRowIsParent)  
            {  
                // Current row contains parent record.   
                static_Input0_ProcessInputRow_parentCounter += 1;  
                this.ParentRecordsBuffer.AddRow();  
                this.ParentRecordsBuffer.ParentID = static_Input0_ProcessInputRow_parentCounter;  
                this.ParentRecordsBuffer.ParentRecord = Row.Column0;  
                static_Input0_ProcessInputRow_nextRowIsParent = false;  
            }  
            else  
            {  
                // Current row contains child record.   
                static_Input0_ProcessInputRow_childCounter += 1;  
                this.ChildRecordsBuffer.AddRow();  
                this.ChildRecordsBuffer.ChildID = static_Input0_ProcessInputRow_childCounter;  
                this.ChildRecordsBuffer.ParentID = static_Input0_ProcessInputRow_parentCounter;  
                this.ChildRecordsBuffer.ChildRecord = Row.Column0;  
            }  
        }  
  
    }  
```  
  
![Integration Services 아이콘 (작은)](../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [스크립트 구성 요소를 사용하여 동기 변환 만들기](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
 [스크립트 구성 요소를 사용하여 비동기 변환 만들기](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
  
  
