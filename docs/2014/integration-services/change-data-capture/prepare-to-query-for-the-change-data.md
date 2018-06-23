---
title: 변경 데이터에 대한 쿼리 준비 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- incremental load [Integration Services],preparing query
ms.assetid: 9ea2db7a-3dca-4bbf-9903-cccd2d494b5f
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6fc278beec749f8698977a153c30b5c584ea8424
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093816"
---
# <a name="prepare-to-query-for-the-change-data"></a>변경 데이터에 대한 쿼리 준비
  변경 데이터를 증분 로드하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 제어 흐름에서 세 번째이자 마지막 태스크는 변경 데이터 쿼리를 준비하고 데이터 흐름 태스크를 추가하는 것입니다.  
  
> [!NOTE]  
>  제어 흐름에 대한 두 번째 태스크는 선택한 간격에 대한 변경 데이터가 준비되었는지 확인하는 것입니다. 이 태스크에 대한 자세한 내용은 [변경 데이터의 준비 여부 확인](determine-whether-the-change-data-is-ready.md)을 참조하세요. 제어 흐름 디자인의 전체 프로세스에 대한 설명은 [데이터 캡처 변경&#40;SSIS&#41;](change-data-capture-ssis.md)을 참조하세요.  
  
## <a name="design-considerations"></a>디자인 고려 사항  
 변경 데이터를 검색하려면 간격의 끝점을 입력 매개 변수로 받아 지정한 간격에 대한 변경 데이터를 반환하는 Transact-SQL 테이블 반환 함수를 호출합니다. 데이터 흐름의 원본 구성 요소에서 이 함수를 호출합니다. 이 원본 구성 요소에 대한 자세한 내용은 [변경 데이터 검색 및 이해](retrieve-and-understand-the-change-data.md)를 참조하세요.  
  
 OLE DB 원본, ADO 원본 및 ADO NET 원본을 비롯하여 가장 자주 사용되는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 원본 구성 요소는 테이블 반환 함수에 대한 매개 변수 정보를 파생시킬 수 없습니다. 따라서 대부분의 원본은 매개 변수가 있는 함수를 직접 호출할 수 없습니다.  
  
 함수에 입력 매개 변수를 전달하는 데에는 두 개의 디자인 옵션이 있습니다.  
  
-   **매개 변수가 있는 쿼리를 문자열로 조합**. 스크립트 태스크나 SQL 실행 태스크를 사용하여 매개 변수 값이 문자열로 하드 코딩된 동적 SQL 문자열을 조합할 수 있습니다. 그런 다음 이 문자열을 패키지 변수에 저장하고 이를 사용하여 원본 구성 요소의 SqlCommand 속성을 설정할 수 있습니다. 원본 구성 요소에서 더 이상 매개 변수 정보를 필요로 하지 않기 때문에 이 방법이 성공합니다.  
  
    > [!NOTE]  
    >  미리 컴파일된 스크립트는 SQL 실행 태스크보다 적은 오버헤드를 발생시킵니다.  
  
-   **매개 변수가 있는 래퍼 사용**. 매개 변수가 있는 저장 프로시저를 매개 변수가 있는 테이블 반환 함수를 호출하는 래퍼로 만들 수도 있습니다. 원본 구성 요소에서 저장 프로시저에 대한 매개 변수 정보를 파생시킬 수 있기 때문에 이 방법이 성공합니다.  
  
 이 항목에서는 첫 번째 디자인 옵션을 사용하여 매개 변수가 있는 쿼리를 문자열로 조합합니다.  
  
## <a name="preparing-the-query"></a>쿼리 준비  
 입력 매개 변수의 값을 단일 쿼리 문자열로 연결하려면 먼저 쿼리에 필요한 패키지 변수를 설정해야 합니다.  
  
#### <a name="to-set-up-package-variables"></a>패키지 변수를 설정하려면  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 **변수** 창에서 SQL 실행 태스크에서 반환하는 쿼리 문자열을 보관할 string 데이터 형식의 변수를 만듭니다.  
  
     이 예에서는 변수 이름으로 SqlDataQuery를 사용합니다.  
  
 패키지 변수가 만들어지면 스크립트 태스크나 SQL 실행 태스크를 사용하여 입력 매개 변수의 값을 연결할 수 있습니다. 다음 두 절차에서는 이러한 구성 요소를 구성하는 방법에 대해 설명합니다.  
  
#### <a name="to-use-a-script-task-to-concatenate-the-query-string"></a>스크립트 태스크를 사용하여 쿼리 문자열을 연결하려면  
  
1.  **제어 흐름** 탭에서 패키지의 For 루프 컨테이너 뒤에 스크립트 태스크를 추가하고 이 태스크에 For 루프 컨테이너를 연결합니다.  
  
    > [!NOTE]  
    >  이 절차에서는 패키지가 단일 테이블에서 증분 로드를 수행한다고 가정합니다. 패키지가 여러 테이블에서 로드하며 여러 자식 패키지가 있는 부모 패키지를 포함하는 경우 이 태스크는 각 자식 패키지에 첫 번째 구성 요소로 추가됩니다. 자세한 내용은 [여러 테이블의 증분 로드 수행](perform-an-incremental-load-of-multiple-tables.md)을 참조하세요.  
  
2.  **스크립트 태스크 편집기**의 **스크립트** 페이지에서 다음 옵션을 선택합니다.  
  
    1.  **ReadOnlyVariables**에 대해 목록에서 **User::DataReady**, **User::ExtractStartTime**및 **User::ExtractEndTime** 을 선택합니다.  
  
    2.  **ReadWriteVariables**에 대해 목록에서 User::SqlDataQuery를 선택합니다.  
  
3.  **스크립트 태스크 편집기**의 **스크립트** 페이지에서 **스크립트 편집** 을 클릭하여 스크립트 개발 환경을 엽니다.  
  
4.  Main 프로시저에 다음 코드 세그먼트 중 하나를 입력합니다.  
  
    -   C#에서 프로그래밍하는 경우 다음 코드 행을 입력합니다.  
  
        ```  
        int dataReady;  
        System.DateTime extractStartTime;  
        System.DateTime extractEndTime;  
        string sqlDataQuery;  
  
        dataReady = (int)Dts.Variables["DataReady"].Value;  
        extractStartTime = (System.DateTime)Dts.Variables["ExtractStartTime"].Value;  
        extractEndTime = (System.DateTime)Dts.Variables["ExtractEndTime"].Value;  
  
        if (dataReady == 2)  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) + "', '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
        else  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" + ", '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
  
        Dts.Variables["SqlDataQuery"].Value = sqlDataQuery;  
        ```  
  
         \- 또는-  
  
    -   [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]에서 프로그래밍하는 경우 다음 코드 행을 입력합니다.  
  
        ```  
        Dim dataReady As Integer  
        Dim extractStartTime As Date  
        Dim extractEndTime As Date  
        Dim sqlDataQuery As String  
  
        dataReady = CType(Dts.Variables("DataReady").Value, Integer)  
        extractStartTime = CType(Dts.Variables("ExtractStartTime").Value, Date)  
        extractEndTime = CType(Dts.Variables("ExtractEndTime").Value, Date)  
  
        If dataReady = 2 Then  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) & _  
              "', '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        Else  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" & _  
              ", '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        End If  
  
        Dts.Variables("SqlDataQuery").Value = sqlDataQuery  
  
        ```  
  
5.  기본 코드 행을 반환 하는 상태로 둡니다 `DtsExecResult.Success` 에서 스크립트를 실행 합니다.  
  
6.  스크립트 개발 환경 및 **스크립트 태스크 편집기**를 닫습니다.  
  
#### <a name="to-use-an-execute-sql-task-to-concatenate-the-query-string"></a>SQL 실행 태스크를 사용하여 쿼리 문자열을 연결하려면  
  
1.  **제어 흐름** 탭에서 패키지의 For 루프 컨테이너 뒤에 SQL 실행 태스크를 추가하고 이 태스크에 For 루프 컨테이너를 연결합니다.  
  
    > [!NOTE]  
    >  이 절차에서는 패키지가 단일 테이블에서 증분 로드를 수행한다고 가정합니다. 패키지가 여러 테이블에서 로드하며 여러 자식 패키지가 있는 부모 패키지를 포함하는 경우 이 태스크는 각 자식 패키지에 첫 번째 구성 요소로 추가됩니다. 자세한 내용은 [여러 테이블의 증분 로드 수행](perform-an-incremental-load-of-multiple-tables.md)을 참조하세요.  
  
2.  **SQL 실행 태스크 편집기**의 **일반** 페이지에서 다음 옵션을 선택합니다.  
  
    1.  **ResultSet**에 **단일 행**을 선택합니다.  
  
    2.  원본 데이터베이스에 대한 올바른 연결을 구성합니다.  
  
    3.  **SQLSourceType**에 **직접 입력**을 선택합니다.  
  
    4.  **SQLStatement**에 다음 SQL 문을 입력합니다.  
  
        ```  
        declare @ExtractStartTime datetime,  
        @ExtractEndTime datetime,   
        @DataReady int  
  
        select @DataReady = ?,   
        @ExtractStartTime = ?,   
        @ExtractEndTime = ?  
  
        if @DataReady = 2  
        select N'select * from CDCSample.uf_Customer'  
        + N'('''+ convert(nvarchar(30),@ExtractStartTime,120)  
        + ''', '''  
        + convert(nvarchar(30),@ExtractEndTime,120) + ''') '   
        as SqlDataQuery  
        else  
        select N'select * from CDCSample.uf_Customer'  
        + N'(null, '''  
        + convert(nvarchar(30),@ExtractEndTime,120)  
        + ''') '  
        as SqlDataQuery  
  
        ```  
  
        > [!NOTE]  
        >  `else` 절이이 샘플에서 시작 날짜 및 시간에 대 한 null 값을 전달 하 여 변경 데이터의 초기 로드에 대 한 쿼리를 생성 합니다. 이 샘플에서는 변경 데이터 캡처가 설정되기 전에 적용된 변경 내용도 데이터 웨어하우스에 업로드되어야 하는 시나리오를 다루지 않습니다.  
  
3.  **SQL 실행 태스크 편집기** 의 **매개 변수 매핑**페이지에서 다음 매핑을 수행합니다.  
  
    1.  DataReady 변수를 매개 변수 0에 매핑합니다.  
  
    2.  ExtractStartTime 변수를 매개 변수 1에 매핑합니다.  
  
    3.  ExtractEndTime 변수를 매개 변수 2에 매핑합니다.  
  
4.  **SQL 실행 태스크 편집기** 의 **결과 집합**페이지에서 결과 이름을 SqlDataQuery 변수에 매핑합니다.  
  
     결과 이름은 반환된 단일 열의 이름인 SqlDataQuery입니다.  
  
 이전 절차에서는 입력 매개 변수에 대한 하드 코딩된 문자열 값이 있는 쿼리 문자열을 준비하는 태스크를 구성합니다. 다음 코드는 이러한 쿼리 문자열의 예입니다.  
  
 `select * from CDCSample. uf_Customer('2007-06-11 14:21:58', '2007-06-12 14:21:58')`  
  
## <a name="adding-a-data-flow-task"></a>데이터 흐름 태스크 추가  
 패키지의 제어 흐름을 디자인하는 마지막 단계는 데이터 흐름 태스크를 추가하는 것입니다.  
  
#### <a name="to-add-a-data-flow-task-and-complete-the-control-flow"></a>데이터 흐름 태스크를 추가하고 제어 흐름을 완료하려면  
  
-   **제어 흐름** 탭에서 데이터 흐름 태스크를 추가하고 쿼리 문자열을 연결한 태스크를 연결합니다.  
  
## <a name="next-step"></a>다음 단계  
 쿼리 문자열을 준비하고 데이터 흐름 태스크를 구성한 후 다음 단계는 데이터베이스에서 변경 데이터를 검색할 테이블 반환 함수를 만드는 것입니다.  
  
 **다음 항목:** [변경 데이터 검색을 위한 함수 만들기](create-the-function-to-retrieve-the-change-data.md)  
  
  