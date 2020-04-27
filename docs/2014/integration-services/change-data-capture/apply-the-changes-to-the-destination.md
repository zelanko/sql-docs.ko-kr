---
title: 대상에 변경 내용 적용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],applying changes
ms.assetid: 338a56db-cb14-4784-a692-468eabd30f41
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fe555d94eb8e00cddd147c2424d0cf60e1d47b34
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62771619"
---
# <a name="apply-the-changes-to-the-destination"></a>대상에 변경 내용 적용
  변경 데이터를 증분 로드하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 데이터 흐름에서 세 번째이자 마지막 태스크는 대상에 변경 내용을 적용하는 것입니다. 삽입을 적용할 구성 요소, 업데이트를 적용할 구성 요소 및 삭제를 적용할 구성 요소가 필요합니다.  
  
> [!NOTE]  
>  변경 데이터를 증분 로드하는 패키지의 데이터 흐름을 디자인하는 두 번째 태스크는 삽입, 업데이트 및 삭제를 구분하는 것입니다. 이 구성 요소에 대한 자세한 내용은 [삽입, 업데이트 및 삭제 처리](process-inserts-updates-and-deletes.md)를 참조하세요. 변경 데이터를 증분 로드하는 패키지를 만드는 전체 프로세스에 대한 설명은 [변경 데이터 캡처&#40;SSIS&#41;](change-data-capture-ssis.md)를 참조하세요.  
  
## <a name="applying-inserts"></a>삽입 적용  
 삽입을 적용하려면 새 행을 특수한 방식으로 처리할 필요가 없으므로 OLE DB 대상을 사용합니다.  
  
#### <a name="to-process-inserts-by-using-an-ole-db-destination"></a>OLE DB 대상을 사용하여 삽입을 처리하려면  
  
1.  **데이터 흐름** 탭에서 OLE DB 대상을 추가합니다.  
  
2.  삽입을 포함하는 출력을 조건부 분할 변환에서 OLE DB 대상에 연결합니다.  
  
3.  **OLE DB 대상 편집기**의 **연결 관리자** 페이지에서 다음 옵션을 선택합니다.  
  
    1.  대상 데이터베이스에 대한 OLE DB 연결 관리자를 선택하거나 만듭니다.  
  
    2.  **데이터 액세스 모드** 옵션을 선택한 다음 대상 테이블을 선택하거나 대상 열을 포함하는 SQL 문을 입력합니다.  
  
4.  편집기의 **매핑** 페이지에서 변경 데이터의 적절한 열을 대상 테이블에 매핑합니다.  
  
## <a name="applying-updates"></a>업데이트 적용  
 업데이트를 적용하려면 OLE DB 명령 변환을 사용합니다. 매개 변수가 있는 UPDATE 문을 사용하여 새 열 값으로 한 번에 한 행을 업데이트해야 하기 때문에 이 변환을 사용합니다.  
  
> [!NOTE]  
>  대상 구성 요소를 사용하여 업데이트를 적용할 수도 있습니다. 이 방법을 사용할 때는 대상 구성 요소를 사용하여 해당 용도로 만든 임시 테이블에 행을 저장합니다. 그런 다음 SQL 실행 태스크를 사용하여 임시 테이블의 대상에 대해 대량 업데이트 및 대량 삭제 작업을 수행합니다.  
  
#### <a name="to-process-updates-by-using-an-ole-db-command-transformation"></a>OLE DB 명령 변환을 사용하여 업데이트를 처리하려면  
  
1.  **데이터 흐름** 탭에서 OLE DB 명령 변환을 추가합니다.  
  
2.  업데이트를 포함하는 출력을 조건부 분할 변환에서 OLE DB 명령 변환에 연결합니다.  
  
3.  **고급 OLE DB 명령 편집기**의 **연결 관리자** 탭에서 대상 데이터베이스에 대한 OLE DB 연결 관리자를 선택하거나 만듭니다.  
  
4.  **고급 OLE DB 명령 편집기**의 **구성 요소 속성** 탭에 있는 **SqlCommand**에 매개 변수가 있는 UPDATE 문을 입력합니다.  
  
     예를 들어 Customer 테이블에 대한 UPDATE 문에는 다음 구문이 있을 수 있습니다.  
  
    ```  
    update CDCSample.Customer  
    set TerritoryID  = ?,  
        CustomerType  = ?,  
        rowguid  = ?,  
        ModifiedDate  = ?  
    where CustomerID = ?  
  
    ```  
  
5.  편집기의 **열 매핑** 탭에서 변경 데이터의 적절한 열을 UPDATE 문의 매개 변수에 매핑합니다.  
  
## <a name="applying-deletes"></a>삭제 적용  
 삭제를 적용하려면 OLE DB 명령 변환을 사용합니다. 행을 고유하게 식별하는 열 값을 기반으로 한 번에 한 행을 삭제하는 매개 변수가 있는 DELETE 문을 사용해야 하기 때문에 이 변환을 사용합니다.  
  
> [!NOTE]  
>  대상 구성 요소를 사용하여 삭제를 적용할 수도 있습니다. 이 방법을 사용할 때는 대상 구성 요소를 사용하여 해당 용도로 만든 임시 테이블에 행을 저장합니다. 그런 다음 SQL 실행 태스크를 사용하여 임시 테이블의 대상에 대해 대량 업데이트 및 대량 삭제 작업을 수행합니다.  
  
#### <a name="to-process-deletes-by-using-an-ole-db-command-transformation"></a>OLE DB 명령 변환을 사용하여 삭제를 처리하려면  
  
1.  **데이터 흐름** 탭에서 데이터 흐름에 OLE DB 명령 변환을 추가합니다.  
  
2.  삭제를 포함하는 출력을 조건부 분할 변환에서 OLE DB 명령 변환에 연결합니다.  
  
3.  고급 편집기를 열어 변환을 구성합니다.  
  
4.  **고급 OLE DB 명령 편집기**의 **연결 관리자** 탭에서 대상 데이터베이스에 대한 OLE DB 연결 관리자를 선택하거나 만듭니다.  
  
5.  **고급 OLE DB 명령 편집기**에 있는 편집기의 **구성 요소 속성** 탭에서 **SqlCommand**에 매개 변수가 있는 DELETE 문을 입력합니다.  
  
     예를 들어 Customer 테이블에 대한 DELETE 문에는 다음 구문이 있을 수 있습니다.  
  
    ```  
    delete from Customer where CustomerID = ?  
  
    ```  
  
6.  편집기의 **열 매핑** 탭에서 변경 데이터의 적절한 열을 DELETE 문의 매개 변수에 매핑합니다.  
  
## <a name="optimizing-inserts-and-updates-by-using-merge-functionality"></a>MERGE 기능을 사용하여 삽입 및 업데이트 최적화  
 Transact-SQL MERGE 키워드와 특정 변경 데이터 캡처 옵션을 함께 사용하여 삽입 및 업데이트 처리를 최적화할 수 있습니다. MERGE 키워드에 대한 자세한 내용은 [MERGE&#40;Transact-SQL&#41;](/sql/t-sql/statements/merge-transact-sql)를 참조하세요.  
  
 변경 데이터를 검색하는 Transact-SQL 문에서 *cdc.fn_cdc_get_net_changes_<capture_instance>* 함수를 호출할 때 *all with merge*를 **row_filter_option** 매개 변수의 값으로 지정할 수 있습니다. 이 변경 데이터 캡처 함수는 삽입과 업데이트를 구분하는 데 필요한 추가 처리를 수행할 필요가 없을 때 보다 효율적으로 작동합니다. *all with merge* 매개 변수 값을 지정할 때 변경 데이터의 **__$operation** 값은 삭제의 경우 1이고 삽입 또는 업데이트로 인한 변경의 경우 5입니다. 변경 데이터를 검색하는 데 사용되는 Transact-SQL 함수에 대한 자세한 내용은 [변경 데이터 검색 및 이해](retrieve-and-understand-the-change-data.md)를 참조하세요. *all with merge* 매개 변수 값을 사용하여 변경 내용을 검색한 후 삭제를 적용하고 나머지 행을 임시 테이블 또는 준비 테이블에 출력할 수 있습니다. 그런 다음 다운스트림 SQL 실행 태스크에서 단일 MERGE 문을 사용하여 준비 테이블의 모든 삽입 또는 업데이트를 대상에 적용할 수 있습니다.  
  
  
