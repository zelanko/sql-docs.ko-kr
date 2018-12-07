---
title: 정적 데이터 마스킹 | Microsoft 문서
ms.date: 11/05/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: a62f4ff9-2953-42ca-b7d8-1f8f527c4d66
author: egranet
ms.author: esgranet
manager: ajayj
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 18dd28aeb4c1678b4b6ae454c065d3d96770cb5a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52539110"
---
# <a name="static-data-masking"></a>정적 데이터 마스킹
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

정적 데이터 마스킹은 [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) 18.0 미리 보기 5 이상의 구성 요소입니다. SQL Server Management Studio의 최신 미리 보기는 [여기](../../ssms/download-sql-server-management-studio-ssms.md)에서 다운로드할 수 있습니다. 

![정적 데이터 마스킹](../../relational-databases/security/media/sql-static-data-masking/static_data_masking_intro_image.PNG)


## <a name="what-is-static-data-masking"></a>정적 데이터 마스킹이란? 
정적 데이터 마스킹은 사용자가 데이터베이스의 마스킹된 사본을 만들 수 있게 하는 SQL Server Management Studio 기능입니다. 이 기능은 중요 데이터를 포함하여 팀 또는 다른 조직과의 데이터 공유가 필요한 조직을 위해 개발되었습니다. 

정적 데이터 마스킹은 중요 데이터(마스킹 이전 데이터)를 새 데이터(마스킹 이후 데이터)를 바꾸어 다음 시나리오를 원활하게 진행합니다. 
- 개발 및 테스트 
- 분석 및 비즈니스 보고 
- 문제 해결 
- 컨설턴트, 연구 팀 또는 제3자와 데이터베이스 공유 

아래 예제에서는 작업에서 정적 데이터 마스킹의 작동 방식을 보여 줍니다. 마스킹 전 열에는 사회 보장 번호가 포함되어 있습니다. 마스킹 후 각 사회 보장 번호의 처음 5자리가 임의 생성된 번호로 바뀌었습니다.

| 미국 사회 보장 번호(마스킹 이전)   | 미국 사회 보장 번호(마스킹 이후)  |
| ------------- | ------------- |
| 140-38-9110 | 302-92-9110 |
| 463-34-5535 | 189-70-5535 |
| 116-30-8733 | 201-01-8733 |
| 209-36-1971 | 683-10-1971 |
| 372-38-6948 | 372-38-6948 |
| 267-64-2334 | 100-03-2334 |
| 523-93-4176 | 582-20-4176 |
| 573-91-5137 | 730-20-5137 |
| 612-72-1026 | 369-40-1026 |

정적 데이터 마스킹 사용자는 여러 마스킹 기능 중에서 선택할 수 있습니다. 마스킹 삼수에 따라 마스킹 이전 데이터와 마스킹 이후 데이터 간에 관련도가 높거나, 전혀 관련이 없을 수 있습니다. 순서 섞기를 수행하는 마스킹 기능에서는 마스킹 이전 데이터와 마스킹 이후 데이터 간의 관련도가 높습니다. 

| 미국 사회 보장 번호(마스킹 이전) | 미국 사회 보장 번호(마스킹 이후) |
| ------------- | ------------- |
| 140-38-9110 | 612-72-1026 |  
| 463-34-5535 | 372-38-6948 | 
| 116-30-8733 | 523-93-4176 |
| 209-36-1971 | 209-36-1971 | 
| 372-38-6948 | 140-38-9110 |
| 267-64-2334 | 463-34-5535 | 
| 523-93-4176 | 573-91-5137 | 
| 573-91-5137 | 267-64-2334 | 
| 612-72-1026 | 116-30-8733 |

NULL로 바꾸기를 수행하는 마스킹 기능에서는 마스킹 이전 데이터와 마스킹 이후 데이터 간에 관련이 없습니다. 
 
| 미국 사회 보장 번호(마스킹 이전) | 미국 사회 보장 번호(마스킹 이후) |
| ------------- | ------------- |
| 140-38-9110 | NULL |  
| 463-34-5535 | NULL | 
| 116-30-8733 | NULL |
| 209-36-1971 | NULL | 
| 372-38-6948 | NULL |
| 267-64-2334 | NULL | 
| 523-93-4176 | NULL | 
| 573-91-5137 | NULL | 
| 612-72-1026 | NULL |

