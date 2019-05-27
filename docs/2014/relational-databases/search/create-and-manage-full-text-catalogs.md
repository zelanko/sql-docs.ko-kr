---
title: 전체 텍스트 카탈로그 만들기 및 관리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text search [SQL Server], using SQL Server Management Studio
ms.assetid: 824b7131-44a6-4815-89e6-62b7bab060e3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d90ba7f8e183beeeeefe25ea20834b07d7a1bf80
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011467"
---
# <a name="create-and-manage-full-text-catalogs"></a>전체 텍스트 카탈로그 만들기 및 관리
  전체 텍스트 카탈로그는 파일 그룹에 속하지 않는 가상 개체이며, 전체 텍스트 인덱스의 그룹을 가리키는 논리적인 개념입니다.  
  
##  <a name="creating"></a> 전체 텍스트 카탈로그 만들기  
  
#### <a name="to-create-a-full-text-catalog"></a>전체 텍스트 카탈로그를 만들려면  
  
1.  개체 탐색기에서 서버, **데이터베이스**를 차례로 확장한 다음 전체 텍스트 카탈로그를 만들려는 데이터베이스를 확장합니다.  
  
2.  **스토리지**를 확장한 다음 **전체 텍스트 카탈로그**를 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **새 전체 텍스트 카탈로그**를 선택합니다.  
  
4.  **새 전체 텍스트 카탈로그** 대화 상자에서 다시 만들려는 카탈로그에 대한 정보를 지정합니다. 자세한 내용은 [새 전체 텍스트 카탈로그&#40;일반 페이지&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)를 참조하세요.  
  
    > [!NOTE]  
    >  전체 텍스트 카탈로그 ID는 00005부터 시작하고 카탈로그를 새로 만들 때마다 1씩 증가합니다.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
  
##  <a name="props"></a> 전체 텍스트 카탈로그의 속성 보기  
 FULLTEXTCATALOGPROPERTY와 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수를 사용하여 전체 텍스트 인덱싱에 관련된 다양한 속성의 값을 얻을 수 있습니다. 이 정보는 전체 텍스트 검색을 관리하고 이러한 검색에서 발생하는 문제를 해결하는 데 유용합니다.  
  
 다음 표에서는 전체 텍스트 카탈로그에 관련된 속성을 나열합니다.  
  
|속성|Description|기능|  
|--------------|-----------------|--------------|  
|`AccentSensitivity`|악센트 구분 설정입니다.|[FULLTEXTCATALOGPROPERTY](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)|  
|`ImportStatus`|전체 텍스트 카탈로그를 가져올지 여부를 나타냅니다.|FULLTEXTCATALOGPROPERTY|  
|`IndexSize`|전체 텍스트 카탈로그의 크기(MB)입니다.|FULLTEXTCATALOGPROPERTY|  
|`ItemCount`|현재 전체 텍스트 카탈로그에 있는 전체 텍스트 인덱싱된 항목 수입니다.|FULLTEXTCATALOGPROPERTY|  
|`MergeStatus`|마스터 병합의 진행 여부를 나타냅니다.|FULLTEXTCATALOGPROPERTY|  
|`PopulateCompletionAge`|마지막 전체 텍스트 인덱스 채우기가 완료된 시간과 01/01/1990 00:00:00 사이의 차이(초)입니다.|FULLTEXTCATALOGPROPERTY|  
|`PopulateStatus`|채우기 상태입니다.<br /><br /> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|FULLTEXTCATALOGPROPERTY|  
|`UniqueKeyCount`|전체 텍스트 카탈로그에서 고유 키 번호입니다.|FULLTEXTCATALOGPROPERTY|  
  
  
  
##  <a name="rebuildone"></a> 전체 텍스트 카탈로그 다시 작성  
  
#### <a name="to-rebuild-a-full-text-catalog"></a>전체 텍스트 카탈로그를 다시 작성하려면  
  
1.  개체 탐색기에서 서버, **데이터베이스**를 차례로 확장한 다음 다시 작성할 전체 텍스트 카탈로그가 포함된 데이터베이스를 확장합니다.  
  
2.  **스토리지**를 확장한 다음 **전체 텍스트 카탈로그**를 확장합니다.  
  
3.  다시 작성하려는 전체 텍스트 카탈로그의 이름을 마우스 오른쪽 단추로 클릭하고 **다시 작성**을 선택합니다.  
  
4.  **전체 텍스트 카탈로그를 삭제하고 다시 작성하시겠습니까?** 라는 질문에 **확인**을 클릭합니다.  
  
5.  **전체 텍스트 카탈로그 다시 작성** 대화 상자에서 **닫기**를 클릭합니다.  
  
  
  
##  <a name="rebuildall"></a> 데이터베이스에 대 한 모든 전체 텍스트 카탈로그를 다시 작성  
  
#### <a name="to-rebuild-the-full-text-catalogs-for-a-database"></a>데이터베이스의 전체 텍스트 카탈로그를 다시 작성하려면  
  
1.  개체 탐색기에서 서버, **데이터베이스**를 차례로 확장한 다음 다시 작성할 전체 텍스트 카탈로그가 포함된 데이터베이스를 확장합니다.  
  
2.  **스토리지**를 확장한 다음 **전체 텍스트 카탈로그**를 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **모두 다시 작성**을 선택합니다.  
  
4.  **전체 텍스트 카탈로그를 모두 삭제하고 다시 작성하시겠습니까?** 라고 질문에 **확인**을 클릭합니다.  
  
5.  **전체 텍스트 카탈로그 모두 다시 작성** 대화 상자에서 **닫기**를 클릭합니다.  
  
  
  
##  <a name="removing"></a> 데이터베이스에서 전체 텍스트 카탈로그 제거  
  
#### <a name="to-remove-a-full-text-catalog-from-a-database"></a>데이터베이스에서 전체 텍스트 카탈로그를 제거하려면  
  
1.  개체 탐색기에서 서버, **데이터베이스**를 차례로 확장한 다음 제거할 전체 텍스트 카탈로그가 포함된 데이터베이스를 확장합니다.  
  
2.  **스토리지**를 확장한 다음 **전체 텍스트 카탈로그**를 확장합니다.  
  
3.  제거할 전체 텍스트 카탈로그를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 선택합니다.  
  
4.  **개체 삭제** 대화 상자에서 **확인**을 클릭합니다.  
  
  
  
## <a name="see-also"></a>관련 항목  
 [CREATE FULLTEXT CATALOG&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)  
  
  
