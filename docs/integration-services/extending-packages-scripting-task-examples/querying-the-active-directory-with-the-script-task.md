---
title: "스크립트 태스크를 사용하여 Active Directory 쿼리 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-task-examples
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs: VB
helpviewer_keywords:
- Script task [Integration Services], Active Directory access
- SSIS Script task, Active Directory access
- Script task [Integration Services], examples
- Active Directory [Integration Services]
ms.assetid: a88fefbb-9ea2-4a86-b836-e71315bac68e
caps.latest.revision: "51"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0328b2eeaa94e279a53b45e8e205c1356768e53d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="querying-the-active-directory-with-the-script-task"></a>스크립트 태스크를 사용하여 Active Directory 쿼리
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지와 같은 엔터프라이즈 데이터 처리 응용 프로그램에서는 Active Directory에 저장된 직원의 직급, 직함 또는 기타 특징에 따라 데이터를 각기 다르게 처리해야 하는 경우가 종종 있습니다. Active Directory는 사용자에 대한 메타데이터뿐 아니라 컴퓨터 및 프린터와 같은 조직의 기타 자산에 대한 메타데이터도 저장하는 중앙 저장소를 제공하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 디렉터리 서비스입니다. Microsoft .NET Framework의 **System.DirectoryServices** 네임스페이스에서는 Active Directory에 저장된 정보에 따라 데이터 처리 워크플로를 제어할 수 있도록 Active Directory 작업을 위한 클래스를 제공합니다.  
  
> [!NOTE]  
>  여러 패키지에서 쉽게 다시 사용할 수 있는 태스크를 만들려면 이 스크립트 태스크 예제에 있는 코드를 바탕으로 사용자 지정 태스크를 만들어 보십시오. 자세한 내용은 [사용자 지정 태스크 개발](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  
  
## <a name="description"></a>Description  
 다음 예에서는 직원의 전자 메일 주소가 들어 있는 `email` 변수의 값에 따라 Active Directory에서 직원의 이름, 직함 및 전화 번호를 검색합니다. 패키지의 선행 제약 조건에서는 검색된 정보를 사용하여 직원의 직함에 따라 낮은 우선 순위의 전자 메일 메시지를 보낼지 높은 우선 순위의 페이지를 보낼지와 같은 사항을 결정합니다.  
  
#### <a name="to-configure-this-script-task-example"></a>이 스크립트 태스크 예를 구성하려면  
  
1.  `email`, `name` 및 `title`이라는 세 개의 문자열 변수를 만듭니다. `email` 변수 값으로 올바른 회사 전자 메일 주소를 입력합니다.  
  
2.  **스크립트 태스크 편집기**의 **스크립트** 페이지에서 **ReadOnlyVariables** 속성에 `email` 변수를 추가합니다.  
  
3.  **ReadWriteVariables** 속성에 `name` 및 `title` 변수를 추가합니다.  
  
4.  스크립트 프로젝트에서 **System.DirectoryServices** 네임스페이스에 대한 참조를 추가합니다.  
  
5.  의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다. 코드에서 **Imports** 문을 사용하여 **DirectoryServices** 네임스페이스를 가져옵니다.  
  
> [!NOTE]  
>  이 스크립트를 성공적으로 실행하려면 회사 네트워크에서 Active Directory가 사용되고 있고 이 예에서 사용하는 직원 정보가 회사에 저장되어 있어야 합니다.  
  
### <a name="code"></a>코드  
  
```vb  
Public Sub Main()  
  
    Dim directory As DirectoryServices.DirectorySearcher  
    Dim result As DirectoryServices.SearchResult  
    Dim email As String  
  
    email = Dts.Variables("email").Value.ToString  
  
    Try  
        directory = New _  
            DirectoryServices.DirectorySearcher("(mail=" & email & ")")  
        result = directory.FindOne  
        Dts.Variables("name").Value = _  
            result.Properties("displayname").ToString  
        Dts.Variables("title").Value = _  
            result.Properties("title").ToString  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, _  
            "Script Task Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
public void Main()  
{  
    //  
    DirectorySearcher directory;  
    SearchResult result;  
    string email;  
  
    email = (string)Dts.Variables["email"].Value;  
  
    try  
    {  
        directory = new DirectorySearcher("(mail=" + email + ")");  
        result = directory.FindOne();  
        Dts.Variables["name"].Value = result.Properties["displayname"].ToString();  
        Dts.Variables["title"].Value = result.Properties["title"].ToString();  
        Dts.TaskResult = (int)ScriptResults.Success;  
    }  
    catch (Exception ex)  
    {  
        Dts.Events.FireError(0, "Script Task Example", ex.Message + "\n" + ex.StackTrace, String.Empty, 0);  
        Dts.TaskResult = (int)ScriptResults.Failure;  
    }  
  
}  
```  
  
## <a name="external-resources"></a>외부 리소스  
  
-   social.technet.microsoft.com의 기술 문서 [SSIS에서 Active Directory 정보 처리](http://go.microsoft.com/fwlink/?LinkId=199588)  
  
  
