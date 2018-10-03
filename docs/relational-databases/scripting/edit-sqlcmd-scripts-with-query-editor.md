---
title: 쿼리 편집기로 SQLCMD 스크립트 편집 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server], SQLCMD scripts
- SQLCMD scripts
- modifying scripts
- Query Editor [Database Engine], SQLCMD scripts
- scripts [SQL Server], SQL Server Management Studio
ms.assetid: f77b866d-c330-47c9-9e74-0b8d8dff4b31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3e122c9e9e3df3d6f532a472d41487184c51af64
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47843513"
---
# <a name="edit-sqlcmd-scripts-with-query-editor"></a>쿼리 편집기로 SQLCMD 스크립트 편집
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 편집기를 사용하여 쿼리를 SQLCMD 스크립트로 작성 및 편집할 수 있습니다. 같은 스크립트에서 Windows 시스템 명령과 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 처리해야 하는 경우 SQLCMD 스크립트를 사용합니다.  
  
## <a name="sqlcmd-mode"></a>SQLCMD 모드  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기를 사용하여 SQLCMD 스크립트를 작성하거나 편집하려면 SQLCMD 스크립팅 모드를 설정해야 합니다. 기본적으로 SQLCMD 모드는 쿼리 편집기에서 설정되지 않습니다. 도구 모음에서 **SQLCMD 모드** 아이콘을 클릭하거나 **쿼리** 메뉴에서 **SQLCMD 모드** 를 선택하여 스크립팅 모드를 설정할 수 있습니다.  
  
> [!NOTE]  
>  SQLCMD 모드를 설정하면 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 편집기에서 IntelliSense 및 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 디버거가 해제됩니다.  
  
 쿼리 편집기에서 SQLCMD 스크립트는 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트가 사용하는 것과 동일한 기능을 사용할 수 있습니다. 이러한 기능에는  
  
-   색 구분  
  
-   스크립트 실행  
  
-   원본 제어  
  
-   스크립트 구문 분석  
  
-   Showplan  
  
## <a name="enable-sqlcmd-scripting-in-query-editor"></a>쿼리 편집기에서 SQLCMD 스크립팅 설정  
 활성 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창에 대해 SQLCMD 스크립팅을 설정하려면 다음 절차를 사용합니다.  
  
#### <a name="to-switch-a-database-engine-query-editor-window-to-sqlcmd-mode"></a>데이터베이스 엔진 쿼리 편집기 창을 SQLCMD 모드로 전환하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리[!INCLUDE[ssDE](../../includes/ssde-md.md)]를 클릭하여 새**  쿼리 편집기 창을 엽니다.  
  
2.  **쿼리** 메뉴에서 **SQLCMD 모드**를 클릭합니다.  
  
     쿼리 편집기의 컨텍스트에서 **sqlcmd** 문이 실행됩니다.  
  
3.  **SQL 편집기** 도구 모음의 **사용 가능한 데이터베이스** 목록에서 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]를 선택합니다.  
  
4.  쿼리 편집기 창에 다음 두 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 `!!DIR` **sqlcmd** 문을 입력합니다.  
  
    ```  
    SELECT DISTINCT Type FROM Sales.SpecialOffer;  
    GO  
    !!DIR  
    GO  
    SELECT ProductCategoryID, Name FROM Production.ProductCategory;  
    GO  
    ```  
  
5.  F5 키를 눌러 혼합된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 MS-DOS 문의 전체 섹션을 실행합니다.  
  
     첫 번째 문과 세 번째 문에서 생성된 두 SQL 결과 창을 확인합니다.  
  
6.  **결과** 창에서 **메시지** 탭을 클릭하여 세 문 모두에서 생성된 메시지를 봅니다.  
  
    -   (6개 행 적용됨)  
  
    -   \<디렉터리 정보>  
  
    -   (4개 행 적용됨)  
  
> [!IMPORTANT]  
>  명령줄에서 **sqlcmd** 유틸리티를 실행하면 운영 체제와의 전체 상호 작용이 허용됩니다. **SQLCMD 모드**에서 쿼리 편집기를 사용할 때는 대화형 문을 실행하지 않도록 주의해야 합니다. 쿼리 편집기에는 운영 체제 프롬프트에 응답하는 기능이 없습니다.  
  
 SQLCMD 실행 방법은 [sqlcmd Utility](../../tools/sqlcmd-utility.md)를 참조하거나 SQLCMD 자습서를 따라하십시오.  
  
## <a name="enable-sqlcmd-scripting-by-default"></a>SQLCMD 스크립팅을 기본적으로 설정  
 SQLCMD 스크립팅을 기본적으로 설정하려면 **도구** 메뉴에서 **옵션**을 선택하고 **쿼리 실행**, **SQL Server**를 차례로 확장한 다음 **일반** 페이지를 클릭하고 **기본적으로 SQLCMD 모드로 새 쿼리를 엽니다.** 상자를 선택합니다.  
  
