---
title: "Transact-SQL 코드 조각 추가 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 901c7995-8eb5-4d12-8bb0-de0a922b48f8
caps.latest.revision: "9"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: dd782cbd60c23d139a980bbf943b158cb38561b3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="add-transact-sql-snippets"></a>Transact-SQL 코드 조각 추가
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함된 미리 정의된 코드 조각 집합에 사용자 고유의 Transact-SQL 코드 조각을 추가할 수 있습니다.  
  
## <a name="creating-a-transact-sql-snippet-file"></a>Transact-SQL 코드 조각 파일 만들기  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드 조각을 만드는 첫 번째 단계는 사용자 코드 조각의 텍스트가 포함된 XML 파일을 만드는 것입니다. 이 파일은 파일 확장명이 .snippet이고 [코드 조각 스키마](http://go.microsoft.com/fwlink/?LinkId=207504)의 요구 사항을 충족해야 합니다. 코드 조각 언어는 SQL로 설정합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 함께 제공되는 미리 정의된 코드 조각을 예로 사용할 수 있습니다. 미리 정의된 코드 조각을 찾으려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 열고 **도구** 메뉴를 선택한 다음 **코드 조각 관리자**를 클릭합니다. **언어** 목록 상자에서 **SQL** 을 선택하면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드 조각의 경로가 **위치** 상자에 표시됩니다.  
  
## <a name="registering-the-code-snippet"></a>코드 조각 등록  
 코드 조각 파일을 만든 후에는 코드 조각 관리자를 사용하여 코드 조각을 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 등록합니다. 여러 코드 조각이 들어 있는 폴더를 추가하거나 개별 코드 조각을 **내 코드 조각** 폴더로 가져올 수 있습니다.  
  
## <a name="procedures"></a>절차  
  
#### <a name="adding-a-snippet-folder"></a>코드 조각 폴더 추가  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다.  
  
2.  **도구** 메뉴를 선택하고 **코드 조각 관리자**를 클릭합니다.  
  
3.  **추가** 단추를 클릭합니다.  
  
4.  코드 조각이 들어 있는 폴더로 이동하고 **폴더 선택** 단추를 클릭합니다.  
  
#### <a name="importing-a-snippet"></a>코드 조각 가져오기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다.  
  
2.  **도구** 메뉴를 선택하고 **코드 조각 관리자**를 클릭합니다.  
  
3.  **가져오기** 단추를 클릭합니다.  
  
4.  코드 조각이 들어 있는 폴더로 이동하고 .snippet 파일을 클릭한 다음 **열기** 단추를 클릭합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **TRY-CATCH** 코드 감싸기 조각을 만들어 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]로 가져옵니다.  
  
1.  다음 코드를 메모장에 붙여 넣은 다음 TryCatch.snippet이라는 파일로 저장합니다.  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">  
    <_locDefinition xmlns="urn:locstudio">  
        <_locDefault _loc="locNone" />  
        <_locTag _loc="locData">Title</_locTag>  
        <_locTag _loc="locData">Description</_locTag>  
        <_locTag _loc="locData">Author</_locTag>  
        <_locTag _loc="locData">ToolTip</_locTag>  
       <_locTag _loc="locData">Default</_locTag>  
    </_locDefinition>  
    <CodeSnippet Format="1.0.0">  
    <Header>  
    <Title>TryCatch</Title>  
                            <Shortcut></Shortcut>  
    <Description>Example Snippet for Try-Catch.</Description>  
    <Author>SQL Server Books Online Example</Author>  
    <SnippetTypes>  
                                    <SnippetType>SurroundsWith</SnippetType>  
    </SnippetTypes>  
    </Header>  
    <Snippet>  
    <Declarations>  
                                    <Literal>  
                                    <ID>CatchCode</ID>  
                                    <ToolTip>Code to handle the caught error</ToolTip>  
                                    <Default>CatchCode</Default>  
                                    </Literal>  
    </Declarations>  
    <Code Language="SQL"><![CDATA[  
    BEGIN TRY  
  
    $selected$ $end$  
  
    END TRY  
    BEGIN CATCH  
  
    $CatchCode$  
  
    END CATCH;  
    ]]>  
    </Code>  
    </Snippet>  
    </CodeSnippet>  
    </CodeSnippets>  
    ```  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다.  
  
3.  **도구** 메뉴를 선택하고 **코드 조각 관리자**를 클릭합니다.  
  
4.  **가져오기** 단추를 클릭합니다.  
  
5.  TryCatch.snippet이 들어 있는 폴더로 이동하고 TryCatch.snippet 파일을 클릭한 다음 **열기** 단추를 클릭합니다. **내 코드 조각** 폴더에 TryCatch 코드 조각이 없어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [코드 감싸기 Transact-SQL 조각 삽입](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
  
  
