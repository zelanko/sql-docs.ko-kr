---
title: Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 반복 | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: a5393c1a-cc37-491a-a260-7aad84dbff68
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6bdcfd84f1b12c48e31bd9d56fe6db3e4155c543
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915429"
---
# <a name="loop-through-excel-files-and-tables-with-a-foreach-loop-container"></a>Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 반복

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  이 항목의 절차에서는 적절한 열거자와 함께 Foreach 루프 컨테이너를 사용하여 폴더 내의 Excel 통합 문서 또는 Excel 통합 문서 내의 테이블을 루핑하는 방법에 대해 설명합니다.  

> [!IMPORTANT]
> Excel 파일 연결 및 Excel 파일에서 데이터를 로드할 때 제한 사항 및 알려진 문제에 대한 자세한 내용은 [SSIS(SQL Server Integration Services)를 통해 Excel로 데이터 로드](../load-data-to-from-excel-with-ssis.md)를 참조하세요.
 
## <a name="to-loop-through-excel-files-by-using-the-foreach-file-enumerator"></a>Foreach File 열거자를 사용하여 Excel 파일을 루핑하려면  
  
1.  루프 반복마다 현재 Excel 경로와 파일 이름을 받을 문자열 변수를 만듭니다. 유효성 검사 문제를 방지하려면 변수의 초기 값으로 유효한 Excel 경로 및 파일 이름을 할당하십시오. 이 절차의 뒷부분에 나오는 예제 식에서는 변수 이름 `ExcelFile`을 사용합니다.  
  
2.  필요에 따라 Excel 연결 문자열의 확장 속성 인수에 대한 값을 보유하는 다른 문자열 변수를 만듭니다. 이 인수는 Excel 버전을 지정하고 첫 번째 행에 열 이름을 포함할지 여부와 가져오기 모드 사용 여부를 결정하는 일련의 값을 포함합니다. 이 절차의 뒷부분에 나오는 예제 식에서는 초기 값 " `ExtProperties`"와 함께 변수 이름`Excel 12.0;HDR=Yes`를 사용합니다.  
  
     확장 속성 인수에 대한 변수를 사용하지 않으면 연결 문자열을 포함하는 식에 해당 변수를 수동으로 추가해야 합니다.  
  
3.  **제어 흐름** 탭에 Foreach 루프 컨테이너를 추가합니다. Foreach 루프 컨테이너를 구성하는 방법에 대한 자세한 내용은 [Foreach 루프 컨테이너 구성](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)을 참조하세요.  
  
4.  **Foreach 루프 편집기**의 **컬렉션** 페이지에서 Foreach 파일 열거자를 선택하고, Excel 통합 문서가 있는 폴더를 지정한 다음, 파일 필터(일반적으로 *.xlsx)를 지정합니다.  
  
5.  **변수 매핑** 페이지에서 루프 반복마다 현재 Excel 경로 및 파일 이름을 받는 사용자 정의 문자열 변수에 인덱스 0을 매핑합니다. 이 절차의 뒷부분에 나오는 샘플 식에서는 변수 이름 `ExcelFile`을 사용합니다.  
  
6.  **Foreach 루프 편집기**를 닫습니다.  
  
