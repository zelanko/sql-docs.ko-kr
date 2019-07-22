---
title: '방법: CLR 데이터베이스 개체 작업 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.allowsqlclrdebugging
ms.assetid: 4a28d43d-eb5e-444d-aace-5df691f38709
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a8ea668f0672a40e8af6fbb81bbce469652eeb54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119886"
---
# <a name="how-to-work-with-clr-database-objects"></a>방법: CLR 데이터베이스 개체 작업
Transact\-SQL 프로그래밍 언어뿐만 아니라 .NET Framework 언어를 사용하여 데이터를 검색 및 업데이트하는 데이터베이스 개체를 만들 수 있습니다. 관리 코드로 작성된 데이터베이스 개체를 SQL Server CLR(공용 언어 런타임) 데이터베이스 개체라고 합니다. SQL Server에서 호스트되는 CLR 데이터베이스 개체를 사용할 경우의 이점과 Transact\-SQL 및 CLR 중에서 선택하는 방법은 [CLR 통합의 장점](../relational-databases/clr-integration/clr-integration-overview.md) 및 [관리 코드를 사용하여 데이터베이스 개체를 만드는 경우의 이점](https://msdn.microsoft.com/library/k2e1fb36.aspx)을 참조하세요.  
  
SQL Server Data Tools를 사용하는 CLR 데이터베이스 개체를 만들려면 데이터베이스 프로젝트를 만든 후 이 프로젝트에 CLR 데이터베이스 개체를 추가합니다. 이전 버전의 Visual Studio와 달리 별도의 CLR 프로젝트를 만든 후 데이터베이스 프로젝트에서 해당 프로젝트에 대한 참조를 추가할 필요가 없습니다. 데이터베이스 프로젝트를 빌드하고 게시하면 프로젝트의 CLR 개체가 동시에 자동으로 게시됩니다. 게시된 CLR 개체는 다른 데이터베이스 개체와 마찬가지 방식으로 호출하고 실행할 수 있습니다.  
  
CLR 및 CLR 빌드 속성 페이지에는 프로젝트에서 CLR 데이터베이스 개체를 사용하기 위한 여러 설정이 포함되어 있습니다. 특히 CLR 속성 페이지에는 CLR 어셈블리에 대한 사용 권한을 설정할 수 있는 권한 수준 설정이 있습니다. 또한 이 페이지에는 프로젝트에 추가된 CLR 데이터베이스 개체에 대한 DDL을 생성할지 여부를 제어하는 "DDL 생성" 설정도 있습니다. CLR 빌드 속성 페이지에는 프로젝트에서 CLR 코드의 컴파일을 구성하기 위해 설정할 수 있는 모든 컴파일러 옵션이 포함되어 있습니다. 이러한 속성 페이지는 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택하여 액세스할 수 있습니다.  
  
CLR 데이터베이스 개체 디버깅을 사용하도록 설정하려면 **SQL Server 개체 탐색기**를 엽니다. 디버그하려는 CLR 데이터베이스 아티팩트를 포함한 서버를 마우스 오른쪽 단추로 클릭하고 **SQL/CLR 디버깅 허용**을 선택합니다. 경고와 함께 다음과 같은 메시지 상자가 표시됩니다. "디버깅하는 동안 이 서버의 모든 관리되는 스레드가 중지됩니다. 이 서버에서 SQL/CLR 디버깅을 사용하도록 설정하시겠습니까?" CLR 데이터베이스 개체를 디버깅할 때 실행을 중단하면 서버의 모든 스레드가 중단되어 다른 사용자에게 영향을 미치게 됩니다. 따라서 프로덕션 서버에서 CLR 데이터베이스 개체 응용 프로그램을 디버깅하면 안 됩니다. 또한 디버깅을 시작한 후에는 **SQL Server 개체 탐색기**에서 설정을 변경할 수 없습니다. **SQL Server 개체 탐색기**의 변경 내용은 다음에 디버깅 세션을 시작할 때까지 적용되지 않습니다.  
  
CLR 데이터베이스 개체를 작성할 때의 요구 사항에 대한 자세한 내용은 [CLR(공용 언어 런타임) 통합을 사용하여 데이터베이스 개체 작성](https://msdn.microsoft.com/library/ms131046.aspx)을 참조하세요.  
  
> [!WARNING]  
> 다음 절차에서는 [연결된 데이터베이스 개발](../ssdt/connected-database-development.md) 및 [프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md) 섹션의 이전 절차에서 만들어진 엔터티를 사용합니다.  
  
### <a name="to-add-a-clr-database-object-to-your-project"></a>프로젝트에 CLR 데이터베이스 개체를 추가하려면  
  
1.  **솔루션 탐색기**에서 **TradeDev** 데이터베이스 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 선택한 후 **새 항목**을 선택합니다.  
  
2.  **C# SQL CLR** 템플릿을 선택하고 **SQL CLR 사용자 정의 함수**를 선택합니다. 기본 이름을 그대로 사용하고 **추가**를 클릭합니다.  
  
3.  클래스 본문에 다음 코드를 추가합니다. 이 함수는 미국 전화 번호의 유효성을 검사합니다. 미국 전화 번호는 선택적으로 괄호로 묶은 3자리 숫자, 3자리 숫자 집합 및 4자리 숫자 집합 순으로 구성해야 합니다. 예를 들어 (425) 555-0123, 425-555-0123, 425 555 0123 및 1-425-555-0123 같은 형식이 지원됩니다.  
  
    ```  
  
    [SqlFunction(IsDeterministic = true, IsPrecise = true)]  
    public static SqlBoolean validatePhone(SqlString phone)  
    {  
        string aNorthAmericanPhoneNumberPattern = @"^[01]?[- .]?(\([2-9]\d{2}\)|[2-9]\d{2})[- .]?\d{3}[- .]?\d{4}$";  
        if (!phone.IsNull)  
        {  
           Regex regex = new Regex(aNorthAmericanPhoneNumberPattern);  
           return regex.IsMatch(phone.Value);  
        }  
        return true;  
     }  
    ```  
  
4.  `Regex`는 빨간색으로 밑줄이 그어져 있습니다. `Regex`를 마우스 오른쪽 단추로 클릭하고 **해결**을 선택한 후 **using System.Text.RegularExpressions**를 선택합니다.  
  
5.  Microsoft SQL Server 2012 서버 인스턴스에 대해 개발하는 경우에는 이 단계를 건너뛰어도 됩니다. 그렇지 않은 경우 SQL Server 2005 및 SQL Server 2008에서는 .NET Framework 버전 2.0, 3.0 또는 3.5로 작성된 데이터베이스 프로젝트만 지원합니다. .NET 대상 플랫폼이 제대로 설정되어 있는지 확인하려면 **솔루션 탐색기**에서 **TradeDev** 데이터베이스 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **SQLCLR** 속성 페이지에서 **대상 플랫폼**을 **.NET Framework 3.5** 이하로 변경합니다. 마지막 화면에서 **예**를 클릭하여 프로젝트를 닫은 후 다시 엽니다.  
  
6.  **TradeDev** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **빌드**를 선택하여 프로젝트를 빌드합니다.  
  
7.  Suppliers.sql을 두 번 클릭하고 **디자이너 보기**를 선택하여 테이블 디자이너에서 Suppliers 테이블을 엽니다.  
  
8.  열 표의 빈 행을 클릭하여 테이블에 새 열을 추가합니다. **이름** 필드에 **phone**을 입력하고 **데이터 형식**에 **nvarchar (128)** 을 입력한 후 **Null 허용** 필드를 선택된 상태로 둡니다.  
  
9. 컨텍스트 창에서 **CHECK 제약 조건** 노드를 마우스 오른쪽 단추로 클릭하고 **새 CHECK 제약 조건 추가**를 선택합니다.  
  
10. 스크립트 창에서 제약 조건의 기본 정의를 다음과 같이 바꿉니다.  
  
    ```  
    CONSTRAINT [CK_Suppliers_CheckPhone] CHECK (dbo.validatePhone(phone)=1),  
    ```  
  
    이렇게 하면 새 phone 필드에 입력하는 모든 내용이 이전에 추가한 CLR UDF를 사용하여 검사됩니다.  
  
11. F5 키를 눌러 프로젝트를 빌드하고 로컬 데이터베이스에 배포합니다.  
  
### <a name="to-use-clr-database-objects"></a>CLR 데이터베이스 개체를 사용하려면  
  
1.  **SQL Server 개체 탐색기**에서 프로젝트를 배포할 로컬 데이터베이스로 이동합니다.  
  
2.  기본적으로 SQL Server의 CLR 통합은 해제되어 있습니다. CLR 데이터베이스 개체를 사용하려면 CLR 통합을 사용하도록 설정해야 합니다. 이렇게 하려면 sp_configure 저장 프로시저의 "clr enabled" 옵션을 사용합니다. 자세한 내용은 [clr enabled 옵션 항목](../relational-databases/clr-integration/clr-integration-enabling.md)을 참조하세요.  
  
    데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다. 쿼리 창에서 다음 코드를 붙여넣고 **쿼리 실행** 단추를 누릅니다.  
  
    ```  
  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO  
    ```  
  
3.  Suppliers 테이블을 마우스 오른쪽 단추로 클릭하고 **데이터 보기**를 선택합니다.  
  
4.  **id** 및 **name**에 각각 **5** 및 **Contoso**를 입력하고 **Address** 필드를 빈 상태로 둔 다음, **phone**에 **425 3122 1222**를 입력합니다. Tab 키로 **phone** 필드 외부로 이동하면 **phone** 필드에 입력한 내용이 미리 정의된 전화 번호 패턴을 따르는지 확인하는 기존 CHECK 제약 조건과 `INSERT` 문이 충돌한다는 메시지가 나타납니다.  
  
5.  입력 내용을 **425 312 1222**로 변경하고 Tab 키를 눌러 이동합니다. 이번에는 입력이 허용됩니다.  
  
## <a name="see-also"></a>참고 항목  
[CLR 통합의 장점](../relational-databases/clr-integration/clr-integration-overview.md)  
[관리 코드를 사용하여 데이터베이스 개체를 만드는 경우의 이점](https://msdn.microsoft.com/library/k2e1fb36.aspx)  
[CLR(공용 언어 런타임) 통합을 사용하여 데이터베이스 개체 작성](https://msdn.microsoft.com/library/ms131046.aspx)  
  