## <a name="writing-and-editing-sqlcmd-scripts"></a>SQLCMD 스크립트 작성 및 편집  
 스크립팅 모드를 설정한 후 SQLCMD 명령과 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 작성할 수 있습니다. 다음 규칙이 적용됩니다.  
  
-   SQLCMD 명령은 줄에서 첫 번째 문이어야 합니다.  
  
-   각 줄에서 SQLCMD 명령이 하나만 허용됩니다.  
  
-   SQLCMD 명령은 주석이나 공백 뒤에 올 수 있습니다.  
  
-   주석 문자 내의 SQLCMD 명령은 실행되지 않습니다.  
  
-   단일 줄 주석 문자는 두 개의 하이픈(`--)` 이며 줄의 시작 부분에 표시되어야 합니다.  
  
-   운영 체제 명령은 두 개의 느낌표(`!!`) 뒤에 와야 합니다. 이중 느낌표 명령은 느낌표 뒤에 있는 문이 `cmd.exe` 명령 처리기를 사용하여 실행되도록 합니다. `!!` 뒤에 있는 텍스트는 매개 변수로 `cmd.exe`에 전달되므로 최종 명령줄은 `"%SystemRoot%\system32\cmd.exe /c <text after !!>"`로 실행됩니다.  
  
-   SQLCMD 명령과 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 분명하게 구분하기 위해 모든 SQLCMD 명령 앞에 콜론(`:`) 접두사가 와야 합니다.  
  
-   `GO` 명령은 접두사 없이 사용하거나 앞에 `!!:`  
  
-   이 올 수 있습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기는 SQLCMD 스크립트의 일부로 정의된 환경 변수 및 변수를 지원하지만 기본 제공 SQLCMD 또는 **osql** 변수는 지원하지 않습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 처리하는 SQLCMD는 변수에 대해 대/소문자를 구분합니다. 예를 들어 PRINT '$(COMPUTERNAME)'는 올바른 결과를 생성하는 반면 PRINT '$(ComputerName)'는 오류를 반환합니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 일반 및 SQLCMD 모드에서의 실행을 위해 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]SqlClient를 사용합니다. 명령줄에서 실행할 경우 SQLCMD는 OLE DB 공급자를 사용합니다. 다른 기본 옵션이 적용될 수 있으므로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] SQLCMD 모드 및 SQLCMD 유틸리티에서 동일한 쿼리를 실행하는 동안 다른 동작이 수행될 수 있습니다.  
  
## <a name="supported-sqlcmd-syntax"></a>지원되는 SQLCMD 구문  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기는 다음 SQLCMD 스크립트 키워드를 지원합니다.  
  
 `[!!:]GO[count]`  
  
 `!! <command>`  
  
 `:exit(statement)`  
  
 `:Quit`  
  
 `:r <filename>`  
  
 `:setvar <var> <value>`  
  
 `:connect server[\instance] [-l login_timeout] [-U user [-P password]]`  
  
 `:on error [ignore|exit]`  
  
 `:error <filename>|stderr|stdout`  
  
 `:out <filename>|stderr|stdout`  
  
> [!NOTE]  
>  `:error` 및 `:out`모두에서 `stderr` 및 `stdout` 은 출력을 메시지 탭으로 보냅니다.  
  
 위에 나열되지 않은 SQLCMD 명령은 쿼리 편집기에서 지원되지 않습니다. 지원되지 않은 SQLCMD 키워드가 포함된 스크립트가 실행되면 쿼리 편집기는 지원되지 않는 각 키워드의 대상에 "Ignoring command *\<무시된 명령*>" 메시지를 보냅니다. 스크립트가 성공적으로 실행되지만 지원되지 않은 명령은 무시됩니다.  
  
> [!CAUTION]  
>  SQLCMD를 명령줄에서 시작하지 않기 때문에 SQLCMD 모드에서 쿼리 편집기를 실행할 때 몇 가지 제한 사항이 있습니다. 변수와 같은 명령줄 매개 변수를 전달할 수 없으며, 쿼리 편집기는 운영 체제 프롬프트에 응답하는 기능이 없으므로 대화형 문을 실행하지 않도록 주의해야 합니다.  
  
## <a name="color-coding-in-sqlcmd-scripts"></a>SQLCMD 스크립트에서 코드 색 구분  
 SQLCMD 스크립팅이 설정되어 있으면 스크립트의 색이 구분됩니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 키워드에 대한 색 구분은 동일하게 유지됩니다. SQLCMD 명령은 회색 배경과 함께 표시됩니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 **sqlcmd** 문을 사용하여 testoutput.txt 출력 파일을 만들고 [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT 문 두 개와 운영 체제 명령 하나를 실행해 현재 디렉터리를 출력합니다. 결과 파일에는 `DIR` 문의 메시지 출력과 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 결과 출력이 차례로 표시됩니다.  
  
```  
:out C:\testoutput.txt  
SELECT @@VERSION As 'Server Version'  
!!DIR  
!!:GO  
SELECT @@SERVERNAME AS 'Server Name'  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sqlcmd Utility](../../tools/sqlcmd-utility.md)  
  
  