7.  [패키지에서 연결 관리자 추가, 삭제 또는 공유](https://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)에 설명된 대로 패키지에 Excel 연결 관리자를 추가합니다. 연결에 기존 Excel 통합 문서 파일을 선택하면 유효성 검사 오류를 방지할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  이 Excel 연결 관리자 관리자를 사용하는 태스크 및 데이터 흐름 구성 요소를 구성할 때 유효성 검사 오류가 발생하지 않도록 하려면 **Excel 연결 관리자 편집기**에서 기존 Excel 통합 문서를 선택합니다. 다음 단계에서 설명하는 대로 **ConnectionString** 속성에 대한 식을 구성하고 나면 연결 관리자는 런타임에 이 통합 문서를 사용하지 않습니다. 패키지를 만들고 구성한 다음에는 속성 창에서 **ConnectionString** 속성 값을 지울 수 있습니다. 그러나 이 값을 지우면 Foreach 루프가 실행될 때까지는 Excel 연결 관리자의 연결 문자열 속성이 유효하지 않게 됩니다. 따라서 연결 관리자가 사용된 태스크나 패키지에서 **DelayValidation** 속성을 **True** 로 설정하여 유효성 검사 오류를 방지해야 합니다.  
    >   
    >  또한 Excel 연결 관리자의 **False** 속성에 기본값 **RetainSameConnection** 를 사용해야 합니다. 이 값을 **True**로 변경하면 루프의 각 반복에서 계속해서 첫 번째 Excel 통합 문서를 엽니다.  
  
8.  새 Excel 연결 관리자를 선택하고 속성 창에서 **Expressions** 속성을 클릭한 다음 줄임표를 클릭합니다.  
  
9. **속성 식 편집기**에서 **ConnectionString** 속성을 선택하고 줄임표를 클릭합니다.  
  
10. 식 작성기에서 다음 식을 입력합니다.  
  
    ```  
    "Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=\"" + @[User::ExtProperties] + "\""  
    ```  
  
     확장 속성 인수의 값을 묶는 내부 따옴표를 닫는 데 이스케이프 문자 "\\"가 사용되었다는 것에 유의하세요.  
  
     확장 속성 인수는 필수입니다. 해당 값을 포함하는 변수를 사용하지 않으면 다음 예제처럼 식에 해당 변수를 수동으로 추가해야 합니다.  
  
    ```  
    "Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=Excel 12.0"  
    ```  
  
11. Excel 연결 관리자를 사용하는 Foreach 루프 컨테이너 내에 태스크를 만들어 지정된 파일 위치 및 패턴과 일치하는 각 Excel 통합 문서에 같은 작업을 수행합니다.  
  
## <a name="to-loop-through-excel-tables-by-using-the-foreach-adonet-schema-rowset-enumerator"></a>Foreach ADO.NET 스키마 행 집합 열거자를 사용하여 Excel 테이블을 루핑하려면  
  
1.  Microsoft ACE OLE DB 공급자를 사용하는 ADO.NET 연결 관리자를 만들어 Excel 통합 문서에 연결합니다. **연결 관리자** 대화 상자의 모든 페이지에서 Excel 버전을 확장 속성의 값으로 입력합니다(이 경우에 Excel 12.0). 자세한 내용은 [패키지에서 연결 관리자 추가, 삭제 또는 공유](https://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)을 참조하세요.  
  
2.  루프 반복마다 현재 테이블의 이름을 받을 문자열 변수를 만듭니다.  
  
3.  **제어 흐름** 탭에 Foreach 루프 컨테이너를 추가합니다. Foreach 루프 컨테이너를 구성하는 방법에 대한 자세한 내용은 [Foreach 루프 컨테이너 구성](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)을 참조하세요.  
  
4.  **Foreach 루프 편집기** 의 **컬렉션**페이지에서 Foreach ADO.NET 스키마 행 집합 열거자를 선택합니다.  
  
5.  **연결**값으로 앞에서 만든 ADO.NET 연결 관리자를 선택합니다.  
  
6.  **스키마**값으로 테이블을 선택합니다.  
  
    > [!NOTE]  
    >  Excel 통합 문서의 테이블 목록에는 워크시트($ 접미사를 가짐)와 명명된 범위가 모두 포함됩니다. 워크시트 또는 명명된 범위 목록만 필터링해야 하는 경우 스크립트 태스크에 이를 위한 사용자 지정 코드를 작성해야 합니다. 자세한 내용은 [스크립트 태스크를 사용 하 여 Excel 파일 작업](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)합니다.  
  
7.  **변수 매핑** 페이지에서 현재 테이블 이름을 포함하도록 앞에서 만든 문자열 변수에 인덱스 2를 매핑합니다.  
  
8.  **Foreach 루프 편집기**를 닫습니다.  
  
9. Excel 연결 관리자를 사용하는 Foreach 루프 컨테이너 내에 태스크를 만들어 지정된 통합 문서의 각 Excel 테이블에 같은 작업을 수행합니다. 스크립트 태스크를 사용하여 열거된 테이블 이름을 검사하거나 각 테이블을 작업할 경우에는 스크립트 태스크의 ReadOnlyVariables 속성에 문자열 변수를 추가해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SSIS(SQL Server Integration Services)를 통해 Excel에서 데이터 로드](../load-data-to-from-excel-with-ssis.md)  
 [Foreach 루프 컨테이너 구성](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)   
 [속성 식 추가 또는 변경](../../integration-services/expressions/add-or-change-a-property-expression.md)   
 [Excel 연결 관리자](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Excel 원본](../../integration-services/data-flow/excel-source.md)   
 [Excel 대상](../../integration-services/data-flow/excel-destination.md)   
 [스크립트 태스크를 사용한 Excel 파일 작업](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  