## <a name="how-does-static-data-masking-work"></a>정적 데이터 마스킹의 작동 방식
정적 데이터 마스킹은 열 수준에서 발생합니다. 사용자는 자신이 마스킹하려는 열과, 선택한 각 열에 적용할 마스킹 기능을 선택합니다. 여러 가지 마스킹 기능을 선택할 수 있습니다. 이에 대해서는 [마스킹 기능](#masking-functions)에서 자세히 설명합니다. 

그런 다음, 정적 데이터 마스킹은 데이터베이스의 사본을 만듭니다. Azure SQL Database의 경우 복사는 [copy 기능](https://azure.microsoft.com/blog/static-data-masking-preview/)을 통해 수행됩니다. SQL Server의 경우 백업 작업과 이후의 복원 작업을 통해 수행됩니다. 이제 각 열에 대해 정적 데이터 마스킹이 선택한 마스킹 기능에 따라 마스킹 이전 데이터를 마스킹 이후 데이터로 바꾸기 시작합니다. 

바꾸기는 스토리지 수준에서 수행됩니다. 이 때문에 정적 데이터 마스킹 완료 후에는 데이터베이스의 마스킹된 사본에서 마스킹 이전 데이터를 검색할 수 없습니다.

## <a name="how-to-guide"></a>방법 가이드

정적 데이터 마스킹을 실행하는 단계별 가이드는 다음과 같습니다. 
 
1. SQL Server Management Studio를 실행합니다. 데이터베이스에 연결합니다. 왼쪽의 **개체 탐색기** 창에서 데이터베이스 폴더를 펼칩니다. 마스킹하려는 데이터베이스를 마우스 오른쪽 단추로 클릭합니다. **작업**을 마우스 왼쪽 단추로 클릭합니다. **데이터베이스 마스킹... (미리 보기)** 를 마우스 왼쪽 단추로 클릭합니다.
 
 ![작업 메뉴](../../relational-databases/security/media/sql-static-data-masking/task_data_masking.PNG)
 
2. 마스킹 구성 창이 열립니다. 데이터베이스의 모든 테이블이 표시됩니다. 테이블은 스키마로 표시된 다음, 스키마 안에서 사전순으로 정렬됩니다. 
 
 ![사용자 인터페이스](../../relational-databases/security/media/sql-static-data-masking/ui_dropdown.PNG)
 
3. 테이블 이름 옆의 드롭다운 아이콘을 클릭하여 테이블 안의 모든 열 목록을 가져옵니다. 테이블의 각 열에 대해 열의 데이터 형식과 Null 허용 여부가 지정됩니다. Null 허용 열은 NULL 값을 항목으로 받을 수 있는 열입니다. 
 
 ![테이블 드롭다운](../../relational-databases/security/media/sql-static-data-masking/ui_dropdown_column.png)
 
4. 마스킹할 모든 열과 적용할 마스킹 기능을 선택합니다. 사용할 수 있는 마스킹의 유형은 **순서 섞기** 마스킹, **그룹 순서 섞기** 마스킹, **단일 값** 마스킹, **NULL** 마스킹,  **복합 문자열** 마스킹입니다. 
 
 ![마스킹 기능 드롭다운](../../relational-databases/security/media/sql-static-data-masking/masking_functions.PNG)
 
 참고: 이 마스킹 기능 대부분에는 추가 구성 매개 변수가 있습니다. 순서 섞기 마스킹의 경우 정적 데이터 마스킹에서 기본 매개 변수를 제공합니다. 그룹 순서 섞기 마스킹, 단일 값 마스킹 및 복합 문자열 마스킹의 경우 사용자가 구성 매개 변수를 제공해야 합니다. 구성 매개 변수를 변경하거나 제공하려면 **구성...** 옵션을 클릭하고 팝업으로 나타나는 대화 상자에서 매개 변수 대체 값을 지정합니다. 각 마스킹 기능에 대한 자세한 설명은 [마스킹 기능](#masking-functions)에서 제공합니다.
 
 ![마스킹 기능 구성 단추](../../relational-databases/security/media/sql-static-data-masking/masking_functions_configure.png)
 
 마스킹 구성 옵션은 즉시 구성 및 스키마 관련 오류와 경고에 대해 유효성을 검사합니다.  검색된 모든 항목이 아이콘 형태로 왼쪽에 표시되며 마우스를 가져가면 추가 정보가 표시됩니다. 
 
 아래 예제에서는 사용자가 NULL 값을 허용하지 않는 열(NOT NULL 제약 조건)에 NULL 마스킹을 선택했습니다.
 
 ![유효성 검사 메커니즘 오류](../../relational-databases/security/media/sql-static-data-masking/validation_mechanism_error_message.PNG)
 
 아래 예제에서는 사용자가 한 열에 대해서만 그룹 순서 섞기 마스킹을 선택했습니다. 그룹 순서 섞기에는 최소 둘 이상의 열이 필요하므로 경고가 발생합니다. 
 
 ![유효성 검사 메커니즘 경고](../../relational-databases/security/media/sql-static-data-masking/validation_warning.PNG)
 
5. 전체 마스킹 구성을 나중에 사용할 수 있게 XML 파일에 저장할 수 있습니다.  마스킹 기능 구성은 Azure SQL 데이터베이스와 온-프레미스 데이터베이스 간에 동일하지만 저장되는 다른 속성(예: 백업 파일 경로)에는 약간의 차이가 있습니다. 구성을 저장하려면 **구성 저장**을 클릭하고 파일 이름을 입력한 다음, 저장을 클릭합니다.  나중에 사용자가 **구성 로드**를 통해 기존 구성 파일을 로드할 수 있습니다. 열 수가 많은 테이블에는 구성 파일을 사용하는 것이 좋습니다. 
 
 ![구성 파일](../../relational-databases/security/media/sql-static-data-masking/load_save_config.PNG)
 
6. 정적 데이터 마스킹을 사용하면 Static Data Masking이라는 사용자의 **Documents** 폴더를 만들고 로그 파일을 그 안에 배치할 수 있습니다. 로그 파일은 디버깅에 유용할 수 있습니다. 로그 파일의 이름은 구성 창의 맨 아래에 표시됩니다. 
  
 
7. (SQL Server만 해당) 온-프레미스 데이터베이스에서 정적 데이터 마스킹을 운용할 경우 정적 데이터 마스킹이 백업/복원 작업을 수행합니다. **2단계: .BAK 파일 복제 위치**에서 백업 파일이 저장되는 서버의 위치를 제공합니다. 

## <a name="masking-functions"></a>마스킹 기능

### <a name="null-masking"></a>NULL 마스킹

NULL 마스킹은 열의 모든 값을 NULL로 바꿉니다. 열에서 NULL 값을 허용하지 않으면 정적 데이터 마스킹 도구가 오류를 반환합니다. 

### <a name="single-value-masking"></a>단일 값 마스킹

단일 값 마스킹은 열의 모든 값을 단일 고정 값으로 바꾸며 이 값은 사용자가 지정합니다. 입력 형식은 선택한 열의 형식에 관계없이 변환 가능해야 합니다. 값을 지정하려면 **구성...** 을 클릭하고 값을 입력한 다음, **확인**을 클릭합니다. 

![단일 값 마스킹 매개 변수](../../relational-databases/security/media/sql-static-data-masking/single_value_parameter.PNG)


### <a name="shuffle-masking"></a>순서 섞기 마스킹

열의 모든 값의 순서를 섞어 새 행을 만듭니다. 새 데이터가 생성되지 않습니다. 순서 섞기 마스킹은 열에 NULL 항목을 유지하는 옵션을 제공합니다. 이렇게 하려면 **구성...** 을 클릭하고 NULL 유지 배치 확인란을 선택합니다.

![순서 섞기 마스킹 매개 변수](../../relational-databases/security/media/sql-static-data-masking/shuffle_parameter.PNG)

NULL 값이 위치에 유지되지 않았다가 이후 유지되는 순서 섞기 마스킹의 예제는 다음과 같습니다.


| 미국 사회 보장 번호(마스킹 이전) | 미국 사회 보장 번호(마스킹 이후, NULL 항목 순서 섞음) | 미국 사회 보장 번호(마스킹 이후, NULL 항목 순서 섞지 않음) |
| ------------- | ------------- | ------------- |
| 116-30-8733 | 612-72-1026 | 463-34-5535 |
| 140-38-9110 | NULL | 573-91-5137  |
| 209-36-1971 | 523-93-4176 | 140-38-9110 |
| NULL | 209-36-1971 | NULL |
| 463-34-5535 | 140-38-9110 | 116-30-8733  |
| 523-93-4176 | 463-34-5535 | 612-72-1026  |
| NULL | 573-91-5137 | NULL |
| 573-91-5137 | NULL | 523-93-4176 |
| 612-72-1026  | 116-30-8733  | 209-36-1971 |  

### <a name="group-shuffle-masking"></a>그룹 순서 섞기 마스킹
그룹 순서 섞기에서는 여러 열을 하나의 순서 섞기 그룹에 바인딩합니다. 순서 섞기 그룹의 열은 함께 순서가 섞입니다. 사용자는 **구성...** 옵션을 사용하여 순서 섞기 그룹의 이름을 지정해야 합니다.

![그룹 순서 섞기 마스킹 매개 변수](../../relational-databases/security/media/sql-static-data-masking/group_shuffle_parameter.PNG)

그룹 순서 섞기는 동일한 테이블에서 수행됩니다. 같은 순서 섞기 그룹 이름을 여러 테이블에서 사용할 경우 두 그룹 순서 섞기는 별개의 작업입니다. 그룹 이름은 그룹에 포함되는 각각의 열에 대해 동일해야 합니다. 이름은 대/소문자를 구분합니다. 여러 순서 섞기 그룹(이름이 다름)이 한 테이블에 있을 수 있습니다. 

### <a name="string-composite-masking"></a>문자열 복합 마스킹

문자열 복합 마스킹은 패턴과 함께 임의 문자열을 생성합니다. 유효한 입력이 되기 위해 미리 정의된 패턴을 따라야 하는 문자열에 적합합니다. 예를 들어 미국 사회 보장 번호 형식은 123-45-6789입니다. 문자열 복합 마스킹을 위한 구문은 사용자가 패턴을 입력해야 하는 대화 상자에서 지정됩니다.

![문자열 복합 마스킹 매개 변수](../../relational-databases/security/media/sql-static-data-masking/string_composite.PNG)

문자열 복합 마스킹은 클릭하여 테스트할 수 있는 세 가지 예제 패턴을 사용합니다. 전화 번호를 클릭하면 패턴 상자에 임의의 미국 전화 번호 생성에 필요한 식이 자동으로 입력됩니다.

![문자열 복합 마스킹 매개 변수 예제](../../relational-databases/security/media/sql-static-data-masking/string_composite_phone_example.PNG)

문자열 복합 마스킹도 기존 데이터의 하위 부분을 패턴 생성 문자열로 변경할 수 있는 고급 모드입니다. 문자열의 바뀐 부분은 정규식의 캡처 그룹으로 결정합니다. 예를 들어, 이메일의 사용자 이름 부분은 바꾸면서 도메인을 유지하거나 전화 번호를 지역 코드는 남기고 바꿀 수 있습니다. 정규식에 대한 자세한 내용은 [여기](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference)에서 제공합니다.

![고급 문자열 복합 마스킹 매개 변수 예제](../../relational-databases/security/media/sql-static-data-masking/string_composite_advanced.PNG)

문자열 복합 마스킹과 고급 모드는 [데이터 형식](../../t-sql/data-types/data-types-transact-sql.md)이 char, varchar, text, nchar, nvarchar, ntext인 열에서만 사용할 수 있습니다.

## <a name="limitations"></a>제한 사항 

정적 데이터 마스킹에는 다음과 같은 제한 사항이 있습니다.

- 정적 데이터 마스킹은 [임시 테이블](../../relational-databases/tables/temporal-tables.md)이 있는 데이터베이스를 지원하지 않습니다.

- 정적 데이터 마스킹은 [메모리 최적화](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md) 테이블을 마스킹하지 않습니다.

- 정적 데이터 마스킹은 [계산된 열](../../relational-databases/tables/specify-computed-columns-in-a-table.md) 및 [ID](../../t-sql/statements/create-table-transact-sql-identity-property.md) 열을 마스킹하지 않습니다.

- 정적 데이터 마스킹은 Azure SQL 하이퍼스케일 데이터베이스를 지원하지 않습니다.

- 정적 데이터 마스킹은 기하 도형 및 지리 데이터 형식을 지원하지 않습니다. 

정적 데이터 마스킹에는 마스킹 기능에 다음과 같은 세 가지 제한 사항도 있습니다.

- 정적 데이터 마스킹은 [히스토그램 통계](../../relational-databases/statistics/statistics.md)를 업데이트하지 않습니다. 따라서 정적 데이터 마스킹 완료 후에도 데이터베이스의 마스킹된 사본에 히스토그램 통계의 중요 데이터가 남아 있을 수 있습니다. 이 문제를 해결하기 위해 [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md)를 실행할 수 있습니다. 

- 정적 데이터 마스킹이 오류를 반환할 경우 모든 마스킹 작업이 일시 중단됩니다. 데이터베이스의 사본이 삭제되지 않으며 중요 정보를 포함할 수 있습니다. 정적 데이터 마스킹이 오류를 반환했을 때 데이터베이스 사본을 삭제할 책임은 사용자에게 있습니다. 

- (SQL Server만 해당) 정적 데이터 마스킹 완료 후에도 [데이터 파일](../../relational-databases/databases/database-files-and-filegroups.md) 및 [로그 파일](../../relational-databases/logs/the-transaction-log-sql-server.md)이 할당되지 않은 메모리의 일부 중요 데이터를 계속 포함할 수 있습니다. 데이터 파일 및 로그 파일에 대한 액세스 권한이 있다면 이런 중요 데이터를 16진 편집기를 통해 검색할 수 있습니다.

## <a name="see-also"></a>참고 항목  
 [동적 데이터 마스킹](../../relational-databases/security/dynamic-data-masking.md)   
 [SQL Database 정적 데이터 마스킹 시작](https://azure.microsoft.com/documentation/articles/sql-database-static-data-masking-get-started/)  
