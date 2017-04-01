---
title: "열 매핑(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.columnmapandtransform.f1"
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
caps.latest.revision: 69
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# 열 매핑(SQL Server 가져오기 및 내보내기 마법사)
  복사할 기존 테이블 및 뷰를 선택하거나 제공한 쿼리를 검토한 후 **매핑 편집**을 클릭하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사가 **열 매핑** 대화 상자를 표시합니다. 이 페이지에서 복사한 데이터를 받을 대상 열을 지정하고 구성합니다.  
 
## <a name="screen-shot-of-the-column-mappings-page"></a>열 매핑 페이지의 스크린샷 
 다음 스크린샷은 마법사의 **열 매핑** 대화 상자를 보여 줍니다. 
 
 이 예제에서는 **대상 테이블 만들기**가 선택되어 있으므로 마법사가 새 대상 테이블을 만들려는 것을 볼 수 있습니다. 기본적으로 새 대상 테이블의 각 열은 해당 원본 열과 이름, 데이터 형식 및 속성이 동일합니다. 
  
 ![Column mappings page of the Import and Export Wizard](../../integration-services/import-export-data/media/column-mappings.png "Column mappings page of the Import and Export Wizard")  
  
## <a name="confirm-the-source-and-destination"></a>원본 및 대상 확인  
 **원본**  
 선택한 원본 테이블, 뷰 또는 쿼리를 식별합니다.  
  
 **대상**  
 선택한 대상 테이블 또는 뷰를 식별합니다.  

## <a name="create-a-new-destination-table"></a>새 대상 테이블 만들기
 **대상 테이블/파일 만들기**  
 아직 없는 경우 대상 테이블을 만듭니다.    
  
 **SQL 편집**  
**SQL 편집**을 클릭하여 **테이블 생성 SQL 문** 대화 상자를 엽니다. 기본 CREATE TABLE 문을 사용하거나 용도에 맞게 수정합니다. 이 문을 수동으로 변경할 경우 열 매핑 목록이 변경 내용을 인식하는지 확인해야 합니다. 자세한 내용은 [테이블 생성 SQL 문](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)을 참조하세요.  
  
 > [!TIP] **원본 테이블 및 뷰 선택** 페이지에서 새 대상 테이블을 지정한 경우 **대상 테이블 만들기** 옵션이 자동으로 선택되고 **SQL 편집** 단추가 활성화됩니다. 그러지 않고 대상 테이블을 만들려는 경우 **원본 테이블 및 뷰 선택** 페이지로 돌아가 **대상** 열에 **새** 테이블의 이름을 입력해야 합니다.
>
> **열 매핑** 페이지에서 **대상 테이블 만들기** 옵션 및 **SQL 편집** 단추가 비활성화된 경우 **원본 테이블 및 뷰 선택** 페이지로 돌아가 **대상** 열에 **새** 테이블의 이름을 입력합니다. 새 대상 테이블 또는 테이블을 지정하고 **다음**을 클릭하면 **대상 테이블 만들기** 옵션이 자동으로 선택되고 **열 매핑** 페이지에 **SQL 편집** 단추가 활성화됩니다. **SQL 편집**을 선택하면 **테이블 생성 SQL 문** 대화 상자가 표시됩니다.  

## <a name="specify-options-for-existing-data-in-the-destination"></a>대상의 기존 데이터에 대한 옵션 지정
 **대상 테이블/파일의 행 삭제**  
 새 데이터를 로드하기 전에 기존 테이블에서 데이터를 지울지 여부를 지정합니다.  
  
 **대상 테이블/파일에 행 추가**  
 기존 테이블에 이미 있는 데이터에 새 데이터를 추가할지 여부를 지정합니다.  
  
 **대상 테이블을 삭제하고 다시 만들기**  
 대상 테이블을 덮어쓰려면 이 옵션을 선택합니다. 이 옵션은 마법사를 사용하여 대상 테이블을 만들 때만 사용할 수 있습니다. 마법사에서 만든 패키지를 저장한 다음 해당 패키지를 다시 실행하는 경우에만 대상 테이블이 삭제되고 다시 생성됩니다. 설정을 두 번 이상 테스트하려는 경우 편리한 옵션입니다.
  
 **ID 삽입 가능**  
 원본 데이터의 기존 ID 값을 대상 테이블의 ID 열에 삽입할 수 있게 하려면 이 옵션을 선택합니다. 기본적으로 대상 ID 열에는 일반적으로 이러한 작업을 수행할 수 없습니다.  
  
> [!TIP] 기존 기본 키가 ID 열, 자동 번호 열에 있는 경우 기존 기본 키 값을 유지하려면 일반적으로 이 옵션을 선택해야 합니다.  그러지 않으면 대상 ID 열은 일반적으로 새 값을 할당합니다.  

## <a name="review-column-mappings-and-destination-data-types"></a>열 매핑 및 대상 데이터 형식 검토 
 **매핑**  
 데이터 원본의 각 열이 대상의 열에 매핑되는 방식을 표시합니다.
 
 복사하지 않을 열에 대해서는 **대상** 열에서 **무시**를 선택합니다. 테이블의 모든 열을 복사할 필요가 없습니다.  
 
 ![열 매핑 - 매핑](../../integration-services/import-export-data/media/column-mappings-mappings.png)
  
 **매핑** 목록에는 다음 열이 있습니다.  
  
-    **원본**  
     필요한 경우 변환 설정을 지정할 수 있는 각 원본 열을 봅니다.  
  
-   **대상**  
    매핑된 대상 열을 보거나 다른 열을 선택합니다.
    
    복사 작업 중에 특정 열을 무시할지 여부를 지정합니다. 건너뛰려는 열에 대한 이 열에서 **무시**를 선택하여 열의 하위 집합만 복사할 수 있습니다. 열을 매핑하기 전에 매핑하지 않을 열은 모두 무시해야 합니다.  
  
-   **형식**  
    대상 열의 데이터 형식을 보거나 다른 데이터 형식을 선택합니다.
  
-   **Null 허용**  
    대상 열에 null 값을 허용하는지 여부를 지정합니다.  
  
-   **크기**  
    대상 열의 문자 수(해당하는 경우)를 지정합니다.  
  
-    **전체 자릿수**  
    숫자 자릿수를 참조하는 대상 열의 숫자 데이터 전체 자릿수(해당하는 경우)를 지정합니다.  
  
 -   **소수 자릿수**  
    소수점 이하 자릿수를 참조하는 대상 열의 숫자 데이터 소수 자릿수(해당하는 경우)를 지정합니다.  
  
## <a name="whats-next"></a>다음 단계  
 복사한 데이터를 받을 대상 열을 지정하고 구성한 후 **확인**을 클릭하면 **열 매핑** 대화 상자가 **원본 테이블 및 뷰 선택** 페이지 또는 **플랫 파일 대상 구성** 페이지를 반환합니다. 자세한 내용은 [원본 테이블 및 뷰 선택](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) 또는 [플랫 파일 대상 구성](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)을 참조하세요.  
  
 **매핑** 목록에서 성공하지 않을 수 있는 매핑을 지정한 경우 **열 매핑** 대화 상자가 **데이터 형식 매핑 검토** 페이지를 표시합니다. 이 페이지에서는 경고를 검토하고 변환 옵션을 지정하고 오류 처리 방법도 지정합니다. 자세한 내용은 [데이터 형식 매핑 검토](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)를 참조하세요.  
 
 ## <a name="see-also"></a>참고 항목
[SQL Server 가져오기 및 내보내기 마법사에서 데이터 형식 매핑](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
